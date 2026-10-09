---
title: "Cloudflare Clef vs TypeSafe Jev: what the numbers do and don't show"
slug: clef-vs-jev-cloudflare-typesafe-decision-models
lang: en
polylang_pair: drafts/tr-clef-vs-jev.md
status: draft (do not publish)
format: B deep dive
hub: https://www.oguzhan.co/ai/
focus_keyphrase: "Clef vs Jev"
yoast_seo_title: "Clef vs Jev: Cloudflare's Decision Models vs TypeSafe"
yoast_meta_description: "Clef vs Jev compared: Cloudflare's open-weight decision models and TypeSafe's Jev 1.13 on price, latency claims, small independent tests and lock-in."
excerpt: "Cloudflare's Clef and Clef-flash speak Jev's API and come with open weights. What the vendors claim, what small independent tests found, and where each model fits."
featured_image: clef-vs-jev-decision-models-cover.webp
---

[[IMAGE: cover | clef-vs-jev-decision-models-cover.webp; alt: Two decision machines side by side, one sealed black box and one open glass case with gears, fed the same cards | Same input, two ways to ship a decision model: a closed hosted API and open weights you can run yourself.]]

Clef vs Jev became a real choice on 1 October 2026. That day Cloudflare released Clef and Clef-flash, two open-weight decision models that answer typed questions with probabilities instead of free text, and pitched them directly against TypeSafe's Jev, which launched on 15 September. [Cloudflare's launch post](https://blog.cloudflare.com/clef-decision-models/) describes them as fully compatible with Jev's System One API. Whether that makes them a swap is less clear.

Where I stand: this site has covered Jev a lot (the backlog is on the [AI hub](https://www.oguzhan.co/ai/)), so weigh my framing accordingly. I have not run either model. Every number below comes from vendor pages or small public tests, linked where it appears.

## What Cloudflare shipped on 1 October

Two models. Clef is 27B, post-trained from a frozen Qwen3.8-27B; Clef-flash is 9B, built on a frozen Qwen3.5-9B, according to [Cloudflare's blog](https://blog.cloudflare.com/clef-decision-models/) and the [Hugging Face card](https://huggingface.co/Cloudflare/clef). The [changelog](https://developers.cloudflare.com/changelog/post/2026-10-01-clef-workers-ai/) calls them "the first models trained by the Cloudflare Workers AI team."

The job is narrow. Clef reads a `state` plus up to 64 typed questions (`noul` for yes/no, `choice` for one option, `score` for an ordered rubric) and returns a probability for every allowed answer. No prose comes back. You call it through the Workers AI binding, the REST endpoint or AI Gateway, and both models are also on OpenRouter.

## How Clef and Jev work under the hood

[[IMAGE: inline-1 | decision-model-state-questions-diagram.webp; alt: Diagram: state plus choice, score and noul questions go into a decision model and come out as probability bars | Jev and Clef take the same request shape: a state, typed questions, and a probability for every allowed answer.]]

The request shape is shared. Only one side documents what sits behind it.

According to Cloudflare's blog, Clef's Qwen backbone does a single prefill pass and a small "joint schema head" scores every valid option in parallel, so nothing is generated token by token. Training mixed label-smoothed cross-entropy with a Brier loss for calibration and added "Reinforcement Learning for Calibrated Decisions (RLCD)" as a secondary objective. RLCD is also the name [TypeSafe's launch post](https://typesafe.ai/blog/introducing-system-one-models-and-jev) gives Jev's training method.

Jev's architecture is not public; [The Register](https://www.theregister.com/ai-and-ml/2026/10/01/cloudflare-tries-to-outplay-jev-with-open-weight-clef-models/5300649) wrote that "TypeSafe has kept that a secret." TypeSafe says Jev "can't hallucinate" in one narrow sense: the output schema is guaranteed, so no type errors.

Inputs differ more than the API suggests. [TypeSafe's docs](https://docs.typesafe.ai/models) list Jev as text only. Clef has a vision encoder, and the [Workers AI model page](https://developers.cloudflare.com/workers-ai/models/clef/) allows up to 4 images per request. The model card also mentions video, but the Workers AI parameter docs only list images, so I'd treat video as a property of the open weights for now. Both have 64K context; TypeSafe reserves 32k of it for `state` plus the longest question, and says languages other than English are "handled but not equally well."

## Open weights, hosted API and lock-in

[[IMAGE: inline-2 | hosted-vs-self-hosted-fork.webp; alt: A circuit-trace road splits toward a locked cloud building and toward a small server rack with an open padlock | Jev is only available as a hosted API. Clef runs on Workers AI or on your own GPUs, if you have about 85 GB of VRAM for the 27B model.]]

This is the clearest difference.

Jev's weights are closed. TypeSafe's docs say every account gets the same weights, with no fine-tuning or LoRA on customer data. The service is "currently based" on the US West Coast and is also reachable through OpenRouter, Vercel AI Gateway and Workers AI, as I covered in the [Jev ecosystem post](https://www.oguzhan.co/jev-ecosystem-openrouter-vercel-cloudflare/). TypeSafe says it doesn't train on customer data and offers zero data retention for enterprise.

Clef's weights are on Hugging Face under Apache-2.0. The training data is not. Michelle Chen of Cloudflare confirmed that to The Register, and the [Hacker News thread](https://news.ycombinator.com/item?id=49923692) was retitled "open-weight" after comments like "Open weights, not open source."

Self-hosting is real but heavy: per Chen, Clef-flash needs at least 41 GB of VRAM and Clef 85 GB, at single concurrency with 64k context. Cloudflare also offers RL fine-tuning, starting hands-on through its forward-deployed engineers and design partners before going self-serve. Jev has nothing equivalent.

My read: Jev ties you to one vendor's API. Clef can tie you to Cloudflare too, but you can leave with the weights.

## What does Clef cost compared with Jev?

[Workers AI pricing](https://developers.cloudflare.com/workers-ai/platform/pricing/) lists Clef at $0.24 per million input tokens and Clef-flash at $0.09, with no output price. TypeSafe's docs list Jev at $0.042, with output free. The Register called Clef "nearly six times" Jev's price; Clef-flash is a little over twice.

The independent per-decision figures point the same way. [Startrise](https://www.startrise.io/blog/jev-vs-clef/) put Clef at about $63 per million decisions against about $17 for Jev. [Construct](https://construct.computer/blog/clef-vs-jev-benchmark/) got $23 for Jev, $35 for Clef-flash and $93 for Clef.

One caveat sits on Jev's side: TypeSafe's launch post admits it "can't prove it isn't subsidized." Its docs also give rate limits of 100K tokens and 80 requests per second, "adjusting dynamically" and changeable without notice. More on Jev's pricing in the [speed and cost post](https://www.oguzhan.co/jev-speed-cost-parallel-sampler/).

## Clef vs Jev at a glance

| | TypeSafe Jev 1.13 | Cloudflare Clef | Cloudflare Clef-flash |
|---|---|---|---|
| Released | 15 Sep 2026 (early access) | 1 Oct 2026 | 1 Oct 2026 |
| Weights | Closed | Open, Apache-2.0 | Open, Apache-2.0 |
| Size / base | Not published | 27B, Qwen3.8-27B | 9B, Qwen3.5-9B |
| API | System One | System One compatible (per Cloudflare) | Same |
| Input | Text only | Text, JSON, up to 4 images | Same |
| Context | 64k (32k state + longest question) | 64K | 64K |
| Price per M input tokens | $0.042 | $0.24 | $0.09 |
| Output tokens | Free | No charge listed | No charge listed |
| Hosting | TypeSafe API, OpenRouter, Vercel, Workers AI | Workers AI, OpenRouter, self-host (~85 GB VRAM) | Workers AI, OpenRouter, self-host (~41 GB VRAM) |
| Fine-tuning | Not offered | RL fine-tuning (design partners) | Same |
| Vendor latency claim | 70 to 500 ms (TypeSafe) | 209.3 ms median (Cloudflare) | 38.8 ms median (Cloudflare) |

Read the last row carefully. The next section explains why.

## Cloudflare's numbers vs independent tests

[[IMAGE: inline-3 | vendor-benchmarks-vs-independent-tests.webp; alt: A spotlit trophy bar chart on a stage next to small notebooks, stopwatches and question marks with mixed results | Cloudflare's tables are self-reported. Small independent tests from Startrise, Construct and others came back mixed.]]

According to the changelog, median latency across 43 runs was 209.3 ms for Clef, 38.8 ms for Clef-flash and 524.1 ms for Jev, which Cloudflare sums up as Clef "2.5x faster" and Clef-flash "13x faster." Those figures are not like-for-like. [Flavio Copes](https://flaviocopes.com/clef/), citing the leaderboard's methodology notes, says Clef was timed on Cloudflare's own serving stack, while Jev's 524 ms is a round trip over the internet from Cloudflare's lab to TypeSafe's API. TypeSafe quotes about 100 ms for most calls from the US West Coast.

On accuracy, Cloudflare says a Clef model "scores highest on 7" of 10 decision benchmarks, for example BANKING77 macro-F1 at 94.20 for Clef against 79.74 for Jev. The full model card is more mixed. Jev leads clearly on reasoning-heavy rows: GPQA Diamond 78.3 vs 48.0, MMLU-Pro 82.7 vs 65.9. On TypeSafe's workflow evals, a Clef model leads in three of four areas by 3 points or less, and Jev takes the fourth. The Register notes the scores are self-reported and "have yet to be reproduced" on the official Decision Index.

Tests that crossed the internet for every model looked different:

- **Startrise**, 10 tasks and 168 decisions per model: agreement with AI-reviewed references was 89.2% for Jev, 89.8% for Clef, 82.6% for Clef-flash. Per decision, Jev took 320 ms, Clef-flash 316 ms, Clef 655 ms.
- **Construct**, 117 labelled synthetic cases: drop-in accuracy 92.3% for Clef, 88.6% for Jev, 82.1% for Clef-flash, a gap it calls "not statistically significant." Laptop medians were 454, 449 and 654 ms for Jev, Clef-flash and Clef.
- **[DEV Community](https://dev.to/therabbithole/cloudflare-just-shipped-two-decision-models-i-raced-them-against-jev-on-openrouter-3fdm)**, sets of 40, 30 and 12 items: accuracy roughly tied, Jev fastest on every task, and one HTTP 429 "Capacity temporarily exceeded" from Clef per task.

[Hacker News](https://news.ycombinator.com/item?id=49923692) and [X](https://x.com/search?q=Clef%20Jev) anecdotes split both ways, from a moderation pipeline called "2-3x slower and worse" on Clef to a 1,000-question run with Clef-Flash at 88.0% and Jev at 88.5%.

### Small samples, and everyone has a stake

Every test above is small and ran within days of launch. Startrise's own caveat: "These small pilots do not establish general accuracy." Startrise is also a consultancy selling related services, and Construct runs on Cloudflare. Cloudflare benchmarked itself against a rival's hosted API. TypeSafe publishes no public Jev benchmarks, per Copes, and says of its own "193.6x faster" eval figures that "some bias could exist."

TypeSafe founder Diogo Almeida replied on X, [as GIGAZINE reported](https://gigazine.net/gsc_news/en/20261005-clef-cloudflare-decision-model/), that "there's a critical difference between benchmaxxed models and ones made by people who truly care about reliability." On a [daily.dev podcast](https://daily.dev/posts/jev-system-one-models-for-prod-not-god-with-diogo-almeida-ceo-typesafe-ai-1c6lthxm7) he called public benchmarks "extremely gameable." Fair, though it also leaves Jev's reliability claims hard to check from outside.

## Is Clef really a drop-in replacement for Jev?

[[IMAGE: inline-4 | threshold-dial-two-models.webp; alt: Two gauges read the same input card at slightly different needle positions above a 0 to 1 threshold slider | Same API, different numbers. Construct found thresholds tuned on Jev did not carry over to Clef without retuning.]]

For the API, mostly. For your decisions, not without retesting.

Construct's clearest finding: thresholds don't transfer. A cut-off tuned on Jev's probabilities doesn't fit Clef's. With per-model thresholds, all three landed between 90.6% and 93.2%.

Confidence also behaves differently. Startrise saw Jev average 0.86 when right and 0.69 when wrong; Clef was 0.94 and 0.84, a narrower gap. The DEV test found Jev at 0.99 vs 0.71 and Clef at 0.81 vs 0.74. If low-confidence cases go to a human in your pipeline, retest that routing. (Background in my [RLCD and confidence post](https://www.oguzhan.co/jev-confidence-rlcd-calibrated-decisions/).)

Repeatability cuts the other way. Construct got identical probabilities from Clef and Clef-flash on all 351 repeat calls each. Jev's acted-on probability moved by up to 0.10, two cases flipped, and its calibration probes shifted between 20 September and 4 October under the same `jev-1.13.0`.

One unverified flag: the DEV post relays an OpenRouter note that Workers AI reads only about the first 2K tokens of a long text `state`. Cloudflare's docs only say long text is "truncated to fit the model's token limit."

## Maturity and version drift

Both are young. Jev is in early access at 1.13, with `jev-latest` and `jev-preview` both pointing to `1.13.0`. Clef isn't labelled beta, but Cloudflare's blog says "We're still early here."

[InfoQ](https://www.infoq.com/news/2026/10/typesafe-ai-jev-released/) reports that TypeSafe's "jaggedness" page lists unreliable counting, arithmetic and date comparison, and advises keeping maths in code and pinning versions. Candid, and a list of real gaps.

## Honest limits of both

**Jev:** closed weights, undisclosed architecture, no fine-tuning; text only; hosted on the US West Coast; dynamic rate limits; documented jaggedness; drift under a fixed version name, per Construct; no public benchmarks.

**Clef and Clef-flash:** list price nearly six times Jev's (Clef) or about twice (Clef-flash); self-reported benchmarks; a headline latency gap that internet-path tests didn't reproduce; 429 capacity errors in one test; behind Jev on reasoning-heavy rows of Cloudflare's own card; open weights but closed training data; 41 to 85 GB of VRAM to self-host.

## When to pick which

No crown. These are starting points for your own eval.

- **Text-only, high-volume decisions:** Jev has the lowest list price and came out cheapest per decision in both cost tests. Accuracy was close, so price and drift tolerance decide.
- **Images in the state:** Clef or Clef-flash. Jev takes text only.
- **Self-hosting, data residency, strict version pinning:** Clef's Apache-2.0 weights let you freeze a model and run it where you choose, GPUs permitting. Jev keeps you on TypeSafe's hosted service.
- **Fine-tuning on your own decisions:** Clef, through a program still at the design-partner stage. Jev is shaped through state and criteria only.
- **Already on Cloudflare Workers:** both run on Workers AI (Jev as `typesafe/jev`), so test them side by side there.
- **Latency-critical hot path:** measure from where your code runs. Cloudflare's on-network numbers favor Clef-flash; Startrise and Construct had Jev and Clef-flash close, with Clef slowest.
- **Reasoning-heavy questions:** Cloudflare's own card has Jev ahead on GPQA Diamond and MMLU-Pro. With either, keep arithmetic and dates in code.

My take: Clef gives Jev users an exit, plus image input. Jev still looks cheaper on text. Neither has evidence strong enough to skip testing on your own workload.

## Sources

- Cloudflare blog, "Introducing Clef" (2026-10-01): https://blog.cloudflare.com/clef-decision-models/
- Cloudflare changelog (2026-10-01): https://developers.cloudflare.com/changelog/post/2026-10-01-clef-workers-ai/
- Workers AI model page, Clef: https://developers.cloudflare.com/workers-ai/models/clef/
- Workers AI pricing (updated 2026-10-01): https://developers.cloudflare.com/workers-ai/platform/pricing/
- Hugging Face model card, Cloudflare/clef: https://huggingface.co/Cloudflare/clef
- The Register (2026-10-01): https://www.theregister.com/ai-and-ml/2026/10/01/cloudflare-tries-to-outplay-jev-with-open-weight-clef-models/5300649
- Hacker News thread: https://news.ycombinator.com/item?id=49923692
- Startrise (2026-10-06): https://www.startrise.io/blog/jev-vs-clef/
- Construct (2026-10-05): https://construct.computer/blog/clef-vs-jev-benchmark/
- DEV Community, TheRabbitHole (2026-10-08): https://dev.to/therabbithole/cloudflare-just-shipped-two-decision-models-i-raced-them-against-jev-on-openrouter-3fdm
- Flavio Copes, Clef deep dive: https://flaviocopes.com/clef/
- GIGAZINE (2026-10-05): https://gigazine.net/gsc_news/en/20261005-clef-cloudflare-decision-model/
- daily.dev podcast summary with Diogo Almeida: https://daily.dev/posts/jev-system-one-models-for-prod-not-god-with-diogo-almeida-ceo-typesafe-ai-1c6lthxm7
- TypeSafe launch post (2026-09-15): https://typesafe.ai/blog/introducing-system-one-models-and-jev
- TypeSafe docs, Models: https://docs.typesafe.ai/models
- InfoQ (Oct 2026): https://www.infoq.com/news/2026/10/typesafe-ai-jev-released/
- X posts, 3 to 8 Oct 2026 (@Lonely__MH, @samsillva, @_mantaroh_): https://x.com/search?q=Clef%20Jev
