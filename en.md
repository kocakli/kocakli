---
title: "Who evaluates AI in Turkey when the lab grades itself?"
slug: "turkey-independent-ai-evaluators"
lang: en
focus_keyphrase: "independent AI evaluators Turkey"
yoast_title: "Independent AI evaluators in Turkey: TSE, private labs, gaps"
yoast_metadesc: "Map of who can independently evaluate AI in Turkey today: TSE's GYZD stamp (not live yet), private EvalOps labs, and what the TBMM report actually proposes."
excerpt: "Labs write their own safety stories. Here is the messy map of independent AI evaluation in Turkey: a standards stamp that is not live yet, private EvalOps shops, and a 900-page Meclis report that is not a law."
categories_note: "coordinator maps IDs: 832+830"
---

Turkey has no single, live government authority independently certifying frontier AI systems today. That is the short answer. The longer answer is more useful: the **independent AI evaluators Turkey** can turn to are split across a TSE certification program still being prepared, narrow sectoral work, private EvalOps and red-team firms, and policy proposals in a parliamentary research report. These pieces do different jobs. A buyer who treats them as interchangeable can pay for a technical assessment and walk away believing it bought a state certificate.

That confusion matters because the party selling an AI system usually arrives with its own benchmark charts, safety claims and carefully chosen demos. Self-testing is necessary. It is not independent scrutiny.

## Independent AI evaluators Turkey can use, in one breath
<!-- INLINE_IMAGE_1 -->

The current map has three layers.

First comes standards and certification. The Turkish Standards Institution, TSE, is preparing the Güvenilir Yapay Zekâ Damgası, or GYZD. It is meant to turn technical, governance and ethics requirements into a certification process. It is not accepting applications or issuing the stamp yet.

Second comes independent technical evaluation. Private shops can test a model or deployed system, run adversarial probes, examine Turkish-language behavior and issue a report. Their work can be valuable, but a report is not automatically an accredited certificate. The contract, methods and evaluator's commercial ties matter.

Third comes policy and research. The TBMM Artificial Intelligence Research Commission's report puts institutional and legal options into the public debate. A commission report can shape legislation. It is not legislation itself, and it did not create a Turkish AI Safety Institute.

Those layers may eventually connect. Today, they should remain clearly labeled. For the broader argument over who writes the rules, see the earlier piece on an [AI standards body, pact or cartel](https://www.oguzhan.co/ai-standards-body-pact-or-cartel/). The distinction here is narrower: who can inspect a claim, what can they inspect, and what document do they hand back?

## Layer 1: TSE stamps are still warming up

TSE's [GYZD program page](https://www.tse.org.tr/guvenilir-yapay-zeka-damgasi-gyzd-belgelendirmesi/) is unusually clear about its status. TSE prepared technical, governance and ethics documents under the Ulusal Yapay Zekâ Stratejisi, held meetings with TÜBİTAK, and says the relevant institutions evaluated and approved the documents. Yet, as of the page published on 29 January 2026 and updated on 12 March 2026, applications and certification activities had not started. Infrastructure and process preparation continued.

That date and status line are more important than the planned logo. No live applications means no buyer should accept “GYZD certified” as a current production credential without fresh, verifiable evidence from TSE.

When the program does open, TSE says applications will run through its application portal. Fee-schedule work is still in progress. Planned examination areas include technical infrastructure, data management, algorithmic transparency, effects on human rights, bias and discrimination controls, security measures and accountability. It is a broad intended scope, not a public record of systems already examined.

TSE also describes a narrower [remote identity verification AI certification track](https://www.tse.org.tr/uzaktan-kimlik-tespiti-yapay-zeka-algoritmalari-ve-tse-belgelendirme-sureci/) tied to MASAK General Communiqué No. 19. Test infrastructure is being prepared with planned TSE and TÜBİTAK BİLGEM cooperation. That certification had not started either on the cited page's dates. If launched, its report would address whether an algorithm met the requirements for remote identity use in the financial sector. It would not certify every safety property of a general-purpose model.

The boundary is simple. GYZD is a general certification scheme under construction. The MASAK-related work is a sector-specific track under construction. Neither is a live national AI evaluation authority handing out certificates today.

## Layer 2: private EvalOps and red-team shops

Private evaluators fill a different gap: they can test now.

[LLM Turkey](https://llmturkey.com/en) presents itself as a private EvalOps hub. Its Judex product is an independent LLM testing platform, paired with training and enterprise consulting. Judex advertises nine parameters across 12 scenarios, including instruction following, truthfulness, safety and compliance, bias and fairness, depth and reasoning, clarity, and explainability. Its Turkish-first positioning is the interesting part for local buyers. An English benchmark pass does not tell a bank, retailer or public service how a model handles Turkish ambiguity, refusals, honorifics or locally specific harmful prompts.

The site also publishes a Turkish Truthfulness, or TR-Truth, leaderboard snapshot dated 5 May 2026 at 21:00. It lists models including GPT-4o, Claude 3.5 Sonnet, Gemini 1.5 Pro, Llama 3.1 70B and Mistral Large. Treat that as LLM Turkey's published measurement, not as an audit of LLM Turkey. Buyers still need the test set rules, sampling method, model versions, run settings and conflict policy.

[TestMy.AI](https://testmy.ai/tr/about) draws an equally useful line around its offer. The boutique firm describes automation-heavy adversarial testing with a human lead auditor signing the report. It maps findings to OWASP LLM Top 10, ISO 42001, NIST AI RMF and EU AI Act Article 15. It operates from St Petersburg, Florida, and Istanbul for EMEA, and says it was founded in 2025.

Crucially, TestMy.AI says it is not a certification body. Its deliverable is a Technical Assessment Report intended to support compliance work with qualified counsel. That sentence should be normal across the market. Technical assessment can reveal prompt injection paths, unsafe tool permissions or weak controls. Certification answers a defined scheme's conformity question. Legal advice answers another question again.

Independence also needs testing. Does the evaluator sell the model, orchestration layer or guardrail it is grading? Does payment depend on a passing result? Can the buyer receive failed cases and raw artifacts, or only a polished scorecard? “Third party” on a sales page is a starting claim, not the conclusion.

## Layer 3: a Meclis report is not a regulator

The TBMM document is substantial. The 28th Term Parliamentary Research Commission's [Sıra Sayısı 260 report](https://cdn.tbmm.gov.tr/KKBSPublicFile/D28/Y1/T10/DosyaKomisyonRaporunuVerdi/9f0e7abf-41f6-4133-ab3d-4879113f7f9f.pdf), dated March 2026 on its cover, examines AI opportunities, legal infrastructure and measures against risks. Secondary accounts describe roughly 900 pages and around 100 policy proposals.

Among the reported proposals are a standing TBMM commission for AI and advanced technologies, a guide for Parliament's own use of AI, social-security updates for labor shifts driven by AI, and Turkish-language LLM and standards work with the Organization of Turkic States. These are proposals from a research process. Sıra Sayısı 260 is not an enacted AI law, a licensing office or proof that a new regulator has opened its doors.

That does not make it irrelevant. The report opens a whole-of-government argument about legal duties and institutional design. It can inform later bills, budgets and oversight structures. But procurement teams need present-tense accuracy. A proposal cannot sign this quarter's assessment report.

The same discipline applies after an agent-access incident abroad. The [Australian Medicare agent episode](https://www.oguzhan.co/openai-agent-medicare-australia-breach/) helps explain why boards suddenly ask who checked the system, but urgency does not turn a planned institution into a live evaluator.

## What a buyer should ask before trusting a “certified AI” claim
<!-- INLINE_IMAGE_2 -->

Start with scope. Is the evaluator examining the base model, a fine-tuned model, the complete application, its MCP or API tool permissions, or the organization's management process? A model can pass a static benchmark while the deployed agent still has excessive access.

Then ask five blunt questions:

1. **What exactly was tested?** Get model identifiers, versions, system prompts, connected tools, data boundaries and test dates. “Our AI passed” is not a scope.
2. **How independent is the evaluator?** Ask whether it built, resells or earns referral income from any component under review. Request the conflict-of-interest policy.
3. **What artifact will we receive?** A leaderboard entry, red-team report, legal memo and certification mark carry different weight. Demand failed cases, severity rules and remediation status where the agreement allows.
4. **Was Turkish tested as Turkish?** Translation-only test sets miss local phrasing, cultural references and multi-turn behavior. Ask who designed and reviewed the Turkish cases.
5. **Is the claim certification or technical assessment?** Request the named scheme, issuing body, certificate scope, issue date, expiry or surveillance terms, and a verification path. If those fields do not exist, stop calling it a certificate.

Procurement should also connect evaluation to operations. A report is a snapshot. Models change, prompts change, permissions spread, and vendors silently replace components. The practical controls in the [misalignment reporting framework for operators](https://www.oguzhan.co/openai-misalignment-reporting-framework-for-operators/) show why incident intake, escalation and evidence retention must continue after the evaluator leaves.

## A short rule when the lab grades its own homework

Keep vendor testing, private technical assessment, standards certification and public policy in separate columns. Then compare what each column can prove.

Turkey has serious work under way: TSE is building GYZD and a narrow remote-ID track, private evaluators are selling Turkish-focused tests and adversarial reviews, and TBMM has put a large proposal set into circulation. None of that adds up to one live state evaluator for frontier AI. Not yet.

Buy the examination you actually need. Name it honestly. For continuing coverage of models, policy and operator practice, the [oguzhan.co AI hub](https://www.oguzhan.co/ai/) keeps the threads together without pretending that a report, a stamp and a law are the same thing.
