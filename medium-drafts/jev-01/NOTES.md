# NOTES: Medium Part 1 (Jev intro)

## Word count
Body (excluding title, subtitle, tags, series line): 1,247 words

## Sources per claim

### TypeSafe System One launch date and team background
- **Claim:** "On September 15, 2026, TypeSafe launched System One, a decision model trained for two years in stealth by ex-OpenAI researchers."
- **Source:** typesafe.ai/blog/introducing-system-one-models-and-jev (cited in brief as "15 Sep 2026, Diogo Almeida")

### Core value proposition
- **Claim:** "unstructured state in, typed probabilistic decisions out"
- **Source:** typesafe.ai/blog/introducing-system-one-models-and-jev (quoted verbatim from brief: "frontier-intelligence function call: unstructured state in, typed probabilistic decisions out")

### Primitives (Choice, Score, Noul)
- **Claim:** Choice, Score, Noul definitions and structure (choice/probabilities/confidence, score/legend/probabilities/confidence, noul 0-1 with no confidence)
- **Source:** docs.typesafe.ai/primitives (cited in brief with field details)
- **Link:** https://www.oguzhan.co/jev-primitives-choice-score-noul/ (oguzhan.co reference post)

### Python SDK example
- **Code snippet:** TypeSafeClient.system_one structure
- **Source:** docs.typesafe.ai/primitives (brief notes "Python SDK example (TypeSafeClient.system_one)")

### Latency figures
- **Claim:** "70 to 500 milliseconds per decision versus 3 to 329 seconds for frontier chat models"
- **Source:** typesafe.ai/blog/introducing-system-one-models-and-jev (brief: "70-500 ms vs 3-329 s for frontier models (TypeSafe's table; evals run from West Coast)")
- **Link:** https://www.oguzhan.co/jev-speed-cost-parallel-sampler/ (oguzhan.co reference post)

### Cost
- **Claim:** "$0.042 per million tokens. Output is free"
- **Source:** typesafe.ai/blog/introducing-system-one-models-and-jev (brief: "$0.042/MTok input, output free")

### Performance multipliers
- **Claim:** "193.6x to 444.6x faster on the higher end of their tested scenarios"
- **Source:** typesafe.ai/blog/introducing-system-one-models-and-jev (brief: "193.6x/444.6x = TypeSafe workflow evals, 'higher end'")

### Batching efficiency
- **Claim:** "Batching 13 questions in one call is 11.5x cheaper and 9.6x faster"
- **Source:** docs.typesafe.ai/primitives (brief: "13 questions batched 11.5x cheaper, 9.6x faster")

### Doom agent cost
- **Claim:** "A Doom agent running at 10 queries per second on text state costs about $7 per hour"
- **Source:** typesafe.ai/blog/introducing-system-one-models-and-jev (brief: "Doom 10 qps ~ $7/hour on text state")

### Naming (Kahneman and Jevons)
- **Claim:** "System One after Daniel Kahneman... Jev comes from William Stanley Jevons"
- **Source:** typesafe.ai/blog/introducing-system-one-models-and-jev (brief: "names from Kahneman (System 1/2) and William Stanley Jevons")

### RLCD
- **Claim:** "trained with RLCD (Reinforcement Learning from Calibrated Distributions)"
- **Source:** typesafe.ai/blog/introducing-system-one-models-and-jev (brief: "RLCD")
- **Link:** https://www.oguzhan.co/jev-confidence-rlcd-calibrated-decisions/ (oguzhan.co reference post)

### No type errors
- **Claim:** "your switch statement never sees a type error"
- **Source:** typesafe.ai/blog/introducing-system-one-models-and-jev (brief: "no type errors")

### awesome-jev community count
- **Claim:** "155 entries by September 20, 2026"
- **Source:** github.com/cobanov/awesome-jev (brief: "155 community entries as of 20 Sep 2026 review")

### Schema-valid vs correct
- **Claim:** "schema-valid output is not the same as a correct decision"
- **Source:** github.com/cobanov/awesome-jev README (quoted verbatim from brief)

### Independent implementations disclaimer
- **Claim:** "LitJev, kev, and minojev are independent implementations, not verified reproductions"
- **Source:** github.com/cobanov/awesome-jev (brief: "LitJev etc. are independent, not verified reproductions")

## oguzhan.co links used (4 total)
1. https://www.oguzhan.co/typesafe-jev-system-one-decision-model/ (hub - linked twice: "TypeSafe launched System One" and closing line)
2. https://www.oguzhan.co/jev-primitives-choice-score-noul/ (primitives)
3. https://www.oguzhan.co/jev-confidence-rlcd-calibrated-decisions/ (confidence)
4. https://www.oguzhan.co/jev-speed-cost-parallel-sampler/ (speed-cost)

## Voice compliance checklist
- [x] No em dashes (—)
- [x] No banned words (delve/tapestry/landscape/robust/leverage/underscore/pivotal)
- [x] No "not only X but also Y" stacks
- [x] No "In this article we will" opening
- [x] Uneven sentence rhythm (short punches next to longer specific sentences)
- [x] Concrete facts with sources (dates, numbers, names)
- [x] First-person practitioner voice ("I have been running Jev...")
- [x] Opening story framed as hypothetical ("Picture this...")
- [x] Specific nouns (TypeSafe, Kahneman, Jevons, RLCD, Doom)
- [x] Short paragraphs
- [x] 1-2 h3 subheads (3 total)
- [x] One Python code snippet
- [x] Two image placeholders with descriptions
- [x] 2-4 in-body links to oguzhan.co (4 used)
- [x] Closing line linking to hub
- [x] Series line at bottom

## Fact restrictions observed
- Only used facts from TypeSafe primary sources listed in brief
- Did not use The Register latency figures (per brief instruction)
- Did not invent numbers or claims beyond brief
- Labeled vendor numbers as "TypeSafe's workflow evals" and "their tested scenarios"
