# Part 3 notes

## Claim-to-source ledger

Only externally verifiable claims are listed here. Product recommendations and the article's arguments are identified as author analysis.

| Claim in `en.md` | Source | What the source supports |
|---|---|---|
| Jev Choice and Score answers include a probability distribution and `confidence`. | https://docs.typesafe.ai/confidence.md | The Confidence reference says every Choice and Score answer includes `probabilities` and a confidence value from 0 to 1. |
| TypeSafe derives Choice and Score confidence from the shape of the returned distribution; concentrated distributions have higher confidence than flat ones. | https://docs.typesafe.ai/confidence.md | The reference defines confidence as a statistic computed from the answer's probabilities and documents the formulas for both primitives. |
| TypeSafe presents three confidence-based paths: act automatically, proceed cautiously, and do not act. | https://docs.typesafe.ai/confidence.md | The “Three paths for using confidence in your code” section defines those routes and says boundaries depend on the stakes. |
| Different actions can use different confidence thresholds according to the consequences of an error. | https://docs.typesafe.ai/confidence.md and https://docs.typesafe.ai/patterns/confidence-routing.md | The docs use separate handling for a balance check and a transfer approval and state that thresholds scale with risk. The article does not reuse those example values. |
| A calibration curve, also called a reliability diagram, bins predictions and compares mean predicted probability with the observed fraction of positives. | https://scikit-learn.org/stable/modules/calibration.html | Scikit-learn's “Calibration curves” section defines the chart and both axes. |
| For a well-calibrated binary classifier, predictions near 0.8 should be positive about 80 percent of the time. | https://scikit-learn.org/stable/modules/calibration.html | The opening definition gives this example. |
| Calibration should be evaluated on data independent of model fitting; small calibration datasets can overfit. | https://scikit-learn.org/stable/modules/calibration.html | The calibration section recommends independent data, and the isotonic section warns that the more flexible method is prone to overfitting on small datasets. This supports the article's conservative holdout advice; the article does not claim a universal minimum sample size. |
| TypeSafe calls its training method Reinforcement Learning for Calibrated Decisions (RLCD). | https://docs.typesafe.ai/introduction/machine-learning-primer.md and https://typesafe.ai/blog/introducing-system-one-models-and-jev | Both first-party sources name RLCD. |
| TypeSafe says RLCD trains its model to return decisions and calibrated probabilities, where higher probability should correspond to a greater chance of correctness across groups of predictions. | https://docs.typesafe.ai/introduction/machine-learning-primer.md | The RLCD section states the output contract and explicitly says calibration rates apply to groups, not individual answers. This is presented in the draft as a vendor claim. |
| TypeSafe's launch post says Jev returns structured values with probabilities and confidence. | https://typesafe.ai/blog/introducing-system-one-models-and-jev | The launch comparison describes typed probabilistic outputs and confidence. The current docs provide the more precise primitive-level exception for Noul. |
| Vendor calibration does not certify performance on a particular application's data; teams should validate on their own data and calibrate thresholds. | https://github.com/cobanov/awesome-jev | The repository's “Important caveat” says schema-valid output is not the same as a correct decision and advises validation on one's own data, threshold calibration, deterministic checks, and a human fallback. |
| Jev version aliases can move, so evaluations should pin a model version. | https://github.com/cobanov/awesome-jev | The repository's “Current model” note distinguishes current aliases from a pinned version and says to pin the version when comparing evaluations. |
| A Noul returns the probability that a yes-or-no statement is true and has no separate `confidence` field. | https://docs.typesafe.ai/primitives/noul.md and https://docs.typesafe.ai/confidence.md | Both pages describe the Noul output; the Confidence page explicitly says there is no separate confidence property. |
| A Noul value near 0.5 expresses uncertainty directly. | https://docs.typesafe.ai/confidence.md | The Noul subsection says a value near 0.5 means the model is unsure. |
| Choice confidence measures concentration among alternatives rather than the probability that a yes-or-no statement is true. | https://docs.typesafe.ai/confidence.md | The Choice subsection defines confidence from the top option's probability relative to an even split. |
| One mistake among nine cases changes an observed rate by more than eleven percentage points. | Arithmetic: `1 / 9 = 0.111...` | Direct calculation used to illustrate small-bin volatility. |

## Author analysis and recommendations

The following are arguments or workflow recommendations made by the article, not claims attributed to a source:

- A threshold is product policy because it allocates the consequences of errors.
- Error costs should be made explicit before selecting cutoffs.
- Separate actions may deserve separate cutoffs.
- Evaluation should preserve the inputs the deployed system will receive.
- Teams should retain a holdout, show counts beside reliability bins, sample live decisions for later labeling, and rerun evaluation after policy, traffic, OCR, or model changes.
- Auto-act, human review, and refusal or fallback should stay visible in product behavior and logs.

## Illustrative material

All expense-report content is illustrative:

- The hotel, train, client dinner, duplicate receipt, `approve` result, 0.81 confidence, and 0.80 policy threshold.
- The three routes: auto-approve, human review, and return to employee.
- The 200-item labeled set.
- The cost categories and all suggested differences among report types.
- The Python input schema, routing names, candidate cutoffs, and cost table.
- The nine-item 0.90 to 1.00 reliability bin.

No example is presented as a production deployment, benchmark, or TypeSafe recommendation.

## Research boundary

- Read the TypeSafe documentation index, Confidence reference, Noul reference, confidence-routing pattern, and AI primer.
- Read TypeSafe's September 15, 2026 launch post.
- Read `cobanov/awesome-jev`, including its validation and version-pinning caveats.
- Opened the required oguzhan.co confidence/RLCD post for linking only. No passage from it was paraphrased.
- Read scikit-learn's probability-calibration documentation for reliability diagrams, independent calibration data, and small-sample cautions.

## Compliance

- Prose word count excluding the fenced code block and HTML image comments: **1,104**
- Em-dash count: **0**
- En-dash count: **0**
- Banned-word count: **0**
- Code blocks: **1**, with **20** lines
- Subheads (`###`): **2**
- Image markers: **2**, exactly `<!-- IMAGE 1 -->` and `<!-- IMAGE 2 -->`
- In-body oguzhan.co links: confidence/RLCD, primitives, and the required closing hub link
- Part 2 linked once in the body and once in the required footer
