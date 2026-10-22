# Notes for the 22 Oct 2026 digest

Word counts are whitespace-separated tokens in the markdown body after the YAML frontmatter. A URL counts as one token. Spaced table pipes count as tokens. HTML comments count.

## Word counts

- EN body: 1100
- TR body: 950

Section tokens, headings included:

| Section | EN | TR |
|---|---|---|
| Opener | 61 | 59 |
| Story 1 DeepInfer | 293 | 245 |
| Story 2 EAGLE-4 | 239 | 199 |
| Story 3 Muse Glimmer | 281 | 252 |
| Story 4 Viggle plus closing | 183 | 152 |
| Sources | 43 | 43 |

Story 3 includes the benchmark table (about 50 tokens). The prose lead is still Story 1. Both files sit at the top of the requested ranges because the table and the sources list are inside the body count.

## Internal links

EN:

- 19 Oct digest, Story 1: https://www.oguzhan.co/openai-misalignment-reports-claude-ecdsa-seeds/
- 15 Oct digest, Story 3: https://www.oguzhan.co/muse-wonder-gemini-4-argon-frontier-agents/
- Frontier-model explainer, Story 3, on Muse Spark: https://www.oguzhan.co/what-is-a-frontier-model/

TR, same placement, /tr/ URLs:

- https://www.oguzhan.co/tr/openai-misalignment-raporlari-claude-ecdsa-tohumlari/
- https://www.oguzhan.co/tr/muse-wonder-gemini-4-argon-frontier-ajanlar/
- https://www.oguzhan.co/tr/frontier-model-ne-demek/

Not used: MiniMax M3.1 Flash (optional, would rehash the 21 Oct dive) and the AI hub.

## Left out or compressed

- X engagement was optional in the brief (about 41.7K likes and 6.3M views on the morning of 22 Oct). Left out.
- No tok/s figure for Muse Glimmer. The brief says the report does not give one.
- Acronyms are not expanded. The brief does not define EPLB, SWA, EP64, DP, CP, MTP, TP4, or SM100.
- "valley pricing" stays in quotation marks in EN. TR renders it literally as "vadi fiyatında". The brief does not say whether that label means off-peak. No extra definition was added.
- The vLLM engine note is paraphrased. The brief joins "derived from vLLM" and "modified by DeepSeek" with a semicolon, which these drafts cannot use, so the sentence states both facts with "and".
- Eagle's 2.74x and 1.69x stay in the brief's order, next to the single-request figure and then the 512-request figure. The brief does not add a separate column label for each multiplier.
- "Up to 64 input views as spatial context" is "Up to 64 input views" in EN and "Mekânsal girdi 64 görüntüye kadar" in TR.
- Third-party API behavior is carried by "fully aligned with the official DeepSeek API" and, in TR, "resmi API ile hizalı". A second sentence spelling out the third-party match was not added.
- TR does not keep the English license label Competing Offering. It is "rakip ürün kullanımı" with a license that does not depend on revenue.
- TR renders "physics-native world foundation model" as "fiziği içinden kurulmuş bir dünya temel modeli".
- English lines from DeepSeek, Eagle, and Meta are in Turkish in the TR file, with attribution. The open-source claim is "artık tamamen açık kaynak".
- The closing does not add a second sentence about a louder model headline. The opinion that is kept: the price cut to watch is in the serving layer, and EAGLE-4's license line belongs beside the benchmark chart.
- Nothing was installed, run, or benchmarked. Every speed, price, and score is a vendor claim, attributed next to the figure.

## Facts held on purpose

- DeepInfer's open-source drop is offline inference. No KV cache system, no prefill/decode disaggregation, no load balancing across replicas, no online-serving wrapper.
- EAGLE-4 is source-available, not OSI-approved open source. Commercial use is under US$20 million aggregate revenue over 12 months. A competing offering needs its own license at any revenue.
- Muse Glimmer weights are dated August 2026 on the model card. The new document is the technical report.
- Jev, TypeSafe, export controls, and US politics are not mentioned.
