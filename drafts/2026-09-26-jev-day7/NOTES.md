---
title: "Editorial notes: Jev Day 7 ecosystem and limits"
slug: "jev-day7-editorial-notes"
focus_keyphrase: "Jev ecosystem editorial notes"
yoast_title: "Jev Day 7 editorial notes"
yoast_metadesc: "Editorial checks, source links, internal links, and word counts for the English and Turkish Jev ecosystem drafts."
excerpt: "Production notes for the bilingual Jev Day 7 drafts, including source verification, link inventory, length checks, and voice review."
---

## Word counts

Counts cover body text after YAML frontmatter. Markdown link text and code identifiers count as words.

- `en.md`: 1,231 words
- `tr.md`: 976 words

Target checks:

- EN target 900 to 1,400: pass
- TR target 750 to 1,100: pass
- `INLINE_IMAGE_1` and `INLINE_IMAGE_2`: present once in each draft

## Outbound URLs used

- OpenRouter model page: https://openrouter.ai/typesafe/jev-1.13
- Vercel AI Gateway launch note: https://vercel.com/changelog/typesafe-ai-jev-now-available-on-ai-gateway
- Vercel TypeSafe client and HTTP API note: https://vercel.com/changelog/ai-gateway-now-supports-typesafe-clients-and-http-api-for-jev
- Cloudflare Workers AI model documentation: https://developers.cloudflare.com/ai/models/typesafe/jev/
- TanStack AI Evaluate documentation: https://tanstack.com/ai/latest/docs/evaluate/evaluate
- LitJev: https://github.com/zhengxuyu/LitJev
- openjev: https://github.com/daseinlabs/open-jev
- Kev: https://github.com/jaredpalmer/kev
- NanoJev: https://github.com/TianyuCodings/NanoJev

Primary-source pages and current repository README/model-card material were checked on 26 September 2026. No GitHub star totals appear in either draft.

## Internal links

English:

- Hub: https://www.oguzhan.co/typesafe-jev-system-one-decision-model/
- Day 1, primitives: https://www.oguzhan.co/jev-primitives-choice-score-noul/
- Day 3, speed and cost: https://www.oguzhan.co/jev-speed-cost-parallel-sampler/
- Day 4, guardrails: https://www.oguzhan.co/jev-agent-guardrails-schema-valid-not-safe/
- Day 6, real-time demos: https://www.oguzhan.co/jev-realtime-doom-wikiracing-browser/

Turkish:

- Hub: https://www.oguzhan.co/tr/typesafe-jev-system-one-karar-modeli/
- Day 1, primitive'ler: https://www.oguzhan.co/tr/jev-primitives-choice-score-noul-karar/
- Day 3, hız ve maliyet: https://www.oguzhan.co/tr/jev-hiz-maliyet-paralel-ornekleyici/
- Day 4, guardrail: https://www.oguzhan.co/tr/jev-ajan-guardrail-sema-gecerli-guvenli-degil/
- Day 6, gerçek zamanlı demolar: https://www.oguzhan.co/tr/jev-gercek-zamanli-doom-wikiracing-tarayici/

## FACTS gaps and editorial cautions

- No unresolved factual gap was filled by inference.
- OpenRouter's price, context, model ID, Decisions API distinction, and displayed P50 latency were verified against its model page and tutorial material.
- Vercel's model ID, AI SDK minimum version, `experimental_evaluate`, per-request ZDR and No Training controls, TypeSafe-compatible base URL, and `/v1/evaluate` route were verified against Vercel's two changelog entries and knowledge-base guide.
- Cloudflare usage and response version were verified against its model documentation. No Cloudflare token price is quoted in the drafts; readers are directed to the dashboard.
- TanStack adapter names and credential paths were verified against its Evaluate documentation.
- LitJev, openjev, Kev, and NanoJev descriptions were checked against current repository material. Kev's 0.5B card now labels that checkpoint superseded and for research, while the repository lists newer family checkpoints. The draft preserves the required warning and notes the newer family without claiming equivalence to Jev.
- Hosted model aliases, provider policies, dashboard prices, and open-repository defaults can change after publication. Recheck before publishing or converting examples into production documentation.

## Voice and compliance checklist

- [x] English drafted first.
- [x] Turkish written as an original native draft, not line-translated.
- [x] Answer-first openings and uneven sentence rhythm.
- [x] No em dash or decorative en dash.
- [x] No banned English terms or `not only ... but also` scaffold.
- [x] No `-maktadır/-mektedir`, `günümüzde`, or `sonuç olarak`.
- [x] No `masa` calque for desktop or computer.
- [x] Turkish title uses a native Turkish thought rather than an English colon pattern.
- [x] No invented Cloudflare prices or GitHub star counts.
- [x] Kev is explicitly separated from vendor Jev and its 0.5B checkpoint is labeled as a research prototype.
- [x] Hub plus four prior-day links appear in each language.
