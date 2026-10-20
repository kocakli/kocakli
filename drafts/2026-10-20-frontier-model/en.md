---
title: "What is a frontier model?"
yoast_title: "What is a frontier model? A plain definition"
meta_description: "A frontier model is a general-purpose AI system at the current leading edge. Origin, EU and California compute lines, and what builders should check."
slug: what-is-a-frontier-model
focus_keyword: frontier model
---

> **Direct answer.** A frontier model is a general-purpose AI model at the leading edge of what current systems can do. The edge moves. Labs, the Frontier Model Forum, and some laws use the label for the most capable models, often tying it to training compute or to capability tests, not to a brand name.

I use frontier model for a place on a moving map of general-purpose systems. Last year's frontier model is often this year's ordinary one. Blogs, safety notes, and statutes do not draw the same line, so I ask which definition a sentence is using. Longer notes sit on the [AI hub](https://www.oguzhan.co/ai/).

## Where the frontier model label comes from

On 26 July 2023, Anthropic, Google, Microsoft, and OpenAI announced the [Frontier Model Forum](https://www.frontiermodelforum.org/updates/announcing-the-frontier-model-forum/). The announcement defined frontier models as large-scale machine-learning models that exceed the capabilities of the most advanced existing models and can perform a wide variety of tasks.

Its [about page](https://www.frontiermodelforum.org/about-us/) uses a wider membership test. A frontier AI model there outperforms, on ordinary benchmarks or high-risk tests, every other model widely deployed for at least 12 months, so more organizations can join the safety work. The Forum is a member-funded 501(c)(6) and says it does not lobby. On 20 October 2026 its member page listed Amazon, Anthropic, Google, Meta, Microsoft, and OpenAI. A seat is not a ranking and does not disclose training compute.

The EU AI Act, Regulation (EU) 2024/1689, does not make frontier model the legal category. It speaks of a general-purpose AI model and, for the top tier, a general-purpose AI model with systemic risk. [Article 51](https://ai-act-service-desk.ec.europa.eu/en/ai-act/article-51) classifies a model that way if it has high-impact capabilities, judged with technical tools and benchmarks, or if the Commission finds equivalent capability or impact under Annex XIII.

Article 51(2) is the number people quote. Cumulative training computation above 10^25 floating-point operations presumes high-impact capabilities. Recital 111 reads that as matching or exceeding the most advanced general-purpose models, and the total includes pre-training, synthetic data generation, and fine-tuning. The Commission may move the threshold by delegated act. Its [FAQ](https://digital-strategy.ec.europa.eu/en/faqs/general-purpose-ai-models-ai-act-questions-answers) still states 10^25, as does the Service Desk consolidated text of 27 July 2026. I have not found a delegated act that changed it. The same FAQ uses more than 10^23 FLOP, with language, image, or video generation, only as a sign that a model is general-purpose at all.

The United Kingdom uses the frontier label and, in the sources I checked, attaches no FLOP cutoff. On 14 February 2025 it renamed the AI Safety Institute the [AI Security Institute](https://www.gov.uk/government/news/tackling-ai-security-risks-to-unleash-growth-and-deliver-plan-for-change). The Institute tests advanced models for cyber and for chemical or biological assistance. On 12 October 2026 it said it had independently evaluated [more than 55 models before release](https://www.aisi.gov.uk/blog/towards-technical-best-practice-for-frontier-ai-development).

California put the words in a statute. Senate Bill 53, the Transparency in Frontier Artificial Intelligence Act, was approved on [29 September 2025](https://www.gov.ca.gov/2025/09/29/governor-newsom-signs-sb-53-advancing-californias-world-leading-artificial-intelligence-industry/) and took effect on 1 January 2026. It is Business and Professions Code sections 22757.10 through 22757.16. [Section 22757.11](https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?lawCode=BPC&division=8.&title=&part=&chapter=25.1.&article=) defines a frontier model as a foundation model trained with more than 10^26 integer or floating-point operations. The count includes the original run, later fine-tuning, reinforcement learning, and any other material modification of a preceding foundation model.

A large frontier developer, with affiliates, had gross revenue above $500 million in the prior year and must publish a frontier AI framework. Any frontier developer must publish a transparency report before or with deployment of a new or substantially modified frontier model. Catastrophic risk is a foreseeable, material chance of contributing, in one listed incident, to the death or serious injury of more than 50 people or to more than $1 billion in property damage. The list includes expert help with a chemical, biological, radiological, or nuclear weapon, a cyberattack or listed crime without meaningful human oversight, and evasion of developer or user control.

California's line is ten times the EU presumption and counts integer operations too. A Commission decision can also place a model in the EU tier. A lab can say frontier and publish neither number.

<!-- INLINE: A horizontal timeline from July 2023 to January 2026. Marks for the Frontier Model Forum announcement, the EU AI Act's 10^25 floating-point presumption, the UK AI Security Institute rename, and California SB 53's 10^26 threshold. No logos and no leaderboard. -->

Who is allowed to move that line is a separate argument. I wrote it up around the proposed Standards Authority for Frontier AI: [who gets to set the speed limit](https://www.oguzhan.co/ai-standards-body-pact-or-cartel/).

## Frontier, foundation, open-weight, small

One model can carry more than one of these labels.

A foundation model, in the 2021 Stanford CRFM report [On the Opportunities and Risks of Foundation Models](https://arxiv.org/abs/2108.07258), is trained on broad data, generally with self-supervision at scale, and can be adapted to many later tasks. SB 53 uses the same idea: broad data, general output, many distinct tasks. A frontier model in that statute is such a model past the compute line. The EU general-purpose model is the Act's cousin, built to perform many tasks inside many downstream systems.

Open-weight means the parameters can be downloaded and run. Training data, code, and license are separate facts, and so is capability. UK AISI compares [leading open-weight models with closed frontier systems](https://www.aisi.gov.uk/blog/how-far-behind-the-frontier-are-leading-open-weight-models-on-cyber) on cyber tasks, which only works if the labels are not opposites. When the file is the sensitive object, export rules take over, as in [China, export controls, and model weights](https://www.oguzhan.co/china-ai-export-controls-model-weights/). Small is a product cut. On 7 October 2026 Anthropic called [Claude Haiku 5.5](https://www.anthropic.com/claude-haiku-5-5) a small model for high-volume summaries, classification, and support. It can still be a foundation model.

| | Frontier model | Foundation model | Open-weight model | Small model |
| --- | --- | --- | --- | --- |
| Question | At the current leading edge? | Trained broadly, then adapted to many tasks? | Can the weights be downloaded and run? | Cheap and fast, for a narrower job? |
| What sets it | A moving edge. California: more than 10^26 operations. EU cousin: presumed systemic risk above 10^25 FLOP. | Breadth. Stanford CRFM, 2021. SB 53 section 22757.11(f). | The release, not the score. | Price, latency, and the provider's own cut. |
| Overlap | Often a foundation model. Sometimes open-weight. | Can be frontier, ordinary, or small. | Near the frontier, or years behind it. | Can still be a foundation model. |
| October 2026 | Google calls Gemini 4 Argon its latest frontier model. | Claude Opus 5.5, sold for many kinds of hard work. | A release choice. See the weights note above. | Anthropic calls Haiku 5.5 a small model. |

<!-- INLINE: Four overlapping circles labeled frontier, foundation, open-weight, and small. One unnamed model sits in the frontier and foundation overlap. Another sits in open-weight only. A third sits in small and foundation. No brand logos and no scores. -->

## What labs were shipping in October 2026

No ranking. None of these posts states training compute, so none shows that a named model clears 10^25 or 10^26.

On 7 October 2026 OpenAI said a [GPT-6 model](https://openai.com/index/gpt-6-for-everyone/) was reaching more ChatGPT users, after the first GPT-6 models went to paid customers the month before.

Anthropic's posts name Claude [Opus 5.5](https://www.anthropic.com/claude-opus-5-5) (22 September 2026), Claude [Sonnet 5.5](https://www.anthropic.com/claude-sonnet-5-5) (28 September 2026), and Claude Haiku 5.5 (7 October 2026). It describes Opus 5.5 as the model for complex work and says Frontier Design and METR tested it before release. It calls Haiku 5.5 small.

On 13 October 2026 Google called [Gemini 4 Argon](https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-argon/) its latest frontier model and tied the safety testing to its Frontier Safety Framework.

I am not naming an October 2026 model for Amazon, Meta, or Microsoft. I did not verify a primary release page for them here.

## Cost, access, and the evaluation

**Cost.** Anthropic lists Opus 5.5 at $4 per million input tokens and $20 per million output tokens, Sonnet 5.5 at $2 and $10. Google listed Argon at an introductory $2 and $10 per million, then $4 and $20 after 30 November 2026. Haiku 5.5 is the high-volume Claude in that family. The model id sets the bill, not the frontier label. I start summaries and first passes on the smaller id.

**Access.** Google points cyber defenders to Fairwind for Argon without the ordinary cyber guardrails. Anthropic offers a life sciences verification program and a cyber path for higher-risk defensive work. A standard API key is not those programs.

**Safety evaluations.** Under Article 55, the provider of an EU general-purpose model with systemic risk must assess and mitigate that risk, evaluate the model, report serious incidents, and protect the model and its infrastructure. The [Commission FAQ](https://digital-strategy.ec.europa.eu/en/faqs/general-purpose-ai-models-ai-act-questions-answers) is the short account. Providers also notify the Commission when compute meets or will meet Article 51(2). That duty is theirs. Tools, data, and what the user can reach stay with the product.

In California I read the published framework and transparency report before I treat a safety adjective as a spec. The Institute's pre-release testing is not a license. "Evaluated before release" needs a scope: biology, cyber, agents, or narrower.

I check which definition the sentence uses, what the test covered, and what happens if the weights can be downloaded.

## Questions I keep getting

### Is a frontier model the same as a foundation model?

No. Foundation means broadly trained and adaptable. Frontier, for the Forum, means the current leading edge. California adds a compute line: more than 10^26 operations, with later fine-tuning and reinforcement learning counted. In that statute every frontier model is a foundation model. Most foundation models are not frontier models.

### Does the EU AI Act say frontier model?

Not as the legal category. It says general-purpose AI model with systemic risk, presumes high-impact capabilities above 10^25 floating-point operations, and lets the Commission designate a model or later change the threshold. If a vendor treats "not frontier" as "outside the Act," ask which article they mean.

### Can an open-weight model be a frontier model?

Yes. Open-weight is the release. Frontier is capability, or in some laws a compute total. Weights can ship for a system at the edge or far behind it. Commission guidance says systemic-risk duties are harder after an open-source release, so the tests belong before the file moves.

### Do I need a frontier model to ship?

Usually no. I ship most work on a smaller or mid-tier id and call a more capable model only for steps that fail a check. Sending every call to a frontier system is a cost choice, not a safety proof.
