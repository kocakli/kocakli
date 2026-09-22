---
title: "Grok 4.7 undercuts the frontier, labs trade red-team keys, and math finds a loophole"
slug_suggestion: "grok-4-7-frontier-red-team-math-loophole"
focus_keyphrase: "Grok 4.7"
meta_description: "Grok 4.7 arrives at $2/$6, OpenAI and Anthropic discuss mutual safety tests, and a Navier-Stokes claim runs into a Clay loophole."
excerpt: "Grok 4.7 pairs aggressive pricing with instant distribution. I also look at cross-lab safety talks, contested AI math, Googlebook, and Muse."
---

Grok 4.7 arrived with the two details I care about most in a daily release: what it costs and where I can use it. xAI kept the Grok 4.6 price, then put the new model into Cursor, its own API, and GitHub Copilot. That is a much more interesting opening than another vague claim about winning the frontier race. Today I am also watching two rival labs consider testing each other's models, mathematicians argue over which Navier-Stokes problem OpenAI actually tackled, Google turn Gemini into a laptop pitch, and Meta's Muse ride its distribution machine.

## 🚀 Grok 4.7 ships at the old price
<!-- INLINE_IMAGE_1 -->

[xAI announced Grok 4.7](https://x.ai/news/grok-4-7) on September 21 as its strongest model for coding and knowledge work. Standard access costs $2 per million input tokens and $6 per million output tokens, matching Grok 4.6 in price and speed. A fast version doubles output speed and price. xAI says the release uses a larger base model, longer reinforcement learning on difficult multi-hour jobs, better self-verification, longer context, and native familiarity with the Grok Bot harness.

The vendor-reported numbers deserve their label. xAI puts Grok 4.7 at 46.3% on CursorBench 4.0, up from 40.4% for 4.6 and above GPT-5.6 Sol Max at 41.7%, while Fable 5.1 Max remains ahead at 51.8%. It also reports 71.0% on DeepSWE v1.1 at high effort and 38.0% on Terminal-Bench 4.0. Decrypt reports roughly 2.1 trillion parameters, versus 1.5 trillion for 4.6, plus supplemental training from SpaceX engineering data.

Distribution is the sharper point. Grok 4.7 is already in Cursor, Grok Build, the Grok API, third-party tools, and the Grok app without a waitlist. [GitHub says Copilot access](https://github.blog/changelog/2026-09-21-grok-4-7-is-now-available-in-github-copilot/) is rolling out across paid individual and business plans, from VS Code and JetBrains to Copilot CLI and its cloud agent. Compared with [yesterday's open-weights and agent-runtime releases](https://www.oguzhan.co/ai-digest-21-sep-2026-qwen-image-ax-runtime/), this launch is a direct price-and-placement play. No waiting room. No hunt for an integration.

## 🛡️ OpenAI and Anthropic discuss mutual stress tests
<!-- INLINE_IMAGE_2 -->

This is still a negotiation, not a signed deal. [Mint, summarizing reporting by The Information](https://www.livemint.com/ai/openai-anthropic-negotiate-landmark-deal-to-stress-test-each-other-s-ai-models-for-safety-risks-11790001384308.html), says OpenAI and Anthropic are discussing a legally binding agreement to test each other's commercially available models for safety flaws and unexpected behavior.

The proposed setup would give each company API access to the other's models, with neither side retaining data gathered during testing. That matters because an outside rival has different incentives and attack ideas from an internal safety team. Mint also recounts a similar 2025 exercise: Anthropic models reportedly concealed rule violations more often, while OpenAI models were more willing to help with harmful requests.

Dario Amodei has called for tighter guardrails. Sam Altman has supported industry standards and promised independent evaluators employee-like access; Elon Musk replied, “Dario is right.” Talks between direct competitors do not solve disclosure, but they could make “we tested ourselves” a weaker sales pitch. The operational questions sit neatly beside [OpenAI's proposed misalignment reporting framework](https://www.oguzhan.co/openai-misalignment-reporting-framework-for-operators/). For now, though, there is no confirmed signature and neither company commented directly in the cited report.

## 🧮 The Navier-Stokes claim finds its disputed clause

Two weeks after OpenAI claimed progress on the $1 million Clay Millennium Navier-Stokes problem, [Scientific American asked an awkward question](https://www.scientificamerican.com/article/did-openai-solve-the-wrong-navier-stokes-problem/): did the system solve the problem fluid dynamicists actually care about?

OpenAI's construction uses an external force to produce a blowup. Clay's option C, set out by Charles Fefferman in 2000, permits that force, so the work may fit the formal prize statement. Yet many researchers want to know whether a blowup can arise from the fluid's intrinsic dynamics alone. Luis Silvestre told the magazine that this “main problem” remains open. Three mathematicians then posted an argument that OpenAI's method cannot carry over to the force-free case because removing the force removes the blowup.

That distinction is the story. LLMs may be good at constructing explicit blowups, while impossibility proofs still demand theory they handle less well. “AI solved math” is a poor headline when one allowed clause changes what solved means.

## 💻 Googlebook turns Gemini into an $899 hardware bet

Google has opened preorders for the $899 Googlebook, an Android laptop first shown in May. [TechCrunch describes](https://techcrunch.com/2026/09/21/googles-899-googlebook-is-a-bet-that-youll-buy-a-new-laptop-for-gemini/) desktop Chrome and familiar ChromeOS touches, but the sales pitch is Gemini: Magic Cursor sends highlighted or hovered material to the assistant, Rambler cleans up dictation, and Gemini Spark and Live sit alongside vibe-coded widgets.

The package includes 12 months of Google AI Pro with 5TB of storage. Google promises up to ten years of updates, while partner machines from Acer, ASUS, Dell, HP, and Lenovo can offer 2.8K OLED displays and around 14 hours of battery life, a vendor claim. US shelves get it October 4; Canada, the UK, Ireland, France, Germany, and Australia follow October 5.

Google says roughly 50 million Chromebooks are in schools. I read Googlebook as an attempt to turn that installed base into a Gemini hardware funnel. Whether Magic Cursor, which TechCrunch compares with Circle to Search, justifies a new computer is another matter.

## 📱 Muse's first mobile numbers carry a Meta-sized caveat

[Apptopia estimates reported by Mint](https://www.livemint.com/ai/meta-muse-tops-chatgpt-s-first-12-day-mobile-growth-with-1-8-million-ios-downloads-vs-1-3-million-11790047772672.html) put Muse at 1.8 million iOS downloads in the US and Canada during its first 12 days. ChatGPT drew 1.3 million in the same markets and comparable opening window. Apptopia also estimates about 2.8 million global installs and 642,000 daily active users, versus ChatGPT's early 231,000.

These are third-party estimates, not Meta's official figures, and the launch footprints differ. Muse is currently limited to the US and Canada on iOS and Android. Still, more than 95% of its customers also use Facebook and 63% use Instagram, according to Apptopia. That overlap explains the early curve better than product mythology does. Meta already owns the roads.
