# Your Threshold Is a Product Decision

## The number between a model's answer and an automatic action decides who pays when the answer is wrong.

**Tags:** Machine Learning, Programming, AI Agents, Artificial Intelligence, Software Engineering

The expense report looked ordinary: one hotel night, one train ticket, one client dinner.

The classifier returned `approve` with 0.81 confidence. The policy said anything above 0.80 could pass without review. So it passed.

Then finance found the duplicate dinner receipt.

This example is illustrative, but the design mistake is common enough to recognize. Someone copied 0.80 from a sample, a default, or a post. The team discussed the model at length and the threshold for five minutes. Yet that decimal decided whose time and money were at risk.

A threshold is policy written as a float.

In [Part 2](https://oguzhankocakli.medium.com/write-questions-a-machine-can-answer-d127eed1c346), I argued for narrow questions with answers that code can use. A typed answer still leaves another question: when should the program trust it enough to act?

TypeSafe's Jev makes that question visible. Choice and Score answers include a probability distribution and a `confidence` value. TypeSafe derives confidence from the shape of that distribution: a concentrated answer scores higher than a flat one. Its [confidence and RLCD reference](https://www.oguzhan.co/jev-confidence-rlcd-calibrated-decisions/) explains the feature. The product decision begins after the response arrives.

<!-- IMAGE 1 -->

### Start with the bill for being wrong

Consider an illustrative expense system with three routes: auto-approve, human review, and return to the employee for clarification. The model chooses `approve`, `review`, or `return`; application code decides whether confidence is sufficient for the proposed route.

Do not begin by asking whether 0.80 feels strict.

Write down the errors. An incorrect auto-approval can pay a duplicate or out-of-policy claim. An incorrect return delays reimbursement and creates work for the employee. Sending a clean report to review consumes finance time. These costs have different owners, and they do not fit into one symmetric “accuracy” number.

Now collect a small labeled set from your own traffic. Two hundred past reports is an illustrative starting size, not a statistical promise. Preserve the inputs the model will actually see. Have the people who own the policy label the intended route, record disagreements, and keep rare expensive cases in view.

Run the candidate model over that frozen set without letting it change the labels. For each possible threshold, count false auto-approvals, false returns, and review volume. Attach an explicit cost to each outcome. The values can be money, staff minutes, or a product-specific loss score, but somebody must own them.

This short Python example is illustrative. It assumes `rows` contains a proposed action, its confidence, and the human label:

```python
def route(row, auto_cutoff, return_cutoff):
    if row["confidence"] < min(auto_cutoff, return_cutoff):
        return "human_review"
    if row["prediction"] == "approve":
        return "auto_approve" if row["confidence"] >= auto_cutoff else "human_review"
    if row["prediction"] == "return":
        return "return_to_employee" if row["confidence"] >= return_cutoff else "human_review"
    return "human_review"

def total_cost(rows, auto_cutoff, return_cutoff, costs):
    return sum(
        costs[(route(row, auto_cutoff, return_cutoff), row["label"])]
        for row in rows
    )

candidates = [i / 100 for i in range(50, 100)]
best = min(
    ((a, r) for a in candidates for r in candidates),
    key=lambda cuts: total_cost(rows, *cuts, costs),
)
```

The code does not discover the correct cost table. That remains a product and operations argument. It does expose the argument. A team can inspect why a false approval costs more than an unnecessary review and change the values when policy changes.

Notice the two cutoffs. Auto-approving and returning a report are separate actions with separate harms. A single global threshold hides that asymmetry. You may need different cutoffs for hotel receipts and mileage claims too, if their error rates or consequences differ.

Use a holdout set before accepting the winning pair. Testing every candidate on the same 200 illustrative records can reward noise, especially when a costly error appears only once or twice. With a small set, prefer broad evidence and conservative routing over a decimal polished to two places.

### Calibration travels poorly

Confidence is useful only if similar scores mean something on your cases.

A basic sanity check is a reliability table. Put predictions into confidence bins, then compare each bin's average reported confidence with its observed accuracy. Scikit-learn's calibration guide describes the same idea for probability predictions: a well-calibrated binary classifier's predictions near 0.8 should be positive about 80 percent of the time. A reliability diagram plots observed frequency against predicted probability.

Do this check per action when the costs differ. An aggregate chart can look respectable while `approve` is weak and a larger, easier class carries the average.

Small bins lie by accident. In an illustrative 200-item set, the 0.90 to 1.00 bin might contain nine reports. One mistake moves observed accuracy by more than eleven percentage points. Show the count beside every bin, combine sparse bins, and resist declaring victory from a tidy diagonal.

TypeSafe says RLCD trains Jev to return calibrated probabilities, with higher probability corresponding to a greater chance of a correct answer across groups of predictions. Its launch post also says Jev returns confidence with structured answers. Those are vendor claims about the model and its evaluation setup. They do not certify an expense policy, your receipt mix, or next quarter's traffic.

Your distribution can differ in boring ways: a new travel vendor, OCR changes, a revised meal policy, more claims from another country. Model updates matter too. Pin the model version during evaluation, and rerun the labeled set after a version change. Keep sampling live decisions for later labeling so drift becomes a measured problem.

Calibration also does not pick a threshold for you. Even a perfectly calibrated score leaves the cost question untouched. If 5 percent error is unacceptable for automatic payment, 0.95 may still be too low. If a review costs more than the reversible action it prevents, the sensible cutoff may move the other way.

There is one API detail that prevents a subtle bug. TypeSafe's docs say Noul returns the probability that a yes-or-no statement is true and has no separate `confidence` field. A Noul value near 0.5 expresses uncertainty directly. Thresholding that value asks, “How probable is yes?” Thresholding Choice confidence asks, “How clearly did one option beat the alternatives?” Those are different operations, as the [primitive guide](https://www.oguzhan.co/jev-primitives-choice-score-noul/) lays out.

<!-- IMAGE 2 -->

The three routes should remain visible in the interface and the logs. Auto-act when the measured risk fits the action. Ask a person when the expected cost justifies their attention. Refuse or fall back when the state is missing, the question is a poor fit, or the action should never be delegated.

Then revisit the number.

A threshold is not model configuration to set once and forget. It is a compact agreement about errors, review capacity, and who absorbs the miss. Treat it like one.

I write the longer, weekly version of this on [oguzhan.co](https://www.oguzhan.co/typesafe-jev-system-one-decision-model/).

---

**Part 3 of 7** in *Smart If-Statements: typed questions for LLM-era software*. Previous: [Write Questions a Machine Can Answer](https://oguzhankocakli.medium.com/write-questions-a-machine-can-answer-d127eed1c346). Next: **Napkin math for a million decisions**.
