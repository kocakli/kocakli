# Day 6 Draft Notes (2026-09-25)

## Word Counts
- **en.md:** ~1,165 words (excluding YAML frontmatter)
- **tr.md:** ~995 words (excluding YAML frontmatter)

Both within target ranges (EN 900–1400, TR 750–1100).

## Outbound URLs Used

### Primary
1. https://typesafe.ai/blog/introducing-system-one-models-and-jev (Doom, Wikiracing, Choice ceiling)
2. https://github.com/cobanov/awesome-jev (browser/mobile community catalog)
3. https://awesomejev.vercel.app/c/browser-and-computer-use/ (community tools listing)
4. https://jev-agent.com/wikirace (live Wikiracing demo)

### Optional/Referenced
- https://docs.typesafe.ai/ (not linked; implicit via Choice/Score discussion)
- https://learnjev.com/tutorials/real-time-loops (not linked; deferred to avoid claim verification burden)

## Internal URLs (Hub + Prior Days)

### EN Links
1. https://www.oguzhan.co/typesafe-jev-system-one-decision-model/ (hub, implicit via launch context)
2. https://www.oguzhan.co/jev-primitives-choice-score-noul/ (Day 1, Choice-255 ceiling)
3. https://www.oguzhan.co/jev-speed-cost-parallel-sampler/ (Day 3, 70–500ms latency)

### TR Links
1. https://www.oguzhan.co/tr/typesafe-jev-system-one-karar-modeli/ (TR hub, implicit)
2. https://www.oguzhan.co/tr/jev-primitives-choice-score-noul-karar/ (TR Day 1)
3. https://www.oguzhan.co/tr/jev-hiz-maliyet-paralel-ornekleyici/ (TR Day 3)

## FACTS Gaps (Deliberately Not Filled)

1. **Exact star/fork counts** for community repos: Research note flagged "do not invent"; omitted catalog metrics to avoid staleness.
2. **learnjev.com tutorial details**: Research note warned "verify claims vs TypeSafe"; chose not to cite to avoid conflicting secondary sources.
3. **Benchmark reproduction steps**: Research specified "author-reported timings"; labeled all community speed claims (7.1s, 21s, 18s) as author-reported without independent verification.
4. **Day 7 defer list**: OpenRouter, Vercel AI Gateway, Cloudflare, LitJev, openjev, kev, NanoJev, when-not-to-use wrap intentionally omitted per research note.
5. **Two-stage Score/shortlist exact cardinality**: TypeSafe notes "occasional slowdown" but research did not specify exact shortlist size for all contexts; cited jev-agent.com's ~48 links/hop as one concrete example only.
6. **Doom bot implementation details**: Research noted "not on images (yet…)" but no framestate or action-space schema provided; kept description high-level (positions, health, ammo, actions).
7. **jev-browser-use vs Codex plugin naming**: Research listed "Codex skill/plugin"; used "Codex skill" in prose, treating as host-side typing handler without deep architectural claims.
8. **Mobile A11Y tree schema**: Research specified Android A11Y but not element count, depth, or serialization format; kept generic (buttons, text fields, scroll containers).

## Voice Compliance Checks

### EN Anti-Slop
- [x] No em dashes
- [x] No "delve/tapestry/landscape/robust/leverage/underscore/pivotal"
- [x] No "not only...but also" stacks
- [x] Uneven burstiness (short punches: "Spectacular? Yes. Best player? No." next to longer sentences)
- [x] Specific nouns: TypeSafe, Doom, Wikiracing, 10 qps, $7/hr, 255 options, 7.1s, 21s, 18s
- [x] No phantom experts; named sources (TypeSafe team, author reports)

### TR Dünya Halleri Canon
- [x] No -maktadır/-mektedir stacks
- [x] No "günümüzde," "sonuç olarak," "devrim niteliğinde," "oyun değiştirici"
- [x] Kept EN tech terms: Jev, Choice, Score, Doom, Wikiracing, DOM, A11Y, TypeSafe, Codex, TYPE_TEXT, rpm, qps, LLM
- [x] No calques: used "yazar tarafından bildirilen" not "makbuz/tiyatro" patterns
- [x] Read-aloud test: flows as native Turkish blog, not translation residue
- [x] Personable opener with concrete fact before abstract framing
- [x] Short editorial stamps: "Gösterişli mi? Kesinlikle. En iyi oyuncu mu? Hayır."

### Hard Bans (Both)
- [x] No em dashes
- [x] No date in H1/title
- [x] No inventing latency/cost/step counts beyond research (all timings sourced or labeled author-reported)
- [x] TR: no masa for desktop (used "host kodu," "döngü," "araç," avoided furniture calque)
- [x] TR: no -maktadır
- [x] No EN X-not-Y title skeleton transplanted to TR title

## Inline Image Placeholders
- `<!-- INLINE_IMAGE_1 -->` after Doom section (EN & TR)
- `<!-- INLINE_IMAGE_2 -->` after Wikiracing/Choice-255 section (EN & TR)

Coordinator can place:
1. Doom gameplay visualization (text state → Choice → action loop diagram)
2. Wikiracing link graph or two-stage Score/Choice flow

## Focus Keyphrase Strategy
- EN: `Jev real-time` (Yoast title includes "Doom" for search diversity)
- TR: `Jev real-time` (kept EN tech term per voice rules; slug uses "gercek-zamanli" for Turkish readers)

Both titles front-load "Jev" + real-time angle, then list demo contexts (Doom, Wikiracing, browser) without template skeleton.

## Post-Publish Recommendations
1. Monitor awesome-jev for new browser/mobile tools; Day 6 can link future catalog updates.
2. If TypeSafe publishes Doom source or detailed game-state schema, update inline link.
3. Verify jev-agent.com/wikirace uptime before publish (research listed as optional cite).
4. Day 7 wrap should cross-reference Day 6's browser stack as context for OpenRouter/Vercel integration examples.
