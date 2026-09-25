# Part 2 claim and source notes

Primary sources are used for product behavior. The oguzhan.co links in `en.md` are contextual links for Medium readers, not the factual basis of the draft.

| Claim in `en.md` | Source | Notes |
|---|---|---|
| Jev has three question shapes: Choice, Score, and Noul. | [TypeSafe docs: Primitives](https://docs.typesafe.ai/primitives) | “The three TypeSafe question types.” |
| A useful question asks for one focused snap judgment rather than “analyze and determine the best course of action.” | [TypeSafe docs: Ask for one snap judgment per question](https://docs.typesafe.ai/primitives#ask-for-one-snap-judgment-per-question) | The post’s moderation wording and examples are original. |
| Choice is for one option from a known, unordered set. | [TypeSafe docs: Choose a question type](https://docs.typesafe.ai/primitives#choose-a-question-type) | |
| Choice should include `other` or `none of the above` when the supplied list may not cover every input. | [TypeSafe docs: Choose a question type](https://docs.typesafe.ai/primitives#choose-a-question-type) | |
| Score is for a spectrum whose ordered levels are explicitly described. | [TypeSafe docs: Choose a question type](https://docs.typesafe.ai/primitives#choose-a-question-type) | |
| A Score can return a position between two levels. | [TypeSafe docs: What comes back](https://docs.typesafe.ai/primitives#what-comes-back) | |
| Noul answers a yes/no proposition with a value from 0 to 1. | [TypeSafe docs: Primitives](https://docs.typesafe.ai/primitives) | |
| A Noul near 0.5 means yes and no have equal probability; it does not mean a medium amount of the measured quality. | [TypeSafe docs: Choose a question type](https://docs.typesafe.ai/primitives#choose-a-question-type) | |
| Choice returns `choice`, `probabilities`, and `confidence`. | [TypeSafe docs: What comes back](https://docs.typesafe.ai/primitives#what-comes-back) | |
| Score returns `score`, `legend`, `probabilities`, and `confidence`. | [TypeSafe docs: What comes back](https://docs.typesafe.ai/primitives#what-comes-back) | |
| Noul returns `noul` and has no separate confidence field. | [TypeSafe docs: What comes back](https://docs.typesafe.ai/primitives#what-comes-back) | |
| Question IDs are application-side identifiers and are not sent to the model; instructions must contain the complete question. | [TypeSafe docs: Define a question](https://docs.typesafe.ai/primitives#define-a-question) | |
| Several questions may share one state in a request, and question types may be mixed. | [TypeSafe docs: Ask multiple questions together](https://docs.typesafe.ai/primitives#ask-multiple-questions-together) | |
| Questions in one request are evaluated independently and in parallel; one answer is not context for another. | [TypeSafe docs: Ask multiple questions together](https://docs.typesafe.ai/primitives#ask-multiple-questions-together) and [When one question depends on another](https://docs.typesafe.ai/primitives#when-one-question-depends-on-another) | |
| A dependent judgment that requires an earlier answer to fetch evidence or construct the next state needs a second request. | [TypeSafe docs: When one question depends on another](https://docs.typesafe.ai/primitives#when-one-question-depends-on-another) | |
| TypeSafe positions Jev as a System One model for fast, structured decisions rather than open-ended string generation. | [TypeSafe launch post, 15 Sep 2026](https://typesafe.ai/blog/introducing-system-one-models-and-jev) | Company framing, stated as such in the post. |
| Typed or schema-valid output does not guarantee that the selected answer is correct. | [TypeSafe launch post: Hallucination and Type-safety](https://typesafe.ai/blog/introducing-system-one-models-and-jev#hallucination-and-type-safety) | The launch post distinguishes guaranteed schema matching from decision quality and discusses disagreements in its evals. |

## Illustrative material

The following are invented examples, not production reports or TypeSafe recommendations:

- Moderation item 4182 and the sentence “I know where you work. See you Friday.”
- The five original “bad prompt” rewrites.
- All moderation categories and their definitions.
- The four-level threat-severity rubric.
- The Python request in `en.md`.
- The `allow`, `limit_visibility`, `human_review`, and `urgent_escalation` action set.
- Any implied policy thresholds, review workflow, override logging, or taxonomy revision process.
- Both image descriptions.

No benchmark, accuracy, latency, cost, or personal production claim appears in the draft.
