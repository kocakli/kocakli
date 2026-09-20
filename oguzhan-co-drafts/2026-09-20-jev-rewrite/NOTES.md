# Jev rewrite notes

## Deliverables

- `4766-en.md`: English TypeSafe Jev hub
- `4767-tr.md`: original Turkish hub
- `4780-en.md`: English primitives day
- `4781-tr.md`: original Turkish primitives day

All four drafts include WordPress-ready front matter for title, Yoast title, meta description, and focus keyphrase.

## Source provenance

The requested `uploads/` directory was not present in the workspace, current `main`, or any mounted upload location available to this run. In particular, `uploads/BRIEF.md`, `uploads/AGENT_VOICE.md`, and the four `post-*.md` files could not be opened.

Work continued from two verifiable substitutes:

1. The exact four published WordPress records and canonical pages for post IDs 4766, 4767, 4780, and 4781.
2. The repository's existing `oguzhan-co-drafts/AGENT_VOICE.md` from remote branch `origin/cursor/weekly-en-tr-drafts-55c0`, which contains the stated EN anti-slop and TR Dünya Halleri rules.

No unavailable brief content has been invented or claimed as reviewed.

## Editorial decisions

### English

- Rebuilt both articles rather than polishing sentences in place.
- Removed template openings, repetitive section rhythm, slogan-heavy transitions, and generic conclusions.
- Avoided the voice pack's banned words and structures, including em dashes, `delve`, `landscape`, `robust`, `leverage`, `underscore`, `pivotal`, and “not only ... but also.”
- Kept paragraphs uneven on purpose: short factual punches next to longer technical explanations.
- Added direct links to primary documentation and clearly labeled company claims.

The hub now opens with the software-interface argument (“An `if` statement has no use for a confident paragraph”) instead of a product definition. The primitives post opens with the size of the API surface, then moves from question design to types, request shape, batching, composition, and safety.

### Turkish

The Turkish drafts are separate compositions, not line translations.

- The hub opens through the Doom demo and its missing small print, then moves to the product idea.
- The primitives article starts with a Turkish support-ticket scene and builds the three types from that case.
- Section order, examples, paragraph boundaries, transitions, and closings differ from the English drafts.
- English technical terms remain where Turkish substitutions would blur meaning: `state`, Choice, Score, Noul, System One, RLCD, benchmark, eval, tool, provider, false positive, false negative.
- Bureaucratic and brochure Turkish was removed. There are no `-maktadır/-mektedir` stacks, “günümüzde,” “sonuç olarak,” “devrim niteliğinde,” “oyun değiştirici,” or decorative dash constructions.

Examples of structural divergence:

1. EN hub begins with an `if` statement; TR hub begins with Doom and the structured-state caveat.
2. EN hub explains the return types before the hallucination claim; TR hub introduces the System One boundary first, then tests the marketing sentence.
3. EN primitives begins with an API summary; TR begins with an airline refund message.
4. EN primitives introduces field paths before batching; TR explains the three primitives through the ticket, then moves into the combined request and JSON paths.
5. EN closes on “a branch, a position, a probability”; TR closes by setting up the next day's question about `confidence`.

## Technical facts retained

- Jev accepts `state` plus named typed questions.
- Choice returns `choice`, `probabilities`, and `confidence`.
- Score returns `score`, `legend`, `probabilities`, and `confidence`.
- Noul returns a probability in `[0, 1]` and no separate confidence field.
- Questions sharing a request are evaluated independently and do not pass answers to one another.
- Dot-and-index field paths are written inside backticks in instructions.
- Choice cardinality is capped at 255 in the Wikiracing discussion.
- Launch pricing remains $0.042 per million input tokens with free output tokens.
- Reported service latency remains 70-500 ms.
- Reported workflow peaks remain 193.6x faster and 444.6x cheaper, explicitly marked as TypeSafe figures from its own harness.
- The Doom bot receives structured game state as text, not pixels.
- Provider IDs remain distinct for OpenRouter, Vercel AI Gateway, and Cloudflare Workers AI.
- Company training terminology remains RLCD, Reinforcement Learning for Calibrated Decisions.

## Parallel cookbook number

The supplied/published source article states 11.5x cheaper and 9.6x faster for 13 batched questions. The live cookbook fetched during the rewrite currently shows a refreshed run at 12.2x and 10.0x.

The rewritten day-one posts preserve the source article's 11.5x and 9.6x figures and add a version-drift warning. This avoids silently changing the source post while acknowledging that cookbook measurements can move.

## Safety and claim handling

- “Cannot hallucinate” is narrowed to output-shape/type safety.
- Schema-valid output is repeatedly distinguished from a correct judgment.
- RLCD is identified as TypeSafe's training account, not an independently reproduced public recipe.
- Company benchmarks are separated from independent evidence.
- Production guidance keeps deterministic checks and human fallback in front of irreversible actions.
- Doom is not described as vision-based gameplay.
- LitJev, openjev, kev, and NanoJev are described as independent experiments, not verified copies of TypeSafe's private stack.

## Final checks

- Requested file set: present, with no extra deliverables in the dated directory.
- Front matter: all four posts include `title`, `yoast_title`, `yoast_metadesc`, and `focus_keyphrase`.
- Markdown sources: each post has a Sources/Kaynaklar section and at least five direct links.
- Word counts including front matter: 4766 EN 1,853; 4767 TR 1,565; 4780 EN 1,523; 4781 TR 1,278.
- Voice scan: no banned EN/TR phrases or em/en dashes occur in the four article files.
- Repository check: `git diff --check` passes.
