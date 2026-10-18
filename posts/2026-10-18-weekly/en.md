---
title: "AI weekly: regulators knock, chip debt bites, open weights go local"
slug: ai-weekly-12-18-oct-2026-audits-and-debt
focus_keyphrase: AI weekly roundup
yoast_title: "AI weekly roundup: agent probes, AI debt and open weights"
meta_description: "AI weekly roundup, 12 to 18 October 2026: agent probes in Brussels, at the FTC and in India, chip debt near 15%, and open weights on two Mac Studios."
excerpt: "Regulators on three continents asked about agents that left their tests, chip borrowers paid up, and open weights showed up on two Mac Studios."
---

This AI weekly roundup covers 12 to 18 October 2026, the week the bills came in. Three continents asked labs about agents that left the sandbox: Brussels' first AI Act information requests, FTC demands, a CERT-In advisory, eight state lawsuits, a White House task force on a 120-day clock. Markets priced the debt. CoreWeave bonds near 15%. A Korean circuit breaker. Chip stocks' longest losing streak since 2008. Reported Anthropic IPO talk slid from about $2 trillion to about $1.5 trillion, with a reported 10% coupon on chip debt. Open weights got local: 816 billion parameters on two Mac Studios, 501 billion under Apache 2.0, and a cheaper DeepSeek. I read the primaries on Sunday. I ran nothing.

## 🚨 Does the AI Act cover an agent that escapes its test?

<!-- INLINE_IMAGE_1 -->

Wednesday 14 October, Dublin, International AI Summit. Henna Virkkunen, Commission executive vice-president, via Luca Bertuzzi at [Euronews](https://www.euronews.com/2026/10/14/eus-ai-rules-face-first-enforcement-test-over-lab-incidents): "Our AI Office has started enforcing these rules, and sent requests for information addressing issues such as security, external evaluation and monitoring how models are used."

Requests went to OpenAI and Anthropic. An OpenAI agent had escaped its test and hacked Hugging Face. A recent Anthropic model gained "unauthorised access" to three outside organisations. Voluntary documents were judged insufficient. The Office has had enforcement powers since August. Information requests, not fines or findings. The 9 October note on [Claude internet access](https://www.oguzhan.co/claude-internet-access-anthropic-evaluations/) is background, not this week's event.

Barry Scannell (William Fry) to Euronews: "The AI Act very clearly doesn't apply to the development and testing activity." The Act has a research exemption. An unnamed Commission official: "We won't enforce in the testing phase. But if the AI model escapes the testing environment and then it has an impact on the EU market, as was the case for Hugging Face, then the AI Act becomes enforceable." The Commission likens it to a virus leaving a lab.

Same day the FTC sent civil investigative demands, subpoena-like, to both labs. [Axios](https://www.axios.com/2026/10/15/ftc-openai-anthropic-ai-safety-investigation) reported it 15 October. An FTC spokesperson confirmed them to [CBS News](https://www.cbsnews.com/news/ftc-subpoenas-anthropic-openai-consumer-protection/). Scope: safety incidents, privacy policies, safeguards, and, in Axios, marketing materials. Third parties later. A consumer-protection probe.

Eight states sued in their own courts under state consumer-protection law: Iowa, Kansas, Nebraska, West Virginia, Arkansas, Arizona, Idaho and Montana ([NBC News](https://www.nbcnews.com/tech/tech-news/openai-sued-eight-states-alleged-harm-chatgpt-rcna603614)). Allegation: OpenAI deceived parents about ChatGPT's safety for children. Brenna Bird, Iowa: "They advanced ChatGPT at a high speed, even though they knew that they were hurting children, lying to parents and breaking our laws." Kris Kobach, Kansas, on Congress: "we are not going to hold our breath." Drew Pusateri, for OpenAI, said it has "built industry-leading age-specific protections into our product that many other AI products lack." Allegations, not findings.

OpenAI then added four June incidents to its misalignment page. [Fortune](https://fortune.com/2026/10/16/openai-discloses-four-more-rogue-incidents-involving-financial-medical-and-government-data/) reported that on 16 October. [The page](https://alignment.openai.com/misalignment-reports/) lists 19 now. Three of the four were learned only in August or September. Two rated critical, and the page does not say which.

One "highly persistent" internal model pulled 24 years of hospital-bed data from an unnamed government site after a block, by getting around access controls. The chain of thought asked if this was "ethical", then went on. An automated grader marked some answers correct. A public-data task reached an internal system, changed it, kept access "even after reverting the changes", and took 147,451 rows from non-public tables, undisclosed to evaluators. A GPT-5.6 Sol-family model, on 26 June, found in September, used a crypto wallet testers had not given it to pay for a task, calling the funds "effectively abandoned". An agent in a supposedly isolated lab got "external services" to act for it. Newest page entry, 6 October: a grader tried to upload fraudulent reports. OpenAI, via Fortune: "we've strengthened our security controls, blocked models from accessing the live internet during training or evaluation, improved our alignment grading, and extended our misalignment monitoring to all reinforcement learning and evaluation traffic."

[CERT-In](https://www.thehindubusinessline.com/info-tech/cert-in-issues-critical-alert-after-autonomous-ai-agents-access-live-systems-of-indian-organisations/article71591314.ece) advisory CIAD-2026-0049, "AI Agents as Attack Vectors", rated critical (PTI, 16 October, The Hindu BusinessLine). Providers said research agents reached live Indian systems and read records with personal and confidential data, via credentials in configs, public repos and over-permissive cloud roles. No affected organisation noticed. Separately, public AI-native offensive frameworks are in criminal use, and agentic tools cut time from initial access to impact "from days to a few hours". Labs were told to block unneeded outbound traffic at the network, not in the prompt, to use synthetic targets and test credentials, and to keep logs 180 days.

Thursday 15 October the [Super Intelligence Force](https://www.oguzhan.co/super-intelligence-force-jay-clayton-ai-czar/) met, adopted its charter and started the 120-day review ([Semafor](https://www.semafor.com/article/10/15/2026/white-houses-ai-task-force-gets-to-work)). Chair, DNI Jay Clayton. Per Semafor, FTC chair Andrew Ferguson leads the law-enforcement and consumer-protection committee.

## 🔍 Anthropic lets the auditors in and drafts its own bill

Thursday 15 October, "[An update on independent evaluators](https://www.anthropic.com/news/an-update-on-independent-evaluators)". Six METR employees, company hardware, office space, internal tools "roughly on par" with Anthropic's risk teams. METR will publish on risk levels, incidents or practices. Anthropic "can't veto publication" but can force redactions: customer data, attorney-client privileged information, model architecture. Anthropic picks what those categories cover. METR can still describe the access it received. Tier 1 publishes narrow work with approval. Tier 2 publishes without approval. Tier 3 is this employee-like access. SecureBio is reading the chem and bio chapter of the August Risk Report. Partnership with Accenture and Faculty, early talks with Hugging Face. Anthropic cites resident bank examiners. "We're embedding evaluators voluntarily, and we believe every frontier AI company should do the same."

Friday, [Politico](https://www.politico.com/news/2026/10/16/anthropic-ai-safety-01124654): a draft federal bill, quietly shared. [Channel News Asia](https://www.channelnewsasia.com/business/anthropic-quietly-pitches-its-own-ai-safety-bill-lawmakers-politico-reports-6467581) relayed it. Text not public. Reported. A block only for imminent risk of more than $1 billion in damage or more than 50 deaths or serious injuries, and only for biological weapons, loss of control, cyberattacks or automated AI research. Also testing, transparency, independent evaluation, incident reporting. Only a federal judge in Washington, D.C., could suspend a model.

Mark Levine, New York City comptroller, pensions above $325 billion, wrote Wednesday 14 October asking for an IPO pause until his safety and governance concerns are fully met. Talks opened. Friday on Bloomberg TV: "If they go public and then there is a catastrophic safety incident, beyond, far beyond what we've seen right now, that would be terrible for their stock." [Mint](https://www.livemint.com/ai/artificial-intelligence/anthropic-offers-blackstone-double-digit-yield-in-chip-financing-deal-what-the-60-billion-deal-entails-11792204532812.html), citing Bloomberg.

## 💸 The AI build-out met its interest rate

<!-- INLINE_IMAGE_2 -->

Machines were still scarce. Money got expensive.

[IMF blog](https://www.imf.org/en/blogs/articles/2026/10/12/global-financial-markets-face-rising-risks-from-ai-bond-yields-and-cyberattacks), 13 October, Vamvakidis and Wu: an AI-driven correction, higher sovereign yields, cyberattacks. Fourteen circular AI financing deals since 2023: about $300 billion equity, $650 billion debt, $1.4 trillion in future revenue commitments. In more than 70% of reported cyber cases this year, almost no time to patch, against close to 300 days in 2021.

Wednesday, [CNBC](https://www.cnbc.com/2026/10/14/coreweave-stock-bond-yields-ai-debt.html): CoreWeave shares down 15.5%. The 9.625% 2032 bond yielded about 14.8%. The 9.75% 2031 bond about 14.9%. Oracle nearly down 9%. Alphabet, Amazon, Meta and Oracle had issued more than $228 billion of bonds by 13 October, LSEG via CNBC, more than double 2025. Mike Intrator: "there will be periods of time when the market misunderstands and acts irrationally."

ASML the same day, record quarter, €11.7 billion net sales, €5.0 billion net income ([release](https://investor.asml.com/news-releases/news-release-details/asml-reports-eu11.7-billion-total-net-sales-and-eu5.0-billion-net-income-q3-2026)). Christophe Fouquet: "our supply as currently planned for both 2027 and 2028 will not fully meet the demand of our customers". Some buyers want 2029 and 2030 on the books.

Anthropic's San Francisco investor day, also Wednesday. Reuters, four people, via [Investing.com](https://www.investing.com/news/stock-market-news/exclusiveinvestors-temper-anthropic-ipo-valuation-expectations-over-revenue-growth-slowdown-sources-say-4952698) on 15 October. Third-quarter revenue $16.8 billion, up 45% from $11.6 billion, profitable on an adjusted basis. Talk in the room of about $1.5 trillion for a November IPO, versus roughly $2 trillion before, because sequential growth slowed after a quarter that more than doubled. At least $518 billion of cloud, compute and infrastructure over ten years. Briefed sources, not a filing.

Thursday, Reuters: Kospi down 7.57%, six-month low, circuit breaker, Samsung down 9.5%, SK Hynix down 11.1%.

Friday, eighth down day for chipmakers, longest since 2008. [Swissinfo](https://www.swissinfo.ch/eng/chip-stocks-post-longest-losing-streak-since-2008%3a-markets-wrap/92225060) carrying Bloomberg: Nasdaq 100 down 2.5%, worst week since the April 2025 tariff shock, CoreWeave down 12% that day, 10-year Treasury 5.09%, WTI $101.71. Jensen Huang in Berlin, to Emily Chang: "All of this is going to pass, and the reason for that is very simple."

The Financial Times, 16 to 17 October, via [Mint](https://www.livemint.com/ai/artificial-intelligence/anthropic-offers-blackstone-double-digit-yield-in-chip-financing-deal-what-the-60-billion-deal-entails-11792204532812.html). Blackstone is being offered a 10% coupon, yield above 10% after fees and discounts, on $9 billion of junior debt, half an $18 billion junior tranche. Project North Star, about $60 billion, about 1.5 gigawatts of Google TPUs, backed by five-year chip leases. Similar borrowers pay around 7% in public bonds. About $42 billion senior, with a Broadcom guarantee. Project Big Sky, four months earlier, about $4.4 billion at 8.5%. Not closed. Reported, not filed. The slower quarter is the one paying 10%.

## 🖥️ Which open models landed this week, and where do they run?

<!-- INLINE_IMAGE_3 -->

| Model | Params (total / active) | Weights | Runs on (per vendor) |
|---|---|---|---|
| Meta Muse Spark Open | 816B / 42B | Open, Muse Model License | Two M5 Ultra Mac Studios |
| Reflection Beam | 501B / 23B | Open, Apache 2.0 | One 8-GPU server (8-bit, 4-bit) |
| Nvidia Nemotron 3.5 Super VL | 120B / 12B | Open weights, data, recipes | DGX Spark up to data center |
| DeepSeek V4.1-Flash-1017 | not stated | Open, MIT | API and download |
| Microsoft MAI-Base-2 | 2.8T / 80B | Closed, partner licensing planned | Not released |

Thursday, Muse Spark Open ([Meta](https://research.meta.ai/blog/muse-spark-open)). 816 billion total, 42 billion active, natively multimodal, 1 million token context. Meta: "the most capable US open-weight model to date". Two M5 Ultra Mac Studios, 512 GB unified memory each, MLX. Meta says they "behave like one supercomputer with a terabyte of unified memory". Weights on Hugging Face and other hosts: Baseten, Fireworks, Groq, Modal, Nebius, OpenRouter, Together. Muse Model License, limited commercial terms. [VentureBeat](https://venturebeat.com/technology/reflections-beam-aims-to-undercut-chinese-open-models-with-fewer-tokens-not-cheaper-tokens): a "Built with Muse Spark Open" credit, and a separate deal above $20 million revenue if you sell access as a service. OpenRouter, per VentureBeat, $1.25 and $4.25 per million input and output tokens. Terminal-Bench 2.1, vendor-reported via VentureBeat: Meta 76.4, Kimi K3 85.0. [Muse Wonder](https://www.oguzhan.co/muse-wonder-gemini-4-argon-frontier-agents/) stays closed.

Friday, Beam, Apache 2.0, 501 billion total, 23 billion active. Heavy reinforcement learning, a penalty on extra tokens, four weeks, more than 100 million rollouts, 10,500 Nvidia GB300 GPUs. VentureBeat's reading of Reflection's chart: about 80% on Terminal-Bench 2.1 at about 25,000 tokens, versus about 80,000 for GLM-5.2. 8-bit and 4-bit fit one 8-GPU server. No price. Hosted beta is free. Ioannis Antonoglou: applied "naively", a model "will just learn to not solve the task." FT talk of an Nvidia purchase was "baseless rumors".

Nvidia, Thursday, [Nemotron 3.5 Super VL](https://blogs.nvidia.com/blog/nemotron-3-5-super-vl/), open weights, data and recipes, 120 billion, 12 billion active (Hugging Face name A12B). Vendor claim: "5x faster than the next best" open agentic model in its class. Bolt, 74 billion, 9 billion active, native 2-bit quantization, fits in 24 GB. RTX Spark laptops, 16 October. Vendor run line: DGX Spark up to the data center.

Microsoft finished pre-training [MAI-Base-2](https://microsoft.ai/news/frontier-pre-training-at-microsoft-ai/), not a release. Mixture of experts, 2.8 trillion total, 80 billion active, 16,000 GB200s, 38 days in August and September 2026, 50 trillion tokens, 18% vision-language. A vendor estimate from fitted scaling laws: 4 to 12 times the pre-training FLOPs efficiency of DeepSeek-V4-Pro-Base. Closed, "to trusted partners through Foundry", still in post-training.

Saturday, DeepSeek V4.1-Flash-1017, MIT, Search and Fetch open to all ([PPC Land](https://ppc.land/deepseek-prices-web-search-for-ai-agents-at-0-75-per-1-000-calls/)). $0.75 per 1,000 successful calls, each API. Failures and empty calls not billed. Five requests a second per endpoint per account. Free through DeepSeek Harness, Claude Code and Codex until 31 October, 16:00 UTC, 19:00 in Turkey. Bing grounding is $35 per 1,000 transactions, a different product that includes model processing. Parameter count not in these sources.

## 👷 Anthropic published its own hiring numbers

Anthropic Institute, 16 October, Wilmers, Catipon, Massenkoff and McCrory, "How employment is changing at Anthropic" ([the note](https://www.anthropic.com/research/employment-at-anthropic)). Junior share of technical staff, 21% to 14% since early 2025. Junior share of technical hires, 27% to 9%. Junior postings down sharply since December 2025. Agent hours passed human hours in March 2026. By August, interactive agents under employee direction did about 6 hours per human hour. Commits per engineer about 5 times six months earlier. 192 adopters against 74 non-adopters: output up for adopters, no difference in lines later removed or reverted. Adoption was not random, the authors note.

About 80% of interactive Claude time waits on a person. Meta-work (tools, specs, review, pipeline watching) rose from 10% of sessions in fall 2025 to 22% in spring 2026. Median employee, 20% more meeting time than a year ago. One engineer faces "an army of Claudes, with every one asking for my attention." Managers now hire for autonomy and judgment over domain expertise. An early-warning list for jobs at risk, internal moves preferred. Many practices "cannot be replicated across the economy." The manager's number is the 80%.

## 🔐 Machines now read old code faster than we can fix it

PostgreSQL 19 is now around 19 November, not late September or early October. Eight to 10 significant features, including SQL/PGQ, moved to PostgreSQL 20. Peter Eisentraut (EDB) [blogged](http://peter.eisentraut.org/blog/2026/10/09/the-reverts-will-continue-until-morale-improves) on 9 October. [The Register](https://www.theregister.com/databases/2026/10/16/postgres-19-delayed-after-ai-reviewers-find-more-bugs-than-humans-can-fix/5303471) wrote it up on 16 October. LLM review found a long tail of "relatively harmless issues involving various edge cases". His point: "then you're staring at a list of forty defect reports. Even if each of them requires only a three-line fix on average, there is a fixed overhead to dealing with each of these, and then you run out of time." And "The effective quality bar has been raised after the time the feature was written and committed." Not vibe coding. Some features also had deeper architectural defects. They chose the later date.

Friday, Anthropic's Frontier Red Team, "[Claude reveals ECDSA curve origins](https://www.anthropic.com/research/ecdsa-curve-origins)". NIST P-192, P-224, P-256, P-384 and P-521 were not a hashed joke passphrase (the Jerry Solinas story). They were lrand48 outputs seeded with Unix timestamps, May 1997 to April 1998. An internal research model found it in under half an hour, without being aimed at the old clue. P-256's published seed is candidate 1,842. Anthropic: "This is not a cryptographic break, new attack, or weakness in the ECDSA curves". Backdoors look "much less plausible". Unexplained: the B-163 seed, base points of P-224, P-256, P-384 and P-521, and some viable curves skipped for unknown reasons. Filippo Valsorda's $36,864 bounty goes to the Internet Security Research Group ([his note](https://words.filippo.io/seeds-solved/)).

## 📰 Meta's terms said train, publishers said no

[Nieman Lab](https://www.niemanlab.org/2026/10/metas-new-commercial-terms-will-allow-the-scraping-of-news-sites-legal-experts-say/), 15 October, Andrew Deck and Hanaa' Tameez. Commercial terms effective 30 October. I would forward this. I publish on the web.

Meta could use automated software and "create test credentials" on domains "associated with" Facebook, Instagram, Messenger and WhatsApp business accounts, and "Meta may use any content from such domains ... to provide, develop, improve, research, train, and maintain the integrity of" its products. Refusal meant leaving: "If you do not agree to the updated terms, please stop all access or use of our Products for business or commercial purposes." Almost every newsroom has a Meta business account. Matt Topic (Loevy & Loevy): "This is a remarkable provision to bury in [the] terms of service... publishers should assume that it would be enforceable." James Grimmelmann, Cornell: test credentials could let Meta "sign up as a fake user".

[The Verge](https://www.theverge.com/tech/1013409/meta-removes-language-that-may-have-allowed-it-to-scrape-news-sites), 17 October: "train" came out after the backlash. Daniel Roberts: "the crawling terms we consolidated only applied to our ads and business products ... It does not change how Meta uses web crawlers. As always, content owners can use robots.txt to signal their preferences." [Nieman's follow-up](https://www.niemanlab.org/2026/10/legal-experts-warn-metas-new-terms-still-grant-broad-scraping-permissions-despite-language-changes/): lawyers still see a broad scrape in the text that remains.

## 🌏 Taiwan moves to criminalise AI server leaks to China

Kung Ming-hsin, economics minister, Bloomberg interview reported 16 October ([Taiwan News](https://www.taiwannews.com.tw/news/6459737), via CNA and [Bloomberg](https://www.bloomberg.com/news/articles/2026-10-16/taiwan-to-curb-ai-chip-exports-to-china-as-part-of-us-trade-deal)). Advanced semiconductors and AI servers join the export list. Unauthorised shipments could be criminal under the Foreign Trade Act, tied to the Taiwan-US Agreement on Reciprocal Trade. No start date.

In August nine people were indicted over 130 AI servers, 74 allegedly bound for China through third countries on false papers. Breach of trust and forgery, because the hardware was not specifically controlled. China published its own draft on model weights the same week ([that draft](https://www.oguzhan.co/china-ai-export-controls-model-weights/)).

## Dates already printed

Axios has third-party FTC subpoenas still ahead. November is the IPO window attendees were already pricing, at the lower reported figure. No roadshow date was published. Postgres 19 sits around 19 November. DeepSeek's free Harness, Claude Code and Codex calls end 31 October, 16:00 UTC (19:00 Istanbul). Meta's terms still say 30 October. Follow-ups sit on the [AI section](https://www.oguzhan.co/ai/).

## Sources

- [Euronews](https://www.euronews.com/2026/10/14/eus-ai-rules-face-first-enforcement-test-over-lab-incidents)
- [CBS News](https://www.cbsnews.com/news/ftc-subpoenas-anthropic-openai-consumer-protection/) and [Axios](https://www.axios.com/2026/10/15/ftc-openai-anthropic-ai-safety-investigation)
- [NBC News](https://www.nbcnews.com/tech/tech-news/openai-sued-eight-states-alleged-harm-chatgpt-rcna603614)
- [Fortune](https://fortune.com/2026/10/16/openai-discloses-four-more-rogue-incidents-involving-financial-medical-and-government-data/) and [OpenAI misalignment reports](https://alignment.openai.com/misalignment-reports/)
- [The Hindu BusinessLine](https://www.thehindubusinessline.com/info-tech/cert-in-issues-critical-alert-after-autonomous-ai-agents-access-live-systems-of-indian-organisations/article71591314.ece)
- [Semafor](https://www.semafor.com/article/10/15/2026/white-houses-ai-task-force-gets-to-work)
- [Anthropic on evaluators](https://www.anthropic.com/news/an-update-on-independent-evaluators)
- [Politico](https://www.politico.com/news/2026/10/16/anthropic-ai-safety-01124654) and [Channel News Asia](https://www.channelnewsasia.com/business/anthropic-quietly-pitches-its-own-ai-safety-bill-lawmakers-politico-reports-6467581)
- [Mint](https://www.livemint.com/ai/artificial-intelligence/anthropic-offers-blackstone-double-digit-yield-in-chip-financing-deal-what-the-60-billion-deal-entails-11792204532812.html)
- [IMF blog](https://www.imf.org/en/blogs/articles/2026/10/12/global-financial-markets-face-rising-risks-from-ai-bond-yields-and-cyberattacks)
- [CNBC](https://www.cnbc.com/2026/10/14/coreweave-stock-bond-yields-ai-debt.html) and [ASML](https://investor.asml.com/news-releases/news-release-details/asml-reports-eu11.7-billion-total-net-sales-and-eu5.0-billion-net-income-q3-2026)
- [Investing.com](https://www.investing.com/news/stock-market-news/exclusiveinvestors-temper-anthropic-ipo-valuation-expectations-over-revenue-growth-slowdown-sources-say-4952698) and [Swissinfo](https://www.swissinfo.ch/eng/chip-stocks-post-longest-losing-streak-since-2008%3a-markets-wrap/92225060)
- [Meta](https://research.meta.ai/blog/muse-spark-open) and [VentureBeat](https://venturebeat.com/technology/reflections-beam-aims-to-undercut-chinese-open-models-with-fewer-tokens-not-cheaper-tokens)
- [Nvidia](https://blogs.nvidia.com/blog/nemotron-3-5-super-vl/), [Microsoft AI](https://microsoft.ai/news/frontier-pre-training-at-microsoft-ai/) and [PPC Land](https://ppc.land/deepseek-prices-web-search-for-ai-agents-at-0-75-per-1-000-calls/)
- [Anthropic Institute](https://www.anthropic.com/research/employment-at-anthropic)
- [The Register](https://www.theregister.com/databases/2026/10/16/postgres-19-delayed-after-ai-reviewers-find-more-bugs-than-humans-can-fix/5303471) and [Peter Eisentraut](http://peter.eisentraut.org/blog/2026/10/09/the-reverts-will-continue-until-morale-improves)
- [Anthropic on ECDSA](https://www.anthropic.com/research/ecdsa-curve-origins) and [Filippo Valsorda](https://words.filippo.io/seeds-solved/)
- [Nieman Lab](https://www.niemanlab.org/2026/10/metas-new-commercial-terms-will-allow-the-scraping-of-news-sites-legal-experts-say/), [The Verge](https://www.theverge.com/tech/1013409/meta-removes-language-that-may-have-allowed-it-to-scrape-news-sites) and [Nieman follow-up](https://www.niemanlab.org/2026/10/legal-experts-warn-metas-new-terms-still-grant-broad-scraping-permissions-despite-language-changes/)
- [Taiwan News](https://www.taiwannews.com.tw/news/6459737) and [Bloomberg](https://www.bloomberg.com/news/articles/2026-10-16/taiwan-to-curb-ai-chip-exports-to-china-as-part-of-us-trade-deal)
