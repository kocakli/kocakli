---
title: "LiteLLM supply chain attack, Block's Dessa, and two small models"
slug: litellm-supply-chain-attack-block-dessa-nanbeige
excerpt: "PyPI carried a malicious LiteLLM 1.107.0 for about two hours on 21 October. The 23 October root-cause post traces the breach to an Agent Platform master key that was flagged and never revoked."
focuskw: "LiteLLM supply chain attack"
yoast_title: "LiteLLM supply chain attack: the key never revoked"
yoast_metadesc: "The LiteLLM supply chain attack began with a master key nobody revoked. Malicious 1.107.0 was on PyPI for about two hours. Dessa and two small models too."
---

A compromised `litellm==1.107.0` sat on PyPI for about two hours on 21 October. The LiteLLM supply chain attack, in LiteLLM's [root-cause post](https://docs.litellm.ai/blog/security-incident-oct-21-2026-attack-chain) of 23 October, starts from an Agent Platform master key flagged in May 2026 and never revoked. I read the posts, the Dessa page, both cards, and the Swedish reports.

## 🔐 The LiteLLM supply chain attack started with a key that was never revoked
<!-- INLINE: litellm-attack-chain -->

LiteLLM is a widely used open-source Python gateway to many LLM providers. On 21 October seven wheels of malicious `litellm==1.107.0` hit PyPI from 11:39:51 to 11:40:13 UTC, then Docker Hub and GHCR at 11:46:56 UTC. The [incident post](https://docs.litellm.ai/blog/security-incident-oct-21-2026) says those builds carried compiled malware that steals credentials and loads remote-code execution tools. PyPI quarantined them by 13:23 UTC. Docker Hub tags `v1.107.0`, `latest`, `main-latest`, and `main-stable` lasted until 14:20 UTC. GHCR tags were unavailable by 13:51 UTC. GitHub's v1.107.0 source tag had no malicious files. The build came from lookalike `Berri-AI/litellm`. The real org is `BerriAI`.

Oliver Jensen and Mateo Wang published the root-cause account at 21:00 UTC on 23 October. LiteLLM calls it the canonical source of truth. On 27 May 2026 `opencode.json`, with the Agent Platform master key, was committed to public `LiteLLM-Labs/lite-harness`. Agent Platform is an internal experimental service for self-hosted cloud agents that open pull requests. The commit was force-pushed over. The key was flagged for revocation and never revoked.

On 10 October the key called `GET /api/v1/managed_agents/agents?limit=100` and returned every managed agent config, including the GitHub CLI OAuth token of one of two GitHub organization owners. The token was not a scoped service account. LiteLLM notes that GitHub CLI tokens come after 2FA and skip GitHub's sudo-style re-auth. Throwaway CI branches that night posted secrets to webhook.site and yielded two more maintainer tokens. More private-repo secrets left on 12 October.

On 21 October branch protection rejected a push to the private release repo. Five seconds later the owner's token overrode it and pointed the workflow at the lookalike fork. A second stolen maintainer token approved the production gate. Normally that gate needs a special account locked to a physical device in the office. Earlier that week any two engineers could trigger and approve releases, for faster bugfix backports. I wrote about approval gates in the [24 October Claude Duet piece](https://www.oguzhan.co/claude-duet-proactive-agent-approvals-limits/). A third token deleted the workflow records. Then `main` was force-pushed clean.

LidorMachluf opened issue #47826 at 12:06 UTC. LiteLLM says the release was caught within 20 minutes of publication. Incident response began at 13:02 UTC. Enterprise customers on the private registry were not affected. From the root-cause post: "This incident has provided a strong illustration of the risks associated with failing to rotate a potentially exposed key." The 21 October post blamed logs of an internal LiteLLM deployment. The root-cause post drops that. The first token came from the Agent Platform API.

Incident post: that PyPI window and those Docker Hub tags are affected. Do not run pip first. Any Python start re-runs `cook.pth` and `sitecustomize.py`.

- Delete `cook.pth` and `sitecustomize.py` from the shell before you start Python.
- Pin `litellm==1.106.2`, or rebuild from scratch.
- Rotate provider keys in the proxy database, master and virtual keys, the `DATABASE_URL` password, and the cloud role.

## 🎙️ What makes Block's Dessa different from other voice AI?
<!-- INLINE: dessa-full-duplex -->

Block announced Dessa on Friday 23 October. The [Dessa page](https://block.xyz/dessa) describes full-duplex speech-to-speech: audio in, audio out, listening and talking at once, cutting in, backchannel "yeah" or "got it".

Block says training was from scratch on human conversation only. No text. No pretrained model. As far as Block knows, this is the first realistic live-conversation AI trained only from human speech. Inference is faster than real time on a MacBook Pro M4 Max or better. Training used one NVIDIA GB200 NVL72. Former members of the Toronto startup Dessa founded the small lab inside Block. It reports directly to Jack Dorsey. Ragavan Thurairatnam leads it.

Dessa is not a product. No public API. No open weights. Early access is a small group of AI safety researchers, for risks Block has not anticipated. Block's line: "Imagine being in serious pain while a voice AI has no idea and just keeps going." I read the page. It includes a clip of Dessa with OpenAI's GPT-Live-1, both AI voices. [The Verge](https://www.theverge.com/ai-artificial-intelligence/1017906/jack-dorsey-block-dessa-ai-voice-speech), on 23 October, called some chats "a little awkward and uncanny". The model once mistook a speaker for "Ronaldo".

## 🧩 Two small open models for local agents

I read both cards.

[Nanbeige4.3-33B](https://huggingface.co/Nanbeige/Nanbeige4.3-33B) is the Nanbeige team's flagship teacher. According to the card, at the highest thinking effort and the same harness, Terminal-Bench 2.1 is 80.9. Nanbeige does not win every benchmark. SWE-Bench Pro is 60.3 (Qwen3.8-27B 61.7), GDPval 84.8 (a listed 86.4), GPQA Diamond 89.5 (Gemma4-31B 91.3). Serving examples use 4-way tensor parallelism in SGLang and vLLM, so the BF16 weights are not a laptop model. Muse Glimmer is the consumer-GPU model from the [22 October digest](https://www.oguzhan.co/deepseek-deepinfer-eagle-4-muse-glimmer/).

NVIDIA post-trained [Nemotron 3.5 Bolt E4B](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Bolt-E4B-BF16) from Google's Gemma-4-E4B-it. GA was 23 October, text in and text out. NVIDIA says the OpenMDW-1.1 weights are ready for commercial use. The Gemma 4 base stays Apache 2.0. According to the card, Tau2-Bench is 55.10 against 38.50 for base Gemma 4 E4B-it. Qwen3.5 4B scores 75.06 on Tau2-Bench in that comparison, so Bolt does not lead there. The table's IFBench figure is that card's claim.

| | Nanbeige4.3-33B | Nemotron 3.5 Bolt E4B |
|---|---|---|
| Parameters | 33B | 8B (4B effective) |
| License | Apache 2.0 | OpenMDW-1.1 |
| Context | 512K tokens | 64K in, 64K out |
| Built for | Coding and office agents | Local voice and device assistants |
| Headline claim | Terminal-Bench 2.1: 80.9 | IFBench: 63.79 (base Gemma 4 E4B: 42.84) |
| Released | 24 to 25 Oct (Hugging Face) | 23 Oct (Hugging Face, build.nvidia.com) |

## 🇸🇪 What did Sweden's government offices block?

From today, Monday 26 October, Regeringskansliet work computers block the ChatGPT and Claude web interfaces. Regeringskansliet is the Swedish Government Offices. [SVT](https://www.svt.se/nyheter/inrikes/ai-tjanster-sparras-pa-regeringskansliet) reported it on 23 October, updated 24 October, citing [Sveriges Radio Ekot](https://www.sverigesradio.se/artikel/chat-gpt-och-claude-forbjuder-regeringskansliet). Staff are pointed to Microsoft Copilot, approved by the offices, with security raised after a review. An email to SVT says the models stay reachable through Intric. The block is the browser chat window.

After the LiteLLM timeline I want a list of which of my tokens sit inside agent tools. I have not made that list yet.

## Sources

[LiteLLM root-cause post](https://docs.litellm.ai/blog/security-incident-oct-21-2026-attack-chain)
[LiteLLM incident post](https://docs.litellm.ai/blog/security-incident-oct-21-2026)
[Block Dessa](https://block.xyz/dessa)
[The Verge](https://www.theverge.com/ai-artificial-intelligence/1017906/jack-dorsey-block-dessa-ai-voice-speech)
[Nanbeige4.3-33B](https://huggingface.co/Nanbeige/Nanbeige4.3-33B)
[Nemotron 3.5 Bolt E4B](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Bolt-E4B-BF16)
[SVT](https://www.svt.se/nyheter/inrikes/ai-tjanster-sparras-pa-regeringskansliet)
[Sveriges Radio](https://www.sverigesradio.se/artikel/chat-gpt-och-claude-forbjuder-regeringskansliet)
