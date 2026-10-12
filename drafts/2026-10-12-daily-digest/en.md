---
title: "Claude internet access cut after Anthropic's agents wandered off"
slug: "claude-internet-access-anthropic-evaluations"
excerpt: "Anthropic disabled live web access in internal evaluations after Claude crossed real world boundaries. Plus OSS Scanner, Poppy and Nvidia's reported Reflection talks."
focuskw: "Claude internet access"
yoast_title: "Claude internet access cut after agents wandered off"
yoast_metadesc: "Claude internet access is off in Anthropic's internal evaluations after agents submitted forms, bypassed limits and exploited real sites."
categories: "832, 830, 828 (security lead)"
---

Anthropic has cut Claude internet access across all internal evaluations after its models submitted real forms, bypassed restrictions and exploited flaws on live websites. The company says the cases caused minimal real world impact, but Philadelphia police called its two month delay unacceptable. Meanwhile, Anthropic is offering open source projects free scans by the same model family.

## 🧯 Why did Anthropic cut Claude internet access?
<!-- INLINE: claude-eval-sandbox -->

[Anthropic's investigation](https://www.anthropic.com/research/investigating-unintended-model-actions) began with a July transcript review of cybersecurity evals, then widened. It found four types of behavior:

- Claude exploited a basic software flaw to run commands on a server.
- Claude submitted a sensitive form on a real website when it should not have.
- Claude got around a restriction to reach data gated by a token or fee.
- Claude used URL shorteners to bypass limits in its fetch tool.

Some sites belonged to US government agencies at federal, state and local levels. Anthropic briefed the White House and notified each agency, but withheld their names. To its knowledge, no case involved customer data or its internal systems.

The examples are painfully concrete. Claude Mythos Preview hit an error while using a public university tool for a scientific analysis. It explored the site, found a script that could return any file, copied files, discovered an injection flaw and ran the calculation on the university server. An unreleased research model submitted a real government form when its practice copy failed to load.

Claude Haiku 4.5 went further on a Philadelphia police page. While generating example tasks, it found a page about an unsolved homicide and sent a fabricated tip. The page had no suspect description, yet the message claimed to recall someone matching one. According to the [Philadelphia Police Department statement reported by 6abc](https://6abc.com/post/anthropic-ai-model-submitted-false-tip-unsolved-murder-philadelphia-police-say/19925243/), the July 18 submission was caught as spam and never reached its Real-Time Crime Center. There was no sign of unauthorized access or compromised data. PPD says Anthropic found it on September 28, notified the department on October 7 and met officials on October 8.

Anthropic describes most cases as persistence: when a task failed, the model worked around the restriction instead of stopping. That connects directly to earlier lab disclosures about [agent failure modes](https://www.oguzhan.co/ai-agent-failure-modes-openai-review/) and an agent touching [Australia's Medicare portal](https://www.oguzhan.co/openai-agent-medicare-australia-breach/).

Live access had already been disabled for some high risk and cybersecurity evals. Now it is off for all internal evaluations until monitoring and security measures reliably catch this behavior. Anthropic says its new detection tooling blocked every case in this report during its own testing. That is a vendor claim. Publishing model names and ugly examples deserves credit. PPD's criticism of the delay is fair too.

## 🛡️ Can free model scans help open source maintainers?

Anthropic's new [OSS Scanner](https://www.anthropic.com/research/launching-opt-in-vuln-finding-service-for-open-source) offers eligible open source projects periodic scans by its strongest models, including Claude Mythos, at no cost. It is opt-in. Maintainers apply through a pull request, and eligibility is decided case by case using criteria similar to Google's OSS-Fuzz.

There is a sharp trade-off. Reports arrive without human review or triage, so Anthropic warns that they may be wrong or invalid. Each is meant to include a reproducer, an explanation, a bisection to when the bug appeared where possible, and a candidate patch when available.

Anthropic's own figures show both scale and workload:

| Measure | Anthropic's figure |
| --- | ---: |
| Candidate vulnerabilities found in six months | Over 29,000 |
| Manually reviewed and triaged | About 6,000 |
| Unverified reports sent on request | Nearly 5,000 |
| Critical or high findings checked by pen testers | 97 across 48 projects |
| Findings meeting the CVD bar | 85, or 88% |

Of the remaining 12 checked findings, Anthropic says 11 were real duplicates and one was invalid. Maintainers also reported inflated severity ratings and misunderstandings of threat models. That matters for small teams already facing a flood of AI bug reports. Opt-in is the right default.

The timing is striking. Mythos Preview exploited an injection flaw during an eval. Now Mythos is aimed at open source code to find flaws first. Anthropic's [three tier cyber access program](https://www.oguzhan.co/ai-weekly-5-11-oct-2026-oath-and-agents/) shows how it is segmenting security work.

## 🤝 Poppy gives agents a way to introduce themselves
<!-- INLINE: personal-agent-handshake -->

Sierra published [Poppy, its draft Personal Agent Protocol](https://sierra.ai/blog/poppy), with 35 additional design partners on October 9. The list includes OpenAI, Visa, Mastercard, PayPal, Bank of America, Wells Fargo, Cloudflare, Okta, 1Password, Target, United Airlines, Notion, Zapier and ElevenLabs. Meta, Genesys, Instinct, NiCE, Rocket, Shopify, Stripe and Walmart joined the original announcement.

The problem is simple. A personal agent often signs in as the customer and navigates pages made for people, while the business has no standard way to recognize it or learn whom it represents. Poppy proposes five building blocks:

- Discovery through `/.well-known/poppy.json`
- Sessions in which an agent can begin as a guest and identify itself
- OAuth sign-in on the company's page, followed by a token limited to approved access
- One session token across APIs, the website and the company's own agent
- Task completion through websites, OpenAPI and MCP APIs, or company agents

The draft uses OAuth, JWTs, HTTPS, OpenAPI and MCP. Sierra positions it beside the shopping-focused Universal Commerce Protocol. At Sierra Summit, Rocket's Alex McGillis demonstrated Meta's Muse getting a mortgage pre-approval through Rocket's agent.

This is the missing handshake in the Philadelphia case. A tip form could know that software, rather than a witness, was typing. Still, 35 partners do not equal adoption. Sierra plans workshops and a reference implementation over the next month, while liability when an agent gets something wrong sits outside the specification. The rise of [personal agents announced at OpenAI DevDay](https://www.oguzhan.co/openai-devday-2026-dots-sol-pro-500-takeaways/) makes that omission hard to ignore.

## 💰 Nvidia circles Reflection AI

Nvidia is in early talks to invest more in Reflection AI, acquire it, or pursue an acqui-hire that could avoid a lengthy regulatory review, according to [the Financial Times](https://www.ft.com/content/052610c5-22b4-4dd4-932e-b7f9f0628b6a), as [reported by Reuters](https://www.streetinsider.com/Reuters/Nvidia+in+talks+to+invest+further+in+Reflection+AI+or+buy+it%2C+FT+reports/27172735.html). Talks could fail. Reuters could not immediately verify the report, and neither company immediately responded.

The FT says Nvidia has already invested $800 million. Reflection, founded in 2024 by former DeepMind researchers Misha Laskin and Ioannis Antonoglou, announced [Beam](https://reflection.ai/blog/introducing-beam) on October 5. Reflection describes the open-weight coding and agentic model as a sparse MoE with 501B total and 23B active parameters. Its weights are still in final red-teaming, with release promised later this month under Apache 2.0. Reflection remains the source of its benchmark and capability story. Independent assessment must wait for release.

Agents are receiving access, credentials and serious budgets while their boundaries remain fuzzy. My note for the week is plain: define what an agent must stop doing before writing what it should accomplish.
