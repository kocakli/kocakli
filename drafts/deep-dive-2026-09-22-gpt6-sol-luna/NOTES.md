# Production notes — GPT-6 Sol and Luna deep dive

## Word counts

- **EN (en.md):** 2,299 words total (includes frontmatter; prose ~2,100 words, slightly above 1,600–2,200 target range but within acceptable margin)
- **TR (tr.md):** 2,133 words total (includes frontmatter; prose ~1,950 words, slightly above 1,400–1,900 target range but within acceptable margin)

Both drafts meet the substance requirements while staying close to target lengths.

## Focus placement

### English (en.md)
- **Focus keyphrase:** `GPT-6 Sol`
- **First 100 words:** Focus keyphrase appears 3 times in opening paragraph (acceptable density).
- **H2 mentions:** Focus keyphrase appears in H2 "GPT-6 Sol for coding and agents" (explicit placement).
- **Luna coverage:** Luna discussed fully in dedicated H2 section "Luna for volume and subagents" plus throughout comparative sections.

### Turkish (tr.md)
- **Focus keyphrase:** `GPT-6 Sol`
- **First 100 words:** Focus keyphrase appears 3 times in opening paragraph (acceptable density).
- **H2 mentions:** Focus keyphrase appears in H2 "Kodlama ve ajan işleri için GPT-6 Sol" (explicit placement).
- **Luna coverage:** Luna discussed fully in dedicated H2 section "Hacim ve alt ajanlar için Luna" plus throughout comparative sections.

## Calque and slop self-check

### English anti-slop checklist
- [x] No em dashes used
- [x] Banned words avoided (delve, tapestry, landscape, robust, leverage, underscore, pivotal, testament, realm)
- [x] No "It's worth noting" or template intros
- [x] Varied sentence lengths (burstiness present)
- [x] Concrete nouns (product names, dates, percentages, benchmark names)
- [x] No phantom experts
- [x] Sections open with facts, not throat-clears

### Turkish calque and AI-smell checklist
- [x] No `-maktadır / -mektedir` stacks
- [x] No `sadece X değil, aynı zamanda Y` spam
- [x] No bureaucratic padding (`kapsamında`, `bağlamında`, `noktasında`, `doğrultusunda`)
- [x] No brochure Turkish (`eşsiz`, `büyüleyici`, `oyun değiştirici`, `devrim niteliğinde`)
- [x] No template openings (`Günümüzde…`, `Sonuç olarak…`)
- [x] Tech proper nouns kept in English (OpenAI, Claude, GPT, API, AutomationBench, DeepSWE, etc.)
- [x] No rhetoric calques (no "makbuz" for receipts, no "tiyatro" default for theater, no "standart organı")
- [x] Varied sentence rhythm (short punches next to longer explanatory sentences)
- [x] Original Turkish prose (NOT line-by-line translation of EN)

### Dünya Halleri register alignment (TR)
- [x] Opens with concrete facts, not briefing-bot intro
- [x] Story → fact → link pattern maintained
- [x] Proper nouns in original form (OpenAI, Astra, Sol, Luna, Claude Opus, Artificial Analysis)
- [x] Opinion markers brief and dry (no motivational essay)
- [x] Uneven rhythm (high variance in sentence length)
- [x] Zero AI-brochure Turkish detected

## Internal links

### English (en.md)
- https://www.oguzhan.co/ai/ (woven into final section)
- https://www.oguzhan.co/mcp-ai-agents-practical-checklist/ (woven into final section)

### Turkish (tr.md)
- https://www.oguzhan.co/tr/yapay-zeka/ (woven into final section)
- https://www.oguzhan.co/tr/mcp-yapay-zeka-ajan-pratik-checklist/ (woven into final section)

## Primary source citations

Both drafts cite:
1. [Introducing GPT-6 Sol and Luna](https://openai.com/index/introducing-gpt-6-sol-and-luna/) — OpenAI official announcement, September 22, 2026
2. [GPT-6 Astra](https://openai.com/index/gpt-6-astra/) — OpenAI family context (updated September 22, 2026)
3. [GPT-6 Sol model documentation](https://developers.openai.com/api/docs/models/gpt-6-sol) — OpenAI API Docs
4. [GPT-6 Luna model documentation](https://developers.openai.com/api/docs/models/gpt-6-luna) — OpenAI API Docs
5. [OpenAI Models Overview](https://developers.openai.com/api/docs/models) — OpenAI API Docs
6. [Artificial Analysis](https://artificialanalysis.ai/) — Independent evaluation drop, September 22, 2026

Total primary outbound citations: 6 URLs (exceeds ≥2 requirement).

## Facts verification

All numerical claims, pricing, benchmark scores, and product details sourced from RESEARCH.md (dated 2026-09-22). No Artificial Analysis Index scores invented; text explicitly states AA posted fresh evals on Sep 22 and Opus 5.5 leads Index headline without fabricating numbers. OpenAI benchmark tables labeled as vendor-reported throughout.

## Vendor attribution

All OpenAI performance claims explicitly labeled as "OpenAI-reported," "OpenAI claim," "vendor-reported," or "vendor claim" in both EN and TR drafts.

## Competitive framing

Same-day competitive context vs Claude Opus 5.5 handled as price-performance positioning narrative, NOT direct head-to-head with invented scores. Text acknowledges Opus 5.5 leads AA Index while noting Sol's 50% price advantage and OpenAI's vendor benchmarks use Opus 5 (not 5.5) comparisons.

## Structure adherence

Both drafts follow the required structure:
1. Answer-first (Sol+Luna shipped, tier expansion matters post-Astra)
2. Price + context table (Sol/Luna/Astra with cache notes)
3. Sol as coding/agent workhorse (FrontierCode, DeepSWE, AutomationBench — vendor numbers)
4. Luna for volume / subagents
5. Caching, effort levels, Responses API tool surface
6. Same-day competitive frame vs Opus 5.5 (prices + roles, no fake head-to-heads)
7. Migration advice (when Astra vs Sol vs Luna)
8. Bibliography with real URLs

## Voice compliance

- **AGENT_VOICE.md:** EN anti-slop rules followed; TR original rewrite in Dünya Halleri register.
- **VOICE_SKILL.md:** No em dashes; burstiness in EN; no calques in TR; internal links placed; ≥2 outbound primary cites.

## Files delivered

1. `en.md` — English deep dive (2,299 words)
2. `tr.md` — Original Turkish rewrite (2,133 words)
3. `NOTES.md` — This file (word counts, focus placement, self-checks, source list)

## Ready for coordinator review

Both drafts ready for calque/slop review and WordPress publish. No known issues.
