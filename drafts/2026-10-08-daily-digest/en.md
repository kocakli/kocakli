---
title: "Claude Haiku 5.5 Meets GPT-6 Luna at Ten Cents"
slug: "claude-haiku-5-5-gpt-6-luna-price-floor"
excerpt: "Anthropic matches GPT-6 Luna pricing, ChatGPT gets a visual GPT-6 interface, and Microsoft puts coding agents on local hardware."
focuskw: "Claude Haiku 5.5"
yoast_title: "Claude Haiku 5.5 Meets GPT-6 Luna at Ten Cents"
yoast_metadesc: "Claude Haiku 5.5 matches GPT-6 Luna pricing as ChatGPT adds Intelligent UI and Microsoft pushes local, sandboxed agents."
categories: "832, 830"
---

Claude Haiku 5.5 has pulled the small-model price floor down to ten cents per million input tokens, matching GPT-6 Luna. That matters because agent systems make many cheap, narrow calls around the occasional difficult one. Wednesday also brought GPT-6 to ChatGPT, a Microsoft machine for local agents, a public SynthID checker, and a dispute over visible AI reasoning.

## 💸 Claude Haiku 5.5 meets the ten-cent price floor
<!-- INLINE: haiku-price-floor -->

[Anthropic released](https://www.anthropic.com/claude-haiku-5-5) its third 5.5 model in about a month. For prompts up to 100K tokens, Haiku costs $0.10 per million input tokens and $0.50 per million output tokens. Cache reads cost $0.01. OpenAI gives [GPT-6 Luna](https://developers.openai.com/api/docs/pricing) the same API list prices.

Past 100K, Haiku jumps fivefold to $0.50 input, $2.50 output, and $0.05 for cache reads. Anthropic says roughly 90% of Haiku 4.5 requests stayed below that line. Its average estimate is around 75% cheaper to run after accounting for a new tokenizer, while short requests are 90% cheaper. Haiku 4.5 cost $1 and $5.

Anthropic calls this its cheapest, fastest and most capable small model so far. The jobs it names are wonderfully unglamorous: summaries, context compactions, database queries, classification, customer support and browser use. It can also sit beneath [Opus 5.5](https://www.oguzhan.co/claude-opus-5-5-deep-dive/) or Sonnet 5.5 as a coding subagent. This is the first Haiku with adjustable effort.

The benchmark figures are Anthropic's own. Haiku scored 72.4% on the OSWorld 2.1 offline subset, against 48.9% for Luna and 83.9% for Sonnet 5.5. On Terminal-Bench 4.0 it posted 39.2%, versus 16.4% for Luna and 70.6% for Sonnet. Anthropic explicitly keeps Sonnet and Opus ahead for complex agentic coding.

My practical note is simple: keep small-agent prompts short. The hundreds of summaries, lookups and [compactions](https://www.oguzhan.co/jev-context-compaction-verbatim-prune/) around a hard model call just became much cheaper, but crossing 100K tokens changes the bill fast.

## 🧩 GPT-6 draws the interface as it answers

[GPT-6 arrived in ChatGPT](https://openai.com/index/gpt-6-for-everyone/) on 7 October for Plus, Pro, Business and Enterprise users. Free and Go users get it today. Paid plans use GPT-6 Sol in Chat, while Free and Go use GPT-6 Luna. Work and Codex models stay unchanged.

The visible change is Intelligent UI. GPT-6 can mix prose with graphics, tappable buttons, forms, charts and small tools, rendered progressively from native streamable components. OpenAI's examples include a bill splitter, a retirement calculator, a retro game and a mapped road trip. Users can reduce the visuals, and OpenAI concedes that its design judgment still needs work.

Answers can now appear while the model is thinking. In OpenAI's internal web-search evaluation, GPT-6 Instant began answering 44% sooner on average than GPT-5.6 Instant. That is a vendor test. The safety pitch also builds on Astra work and claims stronger resistance to multi-turn jailbreaks.

For many people in Turkey, the free tier effectively is ChatGPT. A model-generation jump is substantial. Generated mini-tools could be genuinely handy too, although I would check every number before letting an improvised calculator near money. Our earlier [GPT-6 Sol and Luna deep dive](https://www.oguzhan.co/gpt-6-sol-luna-deep-dive/) has the wider pricing context.

## 💻 Microsoft puts local agents inside a sandbox
<!-- INLINE: local-agent-sandbox -->

Microsoft's answer to cloud token pricing is ["hybrid intelligence"](https://blogs.windows.com/windowsexperience/2026/10/07/building-windows-for-hybrid-intelligence/): run agents locally where sensible, then call the cloud when needed. Its new Surface Laptop Ultra starts at $2,599, ships on 16 October, and pairs NVIDIA RTX Spark with up to 128 GB of unified memory and up to one petaflop of AI compute.

MAI Code 1.1 Flash has 137B total parameters with 6.8B active, quantized to about three bits, plus a 256K local context. Microsoft's own Surface test peaked at 75.5 GB of memory at full context. It measured prompt processing at 923.5 tokens per second at 64K and 769.8 at 128K. Microsoft also says local calls carry no inference charge.

That memory figure is the useful reality check. This is specialist hardware paid for up front. The broader idea may be MXC, Microsoft Execution Containers, now generally available on Windows 11. Organizations can specify the files and networks an agent may reach, with those limits enforced at runtime. MXC is open source and works across operating systems.

Containment is where local agents become credible. Codex, GitHub Copilot, Replit, LM Studio and several others already support MXC, with Claude Code among the tools listed as coming. Microsoft is giving Windows an OS-level answer to the same permissions problem I examined in [Apple's Full Disk Access rules for AI agents](https://www.oguzhan.co/apple-full-disk-access-ai-agents/).

## 🔍 SynthID Detector opens its doors

[Google has opened SynthID Detector](https://blog.google/innovation-and-ai/models-and-research/google-deepmind/synth-id-ai-content/) globally at synthid.com. The English-language tool checks images, video and audio for SynthID watermarks from Google and partners OpenAI, NVIDIA and Kakao. Apple support is listed as coming soon.

Google says more than 180 billion images and videos, plus 240,000 years of audio, have received the watermark since 2023. Verification built into Search, Gemini and Chrome handles more than one million requests each day.

The public site is narrower. [Ars Technica reports](https://arstechnica.com/ai/2026/10/google-rolls-out-improved-synthid-ai-content-detector-now-available-globally/) that sign-in is required, the daily quota is approximately ten checks, and the result no longer highlights marked regions as the internal tool did. Microsoft and Meta use their own watermarking standards, and detection tools can fail.

My reading of a clean result is deliberately limited: it says the checker found no SynthID mark. It cannot certify human authorship. Still, one place to check marks from several labs is useful for a journalist or anyone examining a viral clip. Ten daily tries make it a spot checker rather than a newsroom pipeline.

## 🧯 Fired researchers ask OpenAI to preserve visible reasoning

Three researchers fired by OpenAI last week, Tomek Korbak, Mikita Balesni and Jasmine Wang, have written to its board and safety committees. [The Wall Street Journal reports](https://www.wsj.com/tech/ai/fired-openai-researchers-ask-company-to-preserve-visibility-into-ai-reasoning-987c8c94) that they urged frontier labs to avoid developments that further reduce monitorability, use third-party auditors, and support an open safety ecosystem.

Their letter says the dismissals are chilling remaining staff. OpenAI replied that the firings concerned sensitive company information rather than speaking up about safety, and an internal memo said it strongly agreed with the recommendations. The tension matters because Astra-class models could evade chain-of-thought monitors under adversarial conditions, according to the system-card context covered by [Gizmodo](https://gizmodo.com/3-fired-openai-employees-write-plea-for-chain-of-thought-monitoring-to-be-preserved-2000823349). I would like that shared position recorded as a commitment in the next system card.

Wednesday looked like a pricing day wearing product-day clothes. Small calls reached ten cents, the free tier moved to GPT-6, and Microsoft offered local inference to buyers who can cover the hardware. The harder questions, whether we can inspect reasoning and verify synthetic media, moved a little as well. I will take the movement without pretending the questions are settled.
