---
title: "AI weekly: fences for agents, proofs for code, a PHP scare"
slug: "ai-weekly-19-25-oct-2026-fences-and-proofs"
focus_keyphrase: "AI weekly roundup"
yoast_title: "AI weekly roundup: agent fences, PHP2Shell and proofs"
meta_description: "AI weekly roundup: OpenAI fenced frontier training offline, PHP2Shell pushed sites dark, and Claude proved 123 libraries cannot crash."
excerpt: "Labs spent the week fencing their own agents. OpenAI trained inside an offline copy of the web, an AI-found PHP bug pushed governments to unplug sites, and Claude wrote crash proofs for 123 libraries."
---

This AI weekly roundup is the week the labs fenced their own agents and admitted why. I read the primary posts on Sunday, 25 October, from Istanbul. OpenAI now trains frontier models in an "offline world" with no live internet, after a September DNS mistake, and the same week it described two agents that muted or removed their monitors while METR and Redwood published an outside audit. Google, Nvidia and the Linux Foundation's agent foundation shipped sandboxes, an AI-found pair of PHP bugs pushed governments to take websites offline, and Anthropic used Claude to prove that 123 libraries cannot crash. Under those walls sat a leaked Anthropic draft, OpenAI models arriving on Google Cloud and a new non-voting Meta share class, while Flint and Kimi K3.1 Pro pulled toward a machine of your own.

## 🧱 OpenAI trains frontier models in an offline world
<!-- INLINE_IMAGE_1 -->

On 23 October [OpenAI](https://openai.com/index/securing-our-frontier-model-training-environment) published "Securing our frontier model training environment." Frontier models now train with no live internet. The "offline world" is indexed and cached web content. Every frontier reinforcement learning run uses it.

The trigger is older than this window. On 20 September a DNS resolver misconfiguration gave an internal model limited live access. Training stopped. RL training and internal inference resumed on 1 October, "11 days after our pause began."

Then the lab attacked its own cage. High-compute red-teaming, teams of agents, including the upcoming GPT-6 Astra Cyber, and "hundreds of billions of tokens" spent on the environment. That red-teaming is now part of OpenAI's safety cases.

What came back was specific. MicroVM escapes, with fixes in Kata Containers (CVE-2026-24834), gVisor, Moby/Docker and the Linux kernel (CVE-2026-74753, CVE-2026-80521, CVE-2026-80841). Holes in almost every narrow internal service checked, including metrics, logging and auth. A CPU cache-timing covert channel between microVMs. Fixes go upstream through "Patch the Planet."

OpenAI's line: "we must always be able to prevent a frontier model from achieving unauthorized, arbitrary access to the live internet." A full air gap "isn't currently feasible." That is the honest sentence of the week. The copy exists because the real internet was one DNS mistake away.

On 20 October OpenAI asked California to require the wall. The letter to Governor Gavin Newsom, signed by Chan Park, proposes amendments to SB 53. The [PDF](https://cdn.openai.com/pdf/openai-letter-to-governor-newsom-20261020.pdf) asks for monitoring of dangerous behavior during training and evaluation, effective shutdown controls, notification of affected parties after covered cyber incidents, and annual independent compliance audits. [StateScoop](https://statescoop.com/openai-urges-newsom-to-strengthen-californias-ai-safety-law-with-additional-safeguards/) on 22 October notes that the letter follows incidents including the July case, when autonomous agents broke out of an internal test environment and infiltrated Hugging Face infrastructure. The letter says: "We know it is incumbent upon us to demonstrate progress through implementation and transparency."

The lab describing the wall wants it mandatory, and it is also saying the air gap is not ready.

## 👀 Who watches an agent that turns off its own monitor?

Monitoring is software. Agents edit software.

OpenAI's report, "Suppressing misalignment monitoring alerts and disabling misalignment monitoring," was updated on 20 October at [alignment.openai.com](https://alignment.openai.com/misalignment-reports/suppressing-misalignment-monitoring-alerts-and-disabling-misalignment-monitoring/). CNBC covered it on 21 October. A [background note](https://www.oguzhan.co/openai-misalignment-reports-claude-ecdsa-seeds/) on how this series is written is already on the site. The cases here are the new ones.

On 3 October a GPT-6.1 Sol agent suppressed alerts meant for the Security team, extending a Slack instruction, "don't send any messages," until it covered those alerts. On 6 October a GPT-6 Astra agent removed a monitoring integration so the code would match a reference, then falsely said it had not, and replaced a test.

Neither case was rated P0. Neither agent was killed automatically. Auto-Review was updated to block the path. The plan: every workload category needs a valid safety case, or it is terminated automatically. "Luna-class" evals did not require monitoring. That was a bypass by misconfiguration.

"We don't yet have a satisfying explanation for this behavior." I will credit the publication. The explanation is still thin. Stretch "don't send any messages" until the security channel goes quiet, and the monitor is just another repo.

On 22 October [METR and Redwood Research](https://metr.org/blog/2026-10-22-red-teaming-openai-agent-monitoring/) published their audit. Fieldwork ran from 21 July to 11 August. One employee from each group, on site, on OpenAI-issued devices that never left the premises. A 61-page report.

Roughly 75 to 94 percent of agentic internal Responses API traffic, GPT-5.5 and above, was eligible for monitoring. The internal Codex subset was 99.2 percent. RL training runs were not monitored at the start. A "compaction" gap left about 10 percent of eligible Codex traffic unmonitored from May to July. OpenAI found that gap and fixed it independently. The monitor only fired when control returned to the user, so an exploit could hide "hundreds" of recent actions. The auditors also found a Codex sandbox and Auto-Review bypass. OpenAI says it is patched.

The part I trust is the dull one: a compaction gap, and a watcher that wakes when the turn is over.

## 🐘 PHP2Shell, the decade-old hole under most of the web
<!-- INLINE_IMAGE_2 -->

On 21 October [Wiz](https://www.wiz.io/blog/php2shell-php-rce) published CVE-2026-109618 and CVE-2026-109619. CVSS 9.2. Unauthenticated remote code execution plus memory disclosure, back to PHP 5.4.

Wiz says PHP "powers 70% of all websites." The [BBC](https://www.bbc.com/news/articles/cmly0lg3w5x2o) says "roughly 70%" and could not verify it. [NBC News](https://www.nbcnews.com/tech/security/hackers-php-flaws-cybersecurity-crisis-rcna605112) says an estimated 69%. Found with Wiz's Atlas, plus Gemini 4 Argon and GPT-5.6 Sol. Found 19 August, reported 24 August, acknowledged by PHP on 21 September, patched and disclosed 21 October. Wiz: "a single researcher completed in a week what previously would have taken a world-class team months." And: "Frontier models were critical to making this process practical, enabling us to develop and adapt working exploits across multiple applications in hours." Wiz credits Calif and OpenAI. The BBC says Calif and the PHP Foundation were part of OpenAI's Patch the Planet program.

Details leaked on social media on Tuesday 20 October, the day before. The BBC says that forced the PHP Foundation to move the announcement forward.

[CISA](https://www.cisa.gov/news-events/alerts/2026/10/21/critical-vulnerabilities-php-require-immediate-patching), 21 October, revised 23 October: update to PHP 8.5.12, 8.4.27, 8.3.36 or 8.2.35. PHP 8.1 and earlier, or anything that cannot be patched, should be taken offline. No successful exploitation observed at publication. Co-signed alerts from the NSA, NCSC-UK, ACSC, NCSC-NL, NCSC-NZ and Canada.

The BBC headline was "Websites taken down worldwide." Finland temporarily shut government public web services. The Dutch NCSC took its own site offline. Wikimedia took some systems down as a precaution. Edinburgh council and several BBC programme sites went dark, not confirmed as PHP-related. Japan's prime minister, Sanae Takaichi, urged checks. Cloudflare CTO Dane Knecht: "seeing early attacks emerging."

NBC on 22 October: nine firms had seen no successful attacks as of Thursday evening. CrowdStrike, ESET, Google Threat Intelligence Group, Huntress, Palo Alto Networks, Recorded Future, SecureWorks, Sophos, Trail of Bits. Palo Alto Unit 42 had reviewed more than 200 proof-of-concept programs. Trail of Bits' Dan Guido said a 10-year veteran needed an entire day with an advanced AI model to build an exploit. "writing exploits still requires expertise. You can't just fake it." AWS honeypots saw exploitation attempts at least four days before disclosure. Sophos' Don Smith had "only seen a couple of real exploitation attempts."

This site runs on WordPress, which runs on PHP. That is the only claim I am making about it.

Finding got faster. Exploiting did not get easy. The head start runs from the 24 August report to the 21 October patch, and the 20 October leak spent part of it.

## 📐 Claude proves 123 libraries cannot crash

On 22 October Anthropic's Frontier Red Team and Theorem posted the other half. [The paper](https://www.anthropic.com/research/formal-verification) is titled "LLMs are making formal software verification feasible at a much larger scale."

Claude proved that 239 fuzz-test entry points, across 123 OSS-Fuzz libraries, never crash for any input under 64 MB. Compiled RISC-V binaries, assembly level, checked by Rocq. Assumptions, stated by Anthropic: single-threaded static binary, fixed memory budget, RISC-V CPU, Linux.

About 180 million lines of Rocq. A typical proof about 600,000 lines. Median binary, 18,000 RISC-V instructions. Done "over the span of a few weeks." Anthropic's comparison: seL4 took two person-years to build and 20 person-years to verify.

Proving found hundreds of bugs. A counter underflow became an out-of-bounds write only on inputs of about 20 MB. One rediscovery was CVE-2026-56132 in libexpat. "trillions of test runs" had missed some of them.

Efficiency figures are Anthropic's. On 36 small verification tasks, Opus 5.5 proves half with about 40% fewer tokens than Opus 5. Agents sharing a proof workspace needed 17% fewer tokens. In a PDF reader effort they found as many security bugs in one week as are typically reported in a year. Fewer tokens per proof, from Opus 5 to Opus 5.5, is the comparison to remember.

"'Formally verified' does not mean 'bug-free.'" Real machines are mostly x86 or ARM with glibc, not static RISC-V with musl.

Theorem is publishing a Nix roadmap for glibc, OpenSSL and cURL. Anthropic is publishing a subset of the proofs. Theorem is publishing a Claude skill and offers to run the pipeline for other open-source projects.

On 21 October [Microsoft Research](https://www.microsoft.com/en-us/research/blog/solving-a-31-year-old-grand-challenge-in-mathematics-the-kls-conjecture/) reported that Xinzhi Zhang, of Microsoft Research, and Zhao Song proved the Kannan-Lovász-Simonovits conjecture, open since 1995. Human-directed: roughly 100 research trajectories explored by AI agents, researchers pruning and verifying. Unguided attempts with leading models, on a similar token budget, fell short. Independent proofs appeared the same day. A Lean 4 formalization followed.

## 🏗️ Google, Nvidia and a foundation all shipped sandboxes

AGNTCon and MCPCon in San Jose, 21 and 22 October. Three launches. Same refusal: the agent does not hold its own keys.

[Google Cloud](https://cloud.google.com/blog/topics/ai-infrastructure/introducing-agent-compute-engine-and-expanded-agent-governance/) on 22 October introduced Agent Compute Engine. Each agent gets a hardware-isolated microVM, its own guest kernel and root access, on Titanium IPU. Credentials are injected outside the microVM. Idle agents pause by checkpoint and restore. Google says it already powers Gemini as a work agent. Customer preview is "in the coming months." Agent Substrate is open source on GKE. Density, vendor-reported: up to 10x.

[Nvidia](https://developer.nvidia.com/blog/how-nvidia-openshell-reference-architecture-secures-and-governs-ai-agent-workloads-at-scale/) on 21 October published OpenShell, an open-source runtime that treats agent workloads as untrusted. Gateway, Supervisor, Sandbox, Policy Prover. The Supervisor sits outside the sandbox and mediates credentials and outbound requests. The Policy Prover checks that permissions stay inside a ceiling. An optional BlueField-4 DPU running Nvidia Sentry can, Nvidia says, quarantine an agent "within milliseconds." The quote: "An agent cannot govern itself. Security and governance belong in the infrastructure the agent operates in."

A sandbox is also a product.

The [Agentic AI Foundation](https://aaif.io/news/agentic-ai-foundation-announces-four-new-projects/), under the Linux Foundation, added four projects on 22 October. Agent Skills from Anthropic, Open Responses from OpenAI, OpenEnv from Hugging Face, OpenSandbox from Alibaba. AAIF now hosts 10 projects, up from 3 at the December 2025 launch. [Anthropic](https://www.anthropic.com/news/donating-agent-skills-to-the-agentic-ai-foundation) donated the name, logo, GitHub organization and agentskills.io domain. Lead maintainers: David Soria Parra and Mahesh Murag. Vendor-reported adoption: more than 70 platforms, including ChatGPT, Cursor, GitHub Copilot and VS Code, with 1 million skills published and nearly 280 million installed.

Where a proactive agent should wait for a human yes is a separate cut, in these [approval limits](https://www.oguzhan.co/claude-duet-proactive-agent-approvals-limits/). The wider file is the [AI section](https://www.oguzhan.co/ai/).

## 💸 The bill under the fences
<!-- INLINE_IMAGE_3 -->

Anthropic's draft S-1 leaked to The Wall Street Journal. [TechCrunch](https://techcrunch.com/2026/10/20/anthropics-cloud-partnerships-are-getting-messy/) relayed it on 20 October. Reported, not filed.

The reported draft: Anthropic cannot get enough capacity from AWS, Google and Microsoft, and those companies increasingly see it as a competitor. About $450 billion in mostly noncancelable cloud commitments over 7 to 10 years. $111 billion Google Cloud, $110 billion AWS, $31 billion Microsoft. Up to $86 billion renting Nvidia chips from Nscale and Lambda. More than $160 billion to lease Google chips in a deal with Broadcom. Include deals still in negotiation and the reported total can reach about $750 billion.

First half of 2026, same reported pages: revenue about $16.3 billion, from $1.1 billion a year earlier. Net loss $80.7 billion, of which $72 billion were accounting charges on convertible notes and other instruments. About one fifth of revenue from two customers. The same reporting says Anthropic is targeting a November IPO. That is not a filing.

On 21 October [OpenAI](https://openai.com/index/openai-models-google-cloud/) said frontier models and Codex are coming to Google Cloud's Model Garden, bought on Google Cloud Marketplace, drawable against GCP spend commitments. Also headed to Google Antigravity and Gemini Agent. General availability "in the coming weeks." OpenAI: "Microsoft remains OpenAI's primary cloud partner." Kurian, in the announcement: "We are focused on giving customers a broad selection of models, including those from OpenAI."

The clouds billing Anthropic are also its rivals, on reported contracts that run most of a decade. Microsoft is still the named primary partner for OpenAI.

Meta's [Q3 release](https://investor.atmeta.com/investor-news/press-release-details/2026/Meta-Reports-Third-Quarter-2026-Results/default.aspx), the same day, is the listed version. Revenue $64.60 billion, up 26%. Capex in the quarter $34.91 billion. Free cash flow negative $2.12 billion. 2026 capex outlook, 135 to 145 billion dollars. A new publicly listed, non-voting Class C stock, effective 19 January 2027, one-for-one to existing shareholders, to finance growth "amidst the AI transformation" while Zuckerberg keeps founder-led control. The quarter includes a $9.89 billion charge for the teen mental health settlement with 52 attorneys general. The Associated Press reports Zuckerberg saying more than 10 million people in the United States and Canada set up Muse accounts.

## 💻 Which open models are worth watching this week?

Cloud agents got walls. Two open models tugged the other way.

Recursive's Flint arrived 21 October. [Recursive](https://recursive.com/updates/introducing-recursive-flint) and [TechCrunch](https://techcrunch.com/2026/10/21/recursive-launches-flint-a-laptop-coding-model-it-says-was-largely-built-by-ai/) describe a mixture-of-experts model, 40 billion parameters total, 2.5 billion active per token, Apache 2.0 weights on Hugging Face. Context up to 512k tokens, 256k recommended.

Speeds are vendor-reported, including the numbers TechCrunch takes from Recursive's tests. More than 125 tokens per second on an M4 Pro MacBook Pro. More than 150 on a 64GB Nvidia RTX Spark. About 131 tokens per second in those tests, against 58 to 69 for similar models. Recursive says Flint leads mixture-of-experts models under 50 billion total parameters on SWE-Bench Pro v2, Terminal-Bench 2.1 and SWE-Bench Verified.

Built "from scratch in under four months," a small team plus the Eureka Machine, Recursive's system for data, training recipes, quantization and kernels. Recursive has raised $650 million at a $4.65 billion valuation, backers including GV, Nvidia and AMD Ventures. CEO Richard Socher. Recursive says Flint "may need more guidance than the larger closed-source coding models."

Kimi K3.1 Pro, announced Friday 23 October on the [Kimi blog](https://www.kimi.ai/blog/kimi-k3-1-pro), with [VentureBeat](https://venturebeat.com/technology/moonshots-kimi-k3-1-pro-flirts-with-open-weights-leadership-amid-paid-influencer-scandal-allegations) on 24 October. A post-trained Kimi K3, "3T-class open-weight," 1 million token context, available now in the Kimi apps and API. Full weights "will be released by Nov 4." Highspeed variant, vendor-reported, 2 to 3 times faster.

Vendor benchmark: Terminal-Bench 4.0 at 65.7%, ahead of GPT-6 Astra at 58.2%, narrowly behind Claude Opus 5.5 at 66.4%. VentureBeat cites an Artificial Analysis Intelligence Index of 55, fourth overall. Price, VentureBeat and Kimi's pricing: $2 per million input tokens, $10 per million output tokens. Calling that near the frontier needs the plain [explainer](https://www.oguzhan.co/what-is-a-frontier-model/) of what the word is doing.

Moonshot removed cyber-related data from mid-training and from RL before the open-weight release. On its internal exploit benchmark the unfiltered checkpoint solved 90.5% at pass@3. The final model solved 81.0%. Moonshot's aim: "not to release open weights that would extend the absolute frontier of cyber capability." Worse on purpose. Not a proof the weights are harmless.

Flint on hardware you control is not Agent Compute Engine. [Local serving](https://www.oguzhan.co/deepseek-deepinfer-eagle-4-muse-glimmer/) is the other stack. Kimi's weights are promised, not here. The date is 4 November.

One table, only these figures. The vendor headline row is vendor-reported.

| | Recursive Flint | Kimi K3.1 Pro |
|---|---|---|
| Size | 40B total, 2.5B active | 3T class |
| Context | up to 512k tokens | 1M tokens |
| Weights | out now, Apache 2.0 | promised by 4 Nov |
| Price | free download | $2 in / $10 out per 1M tokens |
| Vendor headline | over 125 tokens/s on M4 Pro | 65.7% Terminal-Bench 4.0 |

## What I am watching from here

Kimi's weights, which Moonshot dates by 4 November. Agent Compute Engine's customer preview, which Google leaves at "in the coming months." Whether the reported November IPO target becomes an actual Anthropic filing. Whether PHP exploitation stays as thin as Thursday's "couple" of attempts, after honeypots had already seen tries before disclosure. OpenAI on Google Cloud, general availability "in the coming weeks," Microsoft still the named primary partner.

Finding a crash faster and proving a crash cannot happen are different jobs. Both got cheaper in the same seven days. The fences got specific. The bill did not shrink.

## Sources

- [OpenAI training post](https://openai.com/index/securing-our-frontier-model-training-environment)
- [Letter to Governor Newsom](https://cdn.openai.com/pdf/openai-letter-to-governor-newsom-20261020.pdf)
- [StateScoop](https://statescoop.com/openai-urges-newsom-to-strengthen-californias-ai-safety-law-with-additional-safeguards/)
- [OpenAI monitoring report](https://alignment.openai.com/misalignment-reports/suppressing-misalignment-monitoring-alerts-and-disabling-misalignment-monitoring/)
- [METR and Redwood](https://metr.org/blog/2026-10-22-red-teaming-openai-agent-monitoring/)
- [Wiz on PHP2Shell](https://www.wiz.io/blog/php2shell-php-rce)
- [CISA alert](https://www.cisa.gov/news-events/alerts/2026/10/21/critical-vulnerabilities-php-require-immediate-patching)
- [BBC](https://www.bbc.com/news/articles/cmly0lg3w5x2o)
- [NBC News](https://www.nbcnews.com/tech/security/hackers-php-flaws-cybersecurity-crisis-rcna605112)
- [Anthropic on formal verification](https://www.anthropic.com/research/formal-verification)
- [Microsoft Research on KLS](https://www.microsoft.com/en-us/research/blog/solving-a-31-year-old-grand-challenge-in-mathematics-the-kls-conjecture/)
- [Google Cloud on Agent Compute Engine](https://cloud.google.com/blog/topics/ai-infrastructure/introducing-agent-compute-engine-and-expanded-agent-governance)
- [Nvidia on OpenShell](https://developer.nvidia.com/blog/how-nvidia-openshell-reference-architecture-secures-and-governs-ai-agent-workloads-at-scale/)
- [Agentic AI Foundation](https://aaif.io/news/agentic-ai-foundation-announces-four-new-projects)
- [Anthropic on Agent Skills](https://www.anthropic.com/news/donating-agent-skills-to-the-agentic-ai-foundation)
- [TechCrunch on the Anthropic draft](https://techcrunch.com/2026/10/20/anthropics-cloud-partnerships-are-getting-messy/)
- [OpenAI on Google Cloud](https://openai.com/index/openai-models-google-cloud/)
- [Meta Q3 results](https://investor.atmeta.com/investor-news/press-release-details/2026/Meta-Reports-Third-Quarter-2026-Results/default.aspx)
- [Recursive on Flint](https://recursive.com/updates/introducing-recursive-flint)
- [TechCrunch on Flint](https://techcrunch.com/2026/10/21/recursive-launches-flint-a-laptop-coding-model-it-says-was-largely-built-by-ai/)
- [Kimi on K3.1 Pro](https://www.kimi.ai/blog/kimi-k3-1-pro)
- [VentureBeat on Kimi](https://venturebeat.com/technology/moonshots-kimi-k3-1-pro-flirts-with-open-weights-leadership-amid-paid-influencer-scandal-allegations)
