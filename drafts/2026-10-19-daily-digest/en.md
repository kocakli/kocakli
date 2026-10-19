---
title: "OpenAI misalignment reports, curve seeds, and open weights"
slug: openai-misalignment-reports-claude-ecdsa-seeds
excerpt: "Four June cases on OpenAI's public misalignment page, Claude's timestamp reading of the NIST seeds, three open-weight releases, and Anthropic's junior hiring shares."
focuskw: "OpenAI misalignment reports"
yoast_title: "OpenAI misalignment reports, seeds, and open weights"
yoast_metadesc: "OpenAI posted four June misalignment cases on 15 Oct, two rated critical. Claude traced NIST seeds to 1997 timestamps. Three open-weight models shipped."
categories: AI
---

OpenAI misalignment reports went up on 15 October: four June cases, two rated critical per [Fortune](https://fortune.com/2026/10/16/openai-discloses-four-more-rogue-incidents-involving-financial-medical-and-government-data/). One model spent Sepolia test ETH from an address it did not own. Another pulled 147,451 non-public rows while looking up public figures. All four sit in training, evaluation, and internal use, with no ChatGPT customer account among them.

## 🚨 OpenAI misalignment reports: four June cases, two critical
<!-- INLINE: openai-agent-borrowed-keys -->

[OpenAI's page](https://alignment.openai.com/misalignment-reports/) posted the four on 15 October, all from June. Fortune: three unknown until August or September, 19 incidents on the page, two of the new four rated critical.

- "Using a funded test cryptocurrency wallet without authorization" (26 June)
- "Accessing and changing internal systems during dashboard research" (17 June)
- "Retrieving server secrets and bypassing authorization on a government statistics website" (17 June)
- "Circumventing internet restrictions through an external browser" (16 June)

A GPT-5.6 Sol family internal research model, in training, had to update a crypto trading prototype and deploy contracts on Sepolia, an Ethereum test network. No funded wallet. Per [OpenAI's wallet report](https://alignment.openai.com/misalignment-reports/using-a-funded-test-cryptocurrency-wallet-without-authorization/), it derived accounts from publicly known developer recovery phrases, checked 362 addresses, found Sepolia ETH, and paid the fees. Chain of thought asked if this was ethical, then called the funds "effectively abandoned" and Sepolia "valueless". Deployment succeeded. The final report hid the source (26 June, found 25 September 2026). OpenAI's words: a model "can substitute its own judgment about likely harm for the account holder's permission". Test ETH has no market value.

A "highly persistent internal model", in an evaluation, was asked for published figures from an international research organization's public dashboard, internet limited to HTTP GET. Per [OpenAI's dashboard report](https://alignment.openai.com/misalignment-reports/accessing-and-changing-internal-systems-during-dashboard-research/), it took live OpenSearch credentials from public JavaScript, downloaded 1,489 user-directory records (names and emails), and changed a cluster setting. A second run changed a token setting, took a cloud-storage token, and downloaded five non-public tables, 147,451 rows. It restored the setting, kept the token, wrote "but ethical?" then "focus on correctness", and disclosed nothing. All five answers in each evaluation were marked incorrect. Found by 13 August 2026.

Fortune on the government site: after a block, the model bypassed access controls and downloaded 24 years of hospital-bed data from an unnamed government website.

OpenAI, quoted by Fortune: strengthened security controls, no live internet in training and evaluation, improved alignment grading, monitoring on all RL and evaluation traffic. A retrospective monitor caught the cases after the July Hugging Face incident.

In the [11 October weekly](https://www.oguzhan.co/ai-weekly-5-11-oct-2026-oath-and-agents/) I noted OpenAI was reviewing past incidents. This page is that review.

## 🔐 Where did the NIST curve seeds come from?
<!-- INLINE: ecdsa-timestamp-seeds -->

Unix timestamps, in under half an hour. [Anthropic, 16 October](https://www.anthropic.com/research/ecdsa-curve-origins).

NIST adopted the ECDSA curves in 2000, FIPS 186-2. A seed's hash sets the coefficient. The NSA supplied the seeds with no explanation, which fed years of backdoor suspicion.

Jerry Solinas (NSA, 2015) said the seeds hashed a joke, something like "Give Bob and Jerry a raise". He died in 2023.

In October 2026 an employee asked an internal research model, in a sandbox, clue withheld. Claude found the P-192, P-224, P-256, P-384, and P-521 seeds. No hash. The bytes are `lrand48` output from the C library, seeded with a Unix timestamp. According to Anthropic, P-256 was candidate 1,842 of a run seeded at 16 August 1997, 01:52:34 UTC. Prime-curve timestamps fall between May 1997 and April 1998.

Claude saw a zero top bit in every 32-bit word (the `lrand48` signature), recovered the states, and used LLL lattice reduction on the truncated outputs.

Anthropic: "This is not a cryptographic break, new attack, or weakness". Backdoors look "much less plausible". No action needed.

Still open: B-163's seed, and base points of P-224, P-256, P-384, and P-521. For P-256, candidate 876 would also have worked. Nobody knows why.

Filippo Valsorda's $36,864 bounty goes to the Internet Security Research Group, behind Let's Encrypt. Anthropic published CC0 Python. The published script reproduces the P-256 seed.

## 🔓 Three open-weight models in three days

On 15, 16, and 17 October, Meta, Reflection, and DeepSeek shipped open-weight models. I have not run them.

[Muse Spark Open](https://research.meta.ai/blog/muse-spark-open): natively multimodal, for coding and agents. Meta's claim: "the most capable US open-weight model to date". Two Apple M5 Ultra Mac Studios with MLX, per Meta. Muse Model License, limited commercial terms, outside the OSI open source definition. Muse Wonder is separate and closed ([15 October digest](https://www.oguzhan.co/muse-wonder-gemini-4-argon-frontier-agents/)).

[Beam](https://reflection.ai/blog/beam-is-available): sparse MoE, text only, BF16, FP8, and NVFP4, more than 40 partners. Reflection's own card, via the [Hugging Face blog](https://huggingface.co/blog/reflection-beam): SWE-bench Verified 81.6% (BF16). Still a promise in the [12 October post](https://www.oguzhan.co/claude-internet-access-anthropic-evaluations/).

[DeepSeek-V4.1-Flash-1017](https://huggingface.co/deepseek-ai/DeepSeek-V4.1-Flash-1017): "minor update" on the [changelog](https://api-docs.deepseek.com/updates). DeepSeek's own table: DeepSWE v1.1 77.0 (74.2 before), Opus 5 at 74.0, Terminal-Bench 4.0 42.3 (31.2 before). API `deepseek-flash`, price unchanged. Search and Fetch the same day at $0.75 per 1,000 calls per endpoint. Billing from 31 October 2026, 16:00 UTC (19:00 Istanbul), per @deepseek_ai on X.

| Model | Lab | Released | Size (total / active) | Context | License |
|---|---|---|---|---|---|
| Muse Spark Open | Meta | 15 Oct 2026 | 816B / 42B | 1M tokens | Muse Model License |
| Beam | Reflection | 16 Oct 2026 | 501B / 23B | 1M tokens | Apache 2.0 |
| DeepSeek-V4.1-Flash-1017 | DeepSeek | 17 Oct 2026 | n.d. | 1M recommended | MIT |

Whoever deploys the weights inherits the monitoring above.

## 👩‍💻 How far did junior hiring fall at Anthropic?

Junior technical hires fell from 27% to 9%, and junior employees from 21% to 14% of technical departments, since early 2025 ([Anthropic, 16 October](https://www.anthropic.com/research/employment-at-anthropic)). Absolute technical hiring still grew, so these are shares. By August 2026 agent hours outnumbered employee hours six to one. Anthropic calls that runtime. April 2026 survey: 20% described a shift from doing the work to managing Claudes. Median meeting time is up 20% on a year ago. Early warning system up, internal redeployment first. Anthropic admits this does not address the junior hiring slowdown.

The [Public Benefit Fund](https://www.anthropic.com/news/public-benefit-fund) (18 October) is a wholly owned LLC. Subject to stockholder approval, 5% of shares now, plus 2% more at the board's discretion for every 50% increase in company value above an undisclosed baseline. Large nonprofit donations or direct distributions. Labor-market impact is the example. $200 million already committed to labor-market work. Fund equity will not be used for lobbying or political giving. With founders' and employees' pledges, Anthropic says roughly 20% of shares go to the public good.

I read all four over the weekend. Agents did more than they were asked. Who writes that down?
