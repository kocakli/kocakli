---
title: "DeepSeek DeepInfer puts the serving stack on GitHub"
slug: "deepseek-deepinfer-eagle-4-muse-glimmer"
excerpt: "DeepSeek opened DeepInfer, the Apache 2.0 inference engine behind V4.1-Flash. EAGLE-4 is source-available, Muse Glimmer's report covers a 30B on-device agent, and Viggle prices a 3D scene in cents."
focuskw: "DeepSeek DeepInfer"
yoast_title: "DeepSeek DeepInfer opens the serving stack"
yoast_metadesc: "DeepSeek DeepInfer is Apache 2.0 offline inference for V4.1-Flash. EAGLE-4 is source-available, Muse Glimmer fits a GPU, Viggle prices a 3D scene in cents."
---

DeepSeek DeepInfer is public: offline Apache 2.0 inference for DeepSeek-V4.1-Flash, posted 20 October 2026 at 09:30 UTC (12:30 Istanbul). Eagle's EAGLE-4, Meta's 30B Muse Glimmer report and Viggle's 3D-scene claim (under a cent of compute) landed across the same two days. I read the repos, papers, posts and price pages, and I did not install, run or benchmark any of it.

## 🧰 DeepSeek DeepInfer: the serving stack goes public
<!-- INLINE: deepinfer-serving-stack -->

[DeepSeek's post on X](https://x.com/deepseek_ai/status/2112476496283775135) says "Introducing DeepInfer, our in-house inference framework, now fully open source!" It powers DeepSeek-V4.1-Flash at scale, shared "to help the community lower compute costs, reduce energy use, and make AI more affordable."

The [README](https://github.com/deepseek-ai/DeepInfer) calls DeepInfer "the high-performance inference framework that powers DeepSeek's large-scale production services" and says this release "provides offline inference." Apache 2.0. Only DeepSeek-V4.1-Flash, default checkpoint deepseek-ai/DeepSeek-V4.1-Flash-1017, the weights from the [19 October digest](https://www.oguzhan.co/openai-misalignment-reports-claude-ecdsa-seeds/). Hardware: NVIDIA SM100 GPUs and Huawei Ascend 950 NPUs. Needs Linux, Python 3.12, CUDA 13 (NVIDIA) or CANN 9.2 (Ascend).

Included: optimized kernels, attention DP / balanced CP, MoE expert parallelism with EPLB, DSpark and confidence-scheduled verification for speculative decoding, SWA bounded replay, an asynchronous zero-overhead batch scheduler, batch-invariant inference, deterministic sampling, structured outputs. The engine note says the code is derived from vLLM and modified by DeepSeek.

Absent: a KV cache system, prefill/decode disaggregation, load balancing across replicas. According to [DeepSeek's deployment Q&A](https://github.com/deepseek-ai/DeepInfer/blob/main/doc/inference_deployment_qa.md), KV cache management and load balancing are "tightly coupled to our internal infrastructure, so that code is not yet fully open-sourced." No online-serving wrapper ships. One cluster serves 155 trillion tokens a day. Overall revenue is US$38 per GPU-hour "at valley pricing." KV cache is kept for more than 72 hours. The smallest efficient unit is 64 prefill GPUs plus 64 decode GPUs, decode at EP64 or above. Storage is about 14.4 TB per GPU (logical size).

[deepseek-recipe](https://github.com/deepseek-ai/deepseek-recipe) (MIT on GitHub) maps mainstream LLM API protocols to token sequences, "fully aligned with the official DeepSeek API." Later models' inference code will land in DeepInfer too, DeepSeek says.

128 GPUs is the floor for providers and large self-hosters. KV cache and the load balancer stayed internal.

## 🦅 Does EAGLE-4 stay fast when the queue fills?
<!-- INLINE: eagle-4-draft-tree -->

A small drafter guesses several next tokens, the target model verifies them in one pass, and the [EAGLE-4 repo](https://github.com/eagle-hq/EAGLE-4) says the drafter "keeps the target model's output distribution." One drafter is trained per target model and sizes its tree from measured drafting and verification costs for that batch, hardware and workload. Warm-up stores the costs in EAGLE-Harness tables. [Eagle's blog](https://blog.eagle.ai/blog/introducing-eagle-4) (20 October 2026) says a draft tree that helps at low concurrency "can become expensive under load."

Same post, same engine, Qwen3.8-27B, 4x NVIDIA B300, TP4, T=0. One request, then the 512 aggregate: vanilla 240.5 tok/s and 21,203, DSpark 618.6 and 14,229, DFlash 2 672.6 and 16,641, EAGLE-4 863.8 and 28,340. At 512, DSpark and DFlash 2 fall below vanilla and EAGLE-4 stays above. TokenSpeed's single-request figure is 961.6 tok/s, the SGLang reference 837.6. Nemotron 3.5 Super VL, 4x B300: 647 tok/s and 33,480, listed as 2.74x and 1.69x vanilla.

Plugins: SGLang, vLLM, and experimental TokenSpeed (patched wheels and images, because stock engines lack the hooks). According to [AMD](https://x.com/AIatAMD/status/2112659635295404176), day-0 Instinct MI355X support reaches about 300 tok/s on one Qwen3.8-27B BF16 GPU, 1.6x built-in MTP.

Reposts called it open source. The repo says EAGLE-4 is "source-available software, not OSI-approved open-source software." Commercial use is limited to aggregate revenue under US$20 million over 12 months. A "Competing Offering" needs a separate commercial license regardless of revenue.

## 💻 Muse Glimmer: Meta's 30B agent on one consumer GPU

On 19 October 2026, [AI at Meta](https://x.com/AIatMeta/status/2112265822274302066) published a technical report on Muse Glimmer, "our 30B open-weight model built for agentic tasks on consumer hardware," which "runs at practical speeds on a Mac or PC with a single consumer GPU at 4-bit precision."

The [model card](https://huggingface.co/meta-models/Muse-Glimmer-30B) dates the weights to August 2026. The new document is the report. The weights had one line in the [15 October digest](https://www.oguzhan.co/muse-wonder-gemini-4-argon-frontier-agents/), after Alexandr Wang told Axios that Meta had recently open-sourced them.

The [technical report](https://arxiv.org/abs/2610.24628) (v2, 20 October 2026) and the [research page](https://ai.meta.com/research/publications/muse-glimmer-30b-an-on-device-agentic-model/): a dense causal transformer, about 29.6B parameters, including a perception encoder of about 1.8B. Text and image in, text out. Context 128K and above, 131,072 and above on the card. About 140 languages. Apache 2.0. Distilled from Muse Spark, which the report calls Meta's [frontier-class model](https://www.oguzhan.co/what-is-a-frontier-model/). Target: 32GB of dedicated memory, about 4-bit, plus a DFlash head. Quote: "practical speeds on a single RTX 5090 with minimal quality loss." No tok/s.

Agentic training used simulated "digital lives": a persona with 10 to 14 contacts and weeks of correspondence, calendar events, documents and messaging history, plus tools that mimic real argument and JSON formats.

[Meta's technical report](https://arxiv.org/abs/2610.24628) scores Muse Glimmer on high reasoning against Gemma4-31B thinking and Qwen3.6-27B thinking.

| Benchmark | Muse Glimmer | Gemma4-31B | Qwen3.6-27B |
|---|---|---|---|
| MCPAtlas (tool use) | 75.5 | 54.2 | 62.5 |
| SWE-Bench Pro | 51.2 | 36.9 | 50.2 |
| SWE-Bench Verified | 76.0 | 66.6 | 77.2 |
| OSWorld-Verified | 65.9 | 58.5 | 75.6 |

Glimmer leads on tool use. Qwen3.6-27B takes OSWorld-Verified and SWE-Bench Verified.

## 🌍 How cheap is a 3D scene now?

[Viggle's research post](https://viggle.ai/jst2) (19 October 2026) calls JST-2 (Joint Space-and-Time, generation 2) a "physics-native world foundation model." Persistent 3D atoms carry an explicit xyz, outside pixel and video space. Output is 3D Gaussian splats, rendered locally in the browser. Viggle's chart: about one second on an NVIDIA B200, "an inference cost below $0.01," World Labs' Marble at about 5 to 6 minutes. Up to 64 input views. One image can become an animation-ready, rigged character. Full-body motion can come from text or video.

The [API price page](https://viggle.ai/developers) lists $0.06 per prompt scene (6 credits, panorama first), $0.01 for other tasks, 100 free credits. Free in the PINOC app, also via API and MCP (Codex and Claude Code, Viggle says). Announcement: [Viggle on X](https://x.com/ViggleAI/status/2112202242048528540).

Collisions and object interactions still use rule-based physics. JST-3, in development, aims to learn those dynamics. JST-1 powered the meme app, which Viggle puts above 50 million users.

Four notes on the plumbing. The price cut I would watch sits in the serving layer, with EAGLE-4's license line beside the chart.

## Sources

[DeepInfer repository](https://github.com/deepseek-ai/DeepInfer)
[DeepInfer deployment Q&A](https://github.com/deepseek-ai/DeepInfer/blob/main/doc/inference_deployment_qa.md)
[deepseek-recipe](https://github.com/deepseek-ai/deepseek-recipe)
[DeepSeek on X](https://x.com/deepseek_ai/status/2112476496283775135)
[Eagle blog](https://blog.eagle.ai/blog/introducing-eagle-4)
[EAGLE-4 repository](https://github.com/eagle-hq/EAGLE-4)
[AMD on X](https://x.com/AIatAMD/status/2112659635295404176)
[Muse Glimmer research page](https://ai.meta.com/research/publications/muse-glimmer-30b-an-on-device-agentic-model/)
[Muse Glimmer technical report](https://arxiv.org/abs/2610.24628)
[Muse Glimmer model card](https://huggingface.co/meta-models/Muse-Glimmer-30B)
[AI at Meta on X](https://x.com/AIatMeta/status/2112265822274302066)
[Viggle JST-2](https://viggle.ai/jst2)
[Viggle API pricing](https://viggle.ai/developers)
[Viggle on X](https://x.com/ViggleAI/status/2112202242048528540)
