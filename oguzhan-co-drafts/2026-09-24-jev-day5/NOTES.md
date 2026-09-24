# Jev Day 5 Drafting Notes

## Word Counts
- **EN**: 1117 words (target: 900-1400) ✓
- **TR**: 985 words (target: 800-1200) ✓

## Outbound URLs Used

### Primary Sources (from research.md)
1. https://github.com/cobanov/awesome-jev
2. https://github.com/tamaratran/fast-jev-compaction
3. https://github.com/leonaaardob/fast-dev-compaction
4. https://github.com/GhalebDweikat/winnow
5. https://github.com/compozy/yoshi
6. https://aiskill.market/blog/context-gc-fast-jev-compaction-winnow
7. https://typesafe.ai/blog/introducing-system-one-models-and-jev

All primary repos covered as requested.

## Internal URLs Used

### Hub Links
- EN: https://www.oguzhan.co/typesafe-jev-system-one-decision-model/
- TR: https://www.oguzhan.co/tr/typesafe-jev-system-one-karar-modeli/

### Day 4 Links
- EN: https://www.oguzhan.co/jev-agent-guardrails-schema-valid-not-safe/
- TR: https://www.oguzhan.co/tr/jev-ajan-guardrail-sema-gecerli-guvenli-degil/

All required internal cross-links included.

## Image Placeholders
Both drafts include two inline image placeholders as requested:
1. `<!-- INLINE_IMAGE_1: prune-tiers diagram -->`
2. `<!-- INLINE_IMAGE_2: admit-vs-compact contrast -->`

## FACTS Gaps (Deliberately Not Filled)
None. All claims sourced from research.md:
- Fast-jev-compaction defaults (keepThreshold 0.5, truncateHeadChars 300, preserveRecentMessages 6, maxStateTokens 25k, maxRequestTokens 30k)
- Fast-dev-compaction author warning and Theo critique
- Winnow thresholds (DROP 0.1, KEEP 0.5), block size (~25 lines), 5% self-reported clean hidden under 0.1 on 97/300 hand labels
- Yoshi candid POC status: v12 slower than baseline, Fable ~34% reduction, Sonnet ~0% savings, incomplete Jev receipts

## Voice Compliance

### EN (anti-slop)
- No em dashes (—)
- Burstiness maintained (short punches: "A probability is not proof." "Pins are simple." next to longer explanatory sentences)
- Specific nouns: tamaratran, leonaaardob, GhalebDweikat, compozy, t3.gg, Theo, 0.5, 300, 25,000, 30,000, 0.1, 5%, 34%, 0%
- No banned patterns (delve/tapestry/robust/leverage/underscore/pivotal/testament)
- No "In this article" opener
- Answer-first H2 opener
- First-person avoided (deep dive register, not digest)

### TR (Dünya Halleri register)
- No line-by-line translation from EN
- ORIGINAL Turkish structure and flow
- English tech terms kept: Jev, Noul, Claude Code, Codex, TypeSafe, compaction, stub, recall, System One, fast-jev-compaction, Winnow, Yoshi, POC
- No em dashes
- No brochure Turkish (-mektedir, günümüzde, sonuç olarak, devrim niteliğinde, oyun değiştirici)
- No calques (no "masa" for desktop/desk)
- Concrete facts with numbers: 0,5 / 0,1 / 300 / 25 bin / 30 bin / %5 / %34 / %0
- Natural Turkish flow: "Kod o puanı eşikle karşılaştırır" not "Kod o skorla eşik arasında karşılaştırma yapar"

## Deferred Topics (per research.md)
- Browser demos (jev-ultrafast) → Day 6-7
- LitJev/openjev/kev/NanoJev ecosystem → Day 6-7
- OpenRouter/Vercel/CF integration → Day 6-7
- Pi ports (pi-fast-jev-compaction, pi-jev-compact) → optional peers, not featured
- LiteLLM relevance guardrail → optional peer, not featured
- Day 1-3 deep dives (Choice/Score/Noul tutorial, RLCD/jaggedness, latency/price Pareto) → one-line reminders only

## Structure Delivered
✓ Answer-first H2 opener (2-4 citation-ready sentences)
✓ Explain pruning pattern (ask → threshold → act)
✓ Walk four tools: fast-jev-compaction, fast-dev-compaction, Winnow, Yoshi
✓ Close: what Jev selects vs what code must keep; recovery paths
✓ YAML frontmatter (both langs)
✓ No date in H1/title
✓ No invented stars/savings%/latency/certifications

## Suggested Slug Refinement Used
- EN: `jev-context-compaction-verbatim-prune` (as suggested)
- TR: `jev-context-compaction-aynen-budama` (as suggested)

Both focus keyphrases align with suggestion.
