---
title: "China AI export controls: Beijing licenses the weights, not the API"
slug: "china-ai-export-controls-model-weights"
focus_keyphrase: "China AI export controls"
yoast_title: "China AI export controls: what the draft restricts"
meta_description: "China AI export controls in the Oct. 16, 2026 draft would license model weights above three lines. API, app and SaaS access stay outside the catalogue."
excerpt: "Announcement No. 48 of 2026 is a draft for comment until November 15. It would license frontier model weights, checkpoints and code, and it leaves API access outside the catalogue."
---

## What Beijing published on October 16

On October 16, 2026, at 16:00 Beijing time, the Ministry of Commerce and the Ministry of Science and Technology published Announcement No. 48 of 2026, a draft revision of the Catalogue of Technologies Prohibited or Restricted from Export (中国禁止出口限制出口技术目录). China AI export controls get their own headings. The licence sits on the file. Weights, checkpoints, source code and architecture need permission to leave China if a large model crosses any of three lines: training compute of 10^26 floating-point operations, 2 trillion parameters, or a global top-10 rank at the time of export. API, app, website, SaaS and lightweight on-device use do not count as a technology export. Comments close on November 15, 2026, by email to jinxianmulu@mofcom.gov.cn, by fax or by letter.

I read the announcement, the annex and the spokesperson's Q&A. I tested nothing and interviewed nobody. The catalogue text is a draft. Interim registration is already live on ecomp.mofcom.gov.cn until a revised catalogue takes effect.

## What is actually on the list?

The [announcement](https://www.mofcom.gov.cn/zcfb/blgg/gg/2026/art/2026/art_05e2643a8ca04eb9adf9dd0542991fe4.html) covers 40 technologies in three fields, 23 of them AI: large models, agents, compute clusters and information processing. The [Q&A](https://www.mofcom.gov.cn/xwfb/xwfyrth/art/2026/art_d7661dbf62794345a221404f82a25959.html) puts the full draft at 14 proposed prohibitions and 26 proposed restrictions. [CTOL](https://www.ctol.digital/news/china-draft-technology-export-catalogue-ai-model-weights-chip-design/) counted the AI items as 6 prohibited and 17 restricted. Biomedicine is 5 technologies, photovoltaics 12. Technology already public through open source or academic papers stays out.

Prohibited: malicious-code generation against critical infrastructure, defense or core government systems (266402J), large models trained on "core data" and offered as a service (266501J), and high-performance agents built specifically or mainly for those scenarios (266502J).

Restricted: frontier model core technology and "important data" models offered as a service (266504X), agent specifications (266505X), vulnerability discovery (266404X), chip design (266506X), compute clusters (266507X). Older entries also add deepfake detection at 98 percent or above, steganography, voiceprint recognition, and Chinese or minority-language translation. [Frontier Now](https://frontiernow.dev/en/news/china-ai-export-catalog-draft/) is right that these are AI's first own headings, written so a firm can test itself.

## China AI export controls draw three lines around a frontier model
<!-- INLINE_IMAGE_1 -->

Item 266504X restricts core technology if a large model meets any of three tests. Training compute of at least 10^26 floating-point operations. At least 2 trillion parameters, written as 20,000亿. Or a "globally leading level": top 10 worldwide at the time of export, in public evaluations by mainstream evaluators in China or abroad, or by large industry platforms, on overall performance, a specific business capability, global call volume, safety, training efficiency, and the note's "etc."

My reading: only the rank is measured at export, so a model can move into scope and back out as the boards move.

Core technology means weights, key checkpoints, source code, architecture, and training-optimization and inference-acceleration techniques.

Separate from those three lines: A model trained on "important data" and offered as a service is restricted under 266504X. Trained on "core data" and offered as a service, it is prohibited under 266501J. [Frontier Now](https://frontiernow.dev/en/news/china-ai-export-catalog-draft/) notes that both terms point at the Data Security Law and that neither is defined here. The exemption is a trace of 0.1 percent or less that cannot substantively lift core R&D capability in that domain, has been desensitized, and is never reproduced in outputs, or data that is legally public.

## Weights leave, APIs don't: what counts as an export
<!-- INLINE_IMAGE_2 -->

The [Q&A](https://www.mofcom.gov.cn/xwfb/xwfyrth/art/2026/art_d7661dbf62794345a221404f82a25959.html) makes scope a transfer question: does restricted technology move from inside China to somewhere else? Localized deployment abroad is a technology export. The same technology on the company's own overseas cloud is eligible for automatic licensing. API calls, an app or website, SaaS, or a lightweight on-device copy do not count as large-model technology export.

Automatic licensing also covers open-sourcing the restricted technology, Chinese firms building and running their own compute centers abroad, chip tape-out abroad, joint research using foreign resources, and international standards work. MOFCOM says this basically achieves "report and ship" (即报即出), and the annex footnotes repeat the list. Already-public technology stays out. World AI Cooperation Organization members are promised more facilitation on capacity building, technology sharing and joint rule-making, with support stated for the Global South. [CTOL](https://www.ctol.digital/news/china-draft-technology-export-catalogue-ai-model-weights-chip-design/) calls that a promise rather than a right, and says the carve-outs could vanish from the final text.

From October 16 until the revised catalogue takes effect, ecomp.mofcom.gov.cn covers ownership transferred abroad (an IP assignment is the example), domestic technology licensed for use abroad, an owner or actual controller becoming a foreign entity, and other cases MOFCOM names. Exports already started and unfinished are included. The record stores exporter, recipient, destination, technology, use and expected value. Products made with the controlled technologies are out of scope. Exporters judge for themselves. Once the measures apply, MOFCOM says, "the vast majority of AI technologies can still be exported freely."

## Agents, malware and bug hunters get their own numbers

Item 266505X gives four agent specifications.

- ≥20 steps from a natural-language instruction, decomposition accuracy ≥80%, average sub-task success ≥90%.
- ≥60 concurrent collaborating agents, time at or below twice the single-agent minimum for the same result, agreement with the standard answer ≥85%.
- ≥200 third-party tools, selection accuracy ≥90%, end-to-end success ≥90% on tasks needing three or more tools.
- Game decisions, every part required: depth ≥20 steps or ≥10 concurrent agents, decisions within 200 milliseconds, beats 90% of humans on standard benchmarks.

Anthropic allows 64 concurrent threads in [Claude Managed Agents](https://www.oguzhan.co/claude-managed-agents-dynamic-workflows/). Sixty and 64 are neighbors, not the same test. The annex also requires the speed and accuracy conditions, and the catalogue only binds exports of Chinese technology.

Item 266402J would prohibit AI-driven malicious-code generation and mutation against critical information infrastructure, defense and core government systems if attack success reaches ≥60% on multi-engine detectors, ≥85% on one mainstream antivirus, or ≥90% on machine learning models. Also in the item: adaptive evasion (detect sandboxes, debuggers and emulators, sandbox escape, rewrite ≥50% of the code structure per run) and bulk variants (≥20 equivalent variants per run, or ≥80% end-to-end automation). MOFCOM's reason is harm to critical systems or national-security defenses, including if non-state actors or malicious entities obtain the tools. Stated aims: keep AI "safe and controllable", and "ensure AI always remains under human control". [AI malware](https://www.oguzhan.co/closedquorum-malware-llm-c2-quorum/) is a separate case, not a reading of this item.

Item 266404X restricts vulnerability discovery on any of: ≥75% on authoritative benchmarks for reproduction and exploitability, exploit-chain success ≥50% against a mainstream operating system or browser (≥40% for arbitrary-code execution), ≥10× a senior security expert's efficiency, autonomously chaining two or more low or medium bugs into a multi-stage attack with a proof of concept, autonomously finding ≥5 previously undisclosed high-severity flaws or ≥50 undisclosed flaws in one major open-source project or OS in one pass, or a top level on mainstream exploit-capability rating systems. [Defenders-first AI bug hunting](https://www.oguzhan.co/gemini-4-argon-cyber-defenders-first/) is a different policy from this export line.

Meet those agent thresholds, built specifically or mainly for critical infrastructure, defense or core government use, and the item becomes prohibited 266502J. Chip triggers include 14 nm or finer process and 2.5D or 3D packaging. Clusters: bidirectional interconnect ≥800 GB/s, distributed-training fault tolerance with mean time to repair ≤120 seconds, large-scale as more than 10,000 AI accelerator cards. MOFCOM says it will drop what is no longer advanced. Institutes, industry groups and major companies were consulted first.

## Is this a copy of the US rule?

Both texts use 10^26.

| | US AI Diffusion Rule | China draft (Announcement 48) |
|---|---|---|
| Published | Jan 15, 2025 (BIS interim final rule) | Oct 16, 2026 (draft for comment until Nov 15) |
| Compute line | weights of closed models above 10^26 operations | ≥10^26 FLOPs, or ≥2T parameters, or global top 10 |
| Open weights | closed-weight models only | already public is out of scope, and new open-sourcing gets automatic licensing |
| What it targets | weights of the most advanced models plus advanced chips | model core tech (weights, checkpoints, code, architecture), agents, chip design, clusters. API, app and SaaS access is not an export per MOFCOM |
| Status | not enforced since May 13, 2025, still in the CFR (GAO) | interim registration live since Oct 16 |

[GAO B-337935](https://www.gao.gov/products/b-337935) (May 12, 2026) covers the US status. BIS issued the Framework for AI Diffusion on January 15, 2025, requiring licences for advanced chips and for weights of the most advanced models. On May 13, 2025 Commerce said it would not enforce the rule and started a rescission. GAO: the rescission is not final, the rule remains in the Code of Federal Regulations, and the non-enforcement announcement counts as a rule under the Congressional Review Act. Per the [Encyclopedia of Economic Statecraft](https://jamesjtennant.com/entries/ai-model-weights-and-frontier-models/), ECCN 4E091 covered weights of advanced closed-weight models trained above 10^26 operations.

Dean W. Ball, described by [The Decoder](https://the-decoder.com/china-plans-to-tighten-export-controls-on-open-weight-models-and-23-key-ai-technologies/) as head of strategic futures at OpenAI, said: "This move does not mean 'China is shutting down open-weight models,' but it does indicate the Chinese government establishing the optionality to shut down future open-weight models at will." He calls this a "mirror image" of US model-weight controls. Closed weights were the US object. This draft leaves already-public weights alone and offers automatic licensing when restricted technology is newly open-sourced.

The spokesperson cites Article 20 of the Foreign Trade Law, on a catalogue revised many times since 2001. [CTOL](https://www.ctol.digital/news/china-draft-technology-export-catalogue-ai-model-weights-chip-design/) places the draft on that law and the technology import and export regulations, apart from the Export Control Law that carried the dual-use lists. MOFCOM calls it "routine" and "not targeted at any specific country, region or entity". Ryan Etzcorn, senior director at Ankura China Advisors, told Bloomberg via [The Straits Times](https://www.straitstimes.com/business/china-plans-ai-export-curbs-to-exert-control-over-key-tech): "This is more than routine maintenance." And: "Beijing is signalling that steadier relations with the West do not mean it will stand still." The same account notes 2020, when algorithms were added after the first Trump administration threatened to ban TikTok unless it sold its US assets. July 2025, per [CTOL](https://www.ctol.digital/news/china-draft-technology-export-catalogue-ai-model-weights-chip-design/), deleted 3 entries, added 1 and modified 1, with no AI item. Forty proposed entries against five changes is the "large step" in CTOL's account.

## Who feels it first
<!-- INLINE_IMAGE_3 -->

Labs drawing models at 2 trillion parameters and up, if that line survives. Bloomberg, via [The Straits Times](https://www.straitstimes.com/business/china-plans-ai-export-curbs-to-exert-control-over-key-tech), names Kimi K3 and Alibaba's Qwen3.8-Max as examples above it. Alibaba said in September it plans models of 5 to 10 trillion parameters. Those are newsroom examples above a draft line, not a ruling that any named model is restricted.

A foreign buyer wanting a non-public restricted model on its own machines needs the Chinese vendor to hold a licence. Localized deployment abroad is the export. The vendor's own overseas cloud is the automatic-licensing path.

Matthias Bastian at [The Decoder](https://the-decoder.com/china-plans-to-tighten-export-controls-on-open-weight-models-and-23-key-ai-technologies/) argues that Europe's plan to run open-weight models in domestic clouds gets harder if the best open models come from the United States or China and can be cut off.

Released Chinese open weights are outside the draft. Public source and papers are excluded. The switch, if the wording holds, sits on future frontier open-weight releases and on deployment abroad, on the customer's machines, of technology still restricted.

Reuters, via [The Straits Times on July 8, 2026](https://www.straitstimes.com/asia/east-asia/beijing-is-looking-at-curbing-overseas-access-to-chinas-top-ai-models-sources-say), described MOFCOM meetings with Alibaba, ByteDance and Z.ai on restricting overseas access, including to unreleased models, closed and open. A May summary in a Supreme People's Court journal floated tiers: simple filing for basic open-source tools, security reviews for advanced ones, the most sensitive frontier models barred from public release or kept domestic. This draft leaves API, app, website and SaaS outside the export. July was about the call. October is about the file.

## What I'm watching before November 15

Whether 10^26 and 2 trillion survive the comments. [CTOL](https://www.ctol.digital/news/china-draft-technology-export-catalogue-ai-model-weights-chip-design/) leaves that open.

How "important data" and "core data" get defined. [Frontier Now](https://frontiernow.dev/en/news/china-ai-export-catalog-draft/) says both are left to later rules.

Whether automatic licensing stays. CTOL calls it a promise rather than a right, and a carve-out that can still be deleted.

Whether the United States replaces the diffusion rule it stopped enforcing. The rescission is not final. That argument is [US federal AI policy](https://www.oguzhan.co/super-intelligence-force-jay-clayton-ai-czar/), separate from this draft.

November 15 ends comments. October 16 turned the filing screen on. Before the final text, the exporter classifies the transfer.

## Sources

- [MOFCOM and MOST, Announcement No. 48 of 2026](https://www.mofcom.gov.cn/zcfb/blgg/gg/2026/art/2026/art_05e2643a8ca04eb9adf9dd0542991fe4.html)
- [MOFCOM spokesperson Q&A, October 16, 2026](https://www.mofcom.gov.cn/xwfb/xwfyrth/art/2026/art_d7661dbf62794345a221404f82a25959.html)
- [CTOL Digital Solutions](https://www.ctol.digital/news/china-draft-technology-export-catalogue-ai-model-weights-chip-design/)
- [Frontier Now](https://frontiernow.dev/en/news/china-ai-export-catalog-draft/)
- [The Decoder (Matthias Bastian)](https://the-decoder.com/china-plans-to-tighten-export-controls-on-open-weight-models-and-23-key-ai-technologies/)
- [Bloomberg via The Straits Times](https://www.straitstimes.com/business/china-plans-ai-export-curbs-to-exert-control-over-key-tech)
- [Reuters via The Straits Times, July 8, 2026](https://www.straitstimes.com/asia/east-asia/beijing-is-looking-at-curbing-overseas-access-to-chinas-top-ai-models-sources-say)
- [GAO decision B-337935](https://www.gao.gov/products/b-337935)
- [Encyclopedia of Economic Statecraft](https://jamesjtennant.com/entries/ai-model-weights-and-frontier-models/)
