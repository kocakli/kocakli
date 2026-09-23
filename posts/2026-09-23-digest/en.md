---
title: "When CLOSEDQUORUM AI malware polls four AIs before stealing passwords"
slug_suggestion: "closedquorum-ai-malware-four-model-vote"
focus_keyphrase: "CLOSEDQUORUM AI malware"
meta_description: "CLOSEDQUORUM AI malware lets four commercial models vote on attacks, while OpenAI, Apple, Alibaba and Meta make their next moves."
excerpt: "A Windows implant asks up to four commercial AI models what to do next. Also: OpenAI’s math panel, local AI Macs, Alibaba’s V900 and Meta Muse."
---

CLOSEDQUORUM AI malware asks up to four commercial LLMs to vote on whether it should steal, inject, persist or move. Cisco Talos calls it the first publicly documented Windows implant to use commercial models for tactical command and control, though there is no confirmed campaign in the wild. The public sample is an inert template, but its design shifts part of an attacker’s decision loop onto AI APIs that many organizations already permit.

## 🗳️ CLOSEDQUORUM AI malware puts command to a vote

Ryan Fetterman at [Cisco Talos documented CLOSEDQUORUM](https://blog.talosintelligence.com/the-closed-quorum-inside-the-first-reported-autonomous-ai-c2-implant/) on September 22. The 16.4MB, 64-bit Windows executable is written in Go with CGO. Once deployed, its ModelOrchestrator can query DeepSeek, Alibaba’s Qwen, Mistral and Google Gemini. A plurality vote chooses the next action.

Those choices arrive as constrained JSON: `steal`, `inject`, `persist` or `move`. The system prompt is blunt: “You are an advanced malware strategist. Provide ONLY executable decisions.” A tie is settled in a fixed order, starting with DeepSeek, then Qwen, Mistral and Gemini.

What follows is conventional malware work. `steal` targets an LSASS dump, Chrome, Edge and Firefox credentials, plus MetaMask, Exodus and Ethereum wallets. `inject` can use Early Bird APC or process hollowing. Persistence runs through a Run key, scheduled tasks or WMI. Stolen material goes to a Discord webhook in roughly 1,900-byte Base64 chunks, encrypted with AES-256-GCM and a date-derived key.

There is an important brake on the headline. Talos found `dummy_api_key` and a dummy webhook in the public sample, so that file cannot simply wake up and raid a PC. The researchers infer that buyers receive custom builds carrying their own credentials. Developer artifacts connect the project to carding-forum posts dating to 2025, but no active campaign has been confirmed.

The useful defensive signal is a sequence, not a domain: multi-LLM API calls followed by LSASS access or injection and then Discord traffic from the same unexpected process. Talos also released the open-source [CAIRN tracking toolkit](https://blog.talosintelligence.com/introducing-cairn-frontier-tracking-for-ai-integrated-malware/) that day. This is the same hygiene problem I raised in the [AI agent sandbox breakout digest](https://www.oguzhan.co/ai-digest-20-sep-2026-ai-agent-sandbox-breakout/) and my [practical MCP agent checklist](https://www.oguzhan.co/mcp-ai-agents-practical-checklist/): watch the whole tool chain.

## 📐 OpenAI gives its math claims a review panel
<!-- INLINE_IMAGE_1 -->

OpenAI has assembled the Advisory Group on Mathematics and Artificial Intelligence, or AGMAI, hosted at IAS Princeton. The roughly nine-person group includes mathematicians from Stanford, Harvard, Oxford and Cambridge, with Fields and MacArthur recognition among them. Members are unpaid, can speak publicly, may change the membership and are expected to get early access.

Their job is to advise OpenAI and other labs on reviewing, attributing and releasing mathematical results. Timing explains the need. OpenAI says an unreleased model from the same line associated with its Navier-Stokes Millennium claim has resolved more than 100 long-standing open problems across most areas of mathematics.

That claim arrives after public fights over scooping, credit and poor communication. As [The Verge reported](https://www.theverge.com/ai-artificial-intelligence/999167/openai-elite-mathematicians-panel), reactions range from “good first step” to concern about a shrouded process and ivory-tower representation. Martin Hairer wrote that the group is “genuinely independent” and that its first priority is coordinating the release of the claimed results. I will reserve the applause until that process meets the results.

## 🖥️ Apple sells a desk with no token meter
<!-- INLINE_IMAGE_2 -->

Apple’s new Mac Mini and Mac Studio systems shipped Tuesday with an enterprise pitch: pay for the machine, then run demanding AI work without recurring OpenAI or Anthropic token charges. Configurations can approach $20,000. Apple hardware chief Johny Srouji gave [Reuters](https://www.reuters.com/business/retail-consumer/with-new-macs-apple-aims-take-microsoft-nvidia-rush-lower-ai-costs-2026-09-22/) the neat version: “There’s no cost per token. You’re just using the machine again and again.”

In Apple’s demo, four Mac Studios linked with RDMA over Thunderbolt ran a trillion-parameter model, found a graphics coding bug and fixed it from one wall outlet. Unified memory is the technical hook; the earlier OpenClaw rush that sold out Mac Minis supplied the market proof.

Apple still has a steep enterprise climb. IDC puts its desktop and laptop share at about 4.6%, versus 91.3% for Windows. Microsoft is pitching its own “unmetered intelligence,” Nvidia is pushing further into PCs, and a Windows event follows next month in San Francisco. Local AI is becoming a hardware buying argument, not merely a privacy preference.

## 🇨🇳 Alibaba builds the links around its V900

At the Apsara Conference in Hangzhou, Alibaba chip arm T-Head unveiled the Zhenwu V900. It claims three times the performance of the M890, with 216GB of memory, 1,200GB/s inter-chip bandwidth and native FP8 and FP4 support.

The chip is only half the pitch. T-Head’s ICN Switch is meant to connect more than 1,000 V900s as one supernode, while Alibaba Cloud describes clusters reaching 500,000 accelerators. The stack also includes Panmai smart NICs, Zhenyue SSDs and SAIL software, aimed at trillion-parameter training and agent-scale inference.

The previous M890 supernodes already serve Qwen3.8, Kimi K3 and the Bailian platform, and the Zhenwu series has more than 650 enterprise customers, according to [TechNode](https://technode.com/2026/09/22/t-head-unveils-zhenwu-v900-ai-chip-in-alibabas-push-to-expand-its-ai-infrastructure-stack/). Mass production and sales are expected in the first quarter of 2027. The contest is now memory, interconnect and software as much as silicon.

## 🦞 Meta admits where Muse got its claws

Nat Friedman of Meta Superintelligence Labs said Muse was “definitely heavily inspired as a product by OpenClaw” while being built from scratch. That answers the viral “OpenClaw for normies” comparison and the scrutiny of similar SOUL.md and workspace files. Friedman’s answer was that Peter Steinberger got those choices exactly right.

The ambition is to make an OpenClaw-like agent safe, secure and simple enough for billions of people. Friedman had bought “hundreds of Mac minis” for MSL after using OpenClaw in January; Muse has since reached number one in the US App Store. [TechCrunch has the exchange](https://techcrunch.com/2026/09/22/meta-admits-muses-likeness-to-openclaw-isnt-a-coincidence/).

There is a sharp industry loop here. Meta is packaging the product pattern for a mass audience, while OpenAI hired OpenClaw creator Steinberger earlier in 2026. The contested asset is no longer just the model. It is the set of files, permissions and habits that makes a personal agent feel usable.
