# Notes: frontier model explainer (20 Oct 2026)

Evergreen pair for oguzhan.co. English is original. Turkish is an original column, not a line translation. Voice pack used: `oguzhan-co-drafts/AGENT_VOICE.md` at commit `9f331c4` (not on `main`).

Target queries, not stated in the posts: Turkish GSC "frontier model ne demek" around position 11 with 0 clicks. English target "what is a frontier model".

## Files

- `en.md` slug `what-is-a-frontier-model`, focus `frontier model`
- `tr.md` slug `frontier-model-ne-demek`, focus `frontier model ne demek`
- Word counts on 20 Oct 2026, body only, HTML comments excluded. Raw split includes URLs. Stripped count drops URLs and markdown markers.
  - EN raw 1683, stripped 1656. Target 1300 to 1700. Direct-answer box 52 words.
  - TR raw 1484, stripped 1456. Target 1100 to 1500. Kısa yanıt box 44 words.
- `yoast_title` EN 44 characters, TR 39. `meta_description` EN 149, TR 139.

## Internal links (all returned HTTP 200)

- EN hub https://www.oguzhan.co/ai/
- TR hub https://www.oguzhan.co/tr/yapay-zeka/
- SAFA EN post 4708 https://www.oguzhan.co/ai-standards-body-pact-or-cartel/
- SAFA TR post 4707 https://www.oguzhan.co/tr/ai-standart-organi-pakt-mi-kartel-mi/
- China weights EN https://www.oguzhan.co/china-ai-export-controls-model-weights/
- China weights TR https://www.oguzhan.co/tr/cin-yapay-zeka-ihracat-kontrolu-model-agirliklari/

The TR SAFA slug still contains `standart-organi`. That is the live URL. The draft does not use "standart organı" in prose.

## Cover

Quiet dusk shoreline. The waterline is the moving edge. Two small handwritten ticks in the margin, labeled `10^25 FLOP` and `10^26 operations`, with no company logos, no leaderboard, no glowing brain, no circuit-face. Wide 16:9, enough empty sky for a title. Alt idea: "A shoreline at dusk, marked with two compute thresholds."

## Inline images

Each draft has two `<!-- INLINE: ... -->` markers.

1. Timeline, July 2023 to January 2026: Forum launch, EU 10^25 presumption, UK rename, California 10^26.
2. Four overlapping circles: frontier, foundation, open-weight, small. Unnamed models only.

## Sources checked

Frontier Model Forum

- Announcement, 26 July 2023. Founders named there: Anthropic, Google, Microsoft, OpenAI. Definition: large-scale machine-learning models that exceed the capabilities present in the most advanced existing models and can perform a wide variety of tasks. https://www.frontiermodelforum.org/updates/announcing-the-frontier-model-forum/
- About page, read 20 Oct 2026. Membership definition: a general-purpose model that outperforms, on conventional benchmarks or high-risk capability assessments, all other models widely deployed for at least 12 months. Wider than current state of the art on purpose. 501(c)(6), established 2023, says it does not lobby. https://www.frontiermodelforum.org/about-us/
- Members on that date: Amazon, Anthropic, Google, Meta, Microsoft, OpenAI. https://www.frontiermodelforum.org/membership/

EU AI Act, Regulation (EU) 2024/1689

- Legal category is general-purpose AI model with systemic risk, not "frontier model".
- Article 51(2): presumption of high-impact capabilities when cumulative training computation is greater than 10^25 floating-point operations. Service Desk summary, consolidated text as of 27 July 2026: https://ai-act-service-desk.ec.europa.eu/en/ai-act/article-51
- Recital 111: high-impact means matching or exceeding the most advanced general-purpose models. Training total includes pre-training, synthetic data generation, and fine-tuning. https://ai-act-service-desk.ec.europa.eu/en/ai-act/recital-111
- Commission FAQ: 10^25 line, Article 55 duties (evaluate, report serious incidents, cybersecurity), notification when the compute line is met or will be met, and an indicative 10^23 FLOP sign for general-purpose models generally (guidelines section 2.1), not for systemic risk. https://digital-strategy.ec.europa.eu/en/faqs/general-purpose-ai-models-ai-act-questions-answers
- Open-source release makes Article 55 duties harder. Same FAQ, pointing at recital 112.

United Kingdom

- AI Safety Institute renamed AI Security Institute on 14 February 2025. https://www.gov.uk/government/news/tackling-ai-security-risks-to-unleash-growth-and-deliver-plan-for-change
- AISI, 12 Oct 2026: more than 55 models evaluated before release. The post says this is not a mandate. https://www.aisi.gov.uk/blog/towards-technical-best-practice-for-frontier-ai-development
- Open-weight comparison page exists (HTTP 200). The drafts say the comparison exists. They do not quote its findings. https://www.aisi.gov.uk/blog/how-far-behind-the-frontier-are-leading-open-weight-models-on-cyber

California SB 53

- Transparency in Frontier Artificial Intelligence Act. Chapter 138, Statutes of 2025. Approved 29 Sept 2025. Effective 1 Jan 2026. Business and Professions Code sections 22757.10 through 22757.16.
- 22757.11(i): frontier model = foundation model trained with more than 10^26 integer or floating-point operations, including the original run plus later fine-tuning, reinforcement learning, or other material modification.
- Large frontier developer: with affiliates, annual gross revenue above $500 million in the prior calendar year.
- Catastrophic risk: foreseeable and material risk of contributing to death or serious injury of more than 50 people, or more than $1 billion in property damage, from a single incident of a listed kind.
- Code: https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?lawCode=BPC&division=8.&title=&part=&chapter=25.1.&article=
- Governor's note: https://www.gov.ca.gov/2025/09/29/governor-newsom-signs-sb-53-advancing-californias-world-leading-artificial-intelligence-industry/

October 2026 examples, primary pages only, no ranking, no FLOP claim

- OpenAI, 7 Oct 2026, GPT-6 reaching more ChatGPT users. First GPT-6 models for paid customers "last month." https://openai.com/index/gpt-6-for-everyone/
- Anthropic, Claude Opus 5.5, 22 Sept 2026. External evaluators named on the page include Frontier Design and METR. API price on that page: $4 / $20 per million input / output tokens. https://www.anthropic.com/claude-opus-5-5
- Anthropic, Claude Sonnet 5.5, 28 Sept 2026. $2 / $10 per million. https://www.anthropic.com/claude-sonnet-5-5
- Anthropic, Claude Haiku 5.5, 7 Oct 2026. Anthropic calls it a small model. https://www.anthropic.com/claude-haiku-5-5
- Google, Gemini 4 Argon, 13 Oct 2026. Google's words: "our latest frontier model." Introductory $2 / $10 per million input / output tokens, then $4 / $20 after 30 Nov 2026. Fairwind for cyber defenders without ordinary cyber guardrails. Frontier Safety Framework named on the post. https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-argon/

Foundation model

- Stanford CRFM, Bommasani et al., 2021, *On the Opportunities and Risks of Foundation Models*. https://arxiv.org/abs/2108.07258
- The drafts paraphrase the usual abstract definition (broad data, generally self-supervision at scale, adaptable to many downstream tasks). They are not a long quotation.

## Open fact questions

1. EUR-Lex HTML for Regulation (EU) 2024/1689 returned almost no body in this run. The 10^25 figure is the Commission FAQ plus the Service Desk summary of the consolidated text as of 27 July 2026. On that Service Desk article page the exponent renders as "1025" in the statute extract and as 10^25 in the summary. Confirm the Official Journal glyphs before publish.
2. I did not find a delegated act moving Article 51(2). Unconfirmed: any act between 28 July 2026 and 20 Oct 2026.
3. Regulation (EU) 2026/1744 (Digital Omnibus on AI) amends the AI Act. The Service Desk says its text is the consolidated version and still describes the 10^25 presumption. I did not diff every Omnibus edit.
4. No training-FLOP figure for GPT-6, Opus 5.5, Sonnet 5.5, Haiku 5.5, or Gemini 4 Argon was in the posts used. Do not add a sentence that any of them clears 10^25 or 10^26 unless a lab or the Commission publishes the number.
5. No UK statute with a FLOP definition of frontier model turned up. If one exists, the UK paragraph needs it.
6. Frontier Model Forum join dates for Amazon and Meta are not on the membership page. Not stated.
7. OpenAI's 7 Oct 2026 post does not, in the portion used here, name GPT-6 Astra, Sol, or Luna. A separate page, "Introducing GPT-6 Sol and Luna," has a confusing update line dated 29 Sept 2026. Those names were left out on purpose.
8. AISI's open-weight cyber post: search snippets mention a 4-to-7-month gap. Not quoted. Read the full post before adding the number.
9. Haiku 5.5's per-token price was not copied. Anthropic says it costs about 75% less to run than Haiku 4.5. That comparison was left out.
10. The Commission FAQ still cites a 2024 Epoch estimate that training above 10^25 FLOP cost tens of millions of euros. Left out as stale for October 2026.
11. SAFA launch status was not re-checked after this site's 19 Oct 2026 update of posts 4708/4707. The drafts link that essay and do not claim a launch date.
12. Google's Argon post includes benchmark ranks and scientific claims (fusion, rare disease, enzyme design). None of those claims are in the drafts.
13. Amazon, Meta, and Microsoft are named only as Forum members. No October 2026 model of theirs was verified for this piece.
