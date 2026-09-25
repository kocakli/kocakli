# Write Questions a Machine Can Answer

## “Analyze this and decide” is not one instruction. It is five hidden arguments waiting to happen.

**Tags:** Artificial Intelligence, Software Engineering, LLM, Programming, Developer Tools

A moderator opens item 4182. The post says, “I know where you work. See you Friday.”

The queue prompt says:

> Analyze the content, consider context and policy, decide whether it is harmful, and take the appropriate action.

A person can deal with that sentence because people quietly invent the missing procedure. Which policy section applies? Does “Friday” make the threat credible? Is this a joke between friends? What actions are available? The moderator checks the account history, opens the policy, and chooses among several imperfect outcomes.

A machine sees one large verb pile.

Even if it returns valid JSON, the team cannot tell which judgment moved the result. A new policy version arrives and somebody edits three adjectives in the prompt. False positives rise. Nobody knows whether the cause was the threat definition, the context window, or the instruction to “take the appropriate action.”

That is a question-design bug, not a model-formatting bug.

The useful unit is smaller: one snap judgment that a knowledgeable reviewer can make from the evidence in front of them. TypeSafe’s [Jev primitives](https://www.oguzhan.co/jev-primitives-choice-score-noul/) give those judgments three shapes: Choice, Score, and Noul. The shape matters less than the discipline it forces. Your application has to say what it wants to know before the model answers.

<!-- IMAGE 1: A dark navy moderation inbox split into five narrow cyan decision cards, with one amber card marked for human review; no people, no text -->

### Turn the policy meeting into five questions

Start with the ugly prompt. Do not polish it. Pull it apart.

**1. “Analyze this post and decide what kind of violation it is.”**

Rewrite it as a Choice: “Which single policy category best describes `post.text`?” Give it `credible_threat`, `targeted_harassment`, `hate`, `spam`, `adult_content`, and `other`.

That last option is not decorative. A closed list without an escape hatch forces an unfamiliar case into the least-wrong bucket. `other` is an operational result: send it to general review, log what the taxonomy missed, then decide whether the list needs a new category.

**2. “Assess how bad this is.”**

Rewrite it as a Score with observable levels:

1. No target and no plausible harm.
2. A target is present, but the language is insulting or unwanted rather than threatening.
3. A target and a threat are present, but timing, means, or intent is unclear.
4. The post names a target and includes a plausible time, place, method, or repeated pursuit.

“Low, medium, high” would be shorter. It would also outsource the rubric to the model. A testable level tells two reviewers what evidence should move an item from 2 to 3.

**3. “Check whether the author threatens the target.”**

Rewrite it as a Noul: “Does `post.text` express or imply that the author, or someone acting for the author, intends physical harm toward `reported_user`?”

This is yes/no shaped. The returned value is the probability of yes. If it comes back near 0.5, that means the model is split between yes and no. It does not mean “a medium-strength threat.”

That confusion matters. Strength is a spectrum, so it belongs in a Score with written levels. Truth of a proposition belongs in a Noul. A coin toss is not a midpoint.

**4. “Review the conversation and account history for context.”**

Rewrite it as two focused questions: “Does `thread.messages` contain clear evidence that the statement is mutually understood as a joke?” and “Does `author.prior_actions` show repeated unwanted contact with `reported_user`?”

Both can be Noul questions if the state contains the named evidence. Neither should pretend to discover records that were never supplied. Retrieval remains ordinary code.

**5. “Decide the appropriate action.”**

Do not ask the model to absorb the entire enforcement manual. Ask for the facts and judgments the program needs, then keep policy in code. For an illustrative queue, category, threat severity, joke context, and repeated-contact probability might feed `allow`, `limit_visibility`, `human_review`, or `urgent_escalation`.

Those action names and thresholds are examples, not recommendations. A gaming forum, a school platform, and a marketplace should not share one enforcement rule.

Here is the whole request shape:

```python
questions = {
    "policy_category": Choice(
        instructions="Which policy category best describes `post.text`?",
        criteria={
            "credible_threat": "Threat of physical harm with credible detail.",
            "targeted_harassment": "Abuse aimed at a person without a credible threat.",
            "hate": "Attack based on a protected characteristic.",
            "spam": "Unsolicited repetitive or deceptive promotion.",
            "adult_content": "Sexually explicit content.",
            "other": "None of the listed categories fits.",
        },
    ),
    "threat_severity": Score(
        instructions="How severe is the threat evidence in `post.text`?",
        criteria=[
            "No target and no plausible harm.",
            "Targeted abuse, but no threat.",
            "Threat present; timing, means, and intent unclear.",
            "Threat plus plausible time, place, method, or repeated pursuit.",
        ],
    ),
    "physical_harm_intent": Noul(
        instructions=(
            "Does `post.text` imply intent to physically harm `reported_user`?"
        ),
    ),
}
```

Choice returns the selected option, a distribution over the supplied options, and confidence. Score returns a position along the ordered levels, the legend, a distribution, and confidence. Noul returns one 0-to-1 probability and no separate confidence field. Question IDs such as `physical_harm_intent` are for application code; TypeSafe’s documentation says they are not sent to the model, so the full meaning must live in `instructions`.

Several independent questions can share one state in a request. They are evaluated independently and in parallel. One answer does not secretly become context for the next. If the category must determine which policy document gets fetched, that is a real dependency: receive the first answer, fetch the document in code, then make another request. If every judgment can use the original post and history, ask them together.

This is the practical boundary behind the [System One framing](https://www.oguzhan.co/typesafe-jev-system-one-decision-model/). Fast judgment is useful when the question is narrow. “Read everything, apply our values, and be right” is not narrow.

### The escape route belongs in the design

A good moderation system has two kinds of escape.

The first is semantic: `other`, `none_of_the_above`, or an equivalent Choice option. It admits that a taxonomy is incomplete.

The second is operational: human review. Uncertainty, missing context, policy conflict, or high-impact action should have somewhere to go. The model can produce a schema-valid answer and still choose the wrong category. Typed output removes one failure mode. It does not certify the judgment.

<!-- IMAGE 2: Dark navy flow diagram made from objects only: an amber inbox card branching to cyan choice, ruler, and probability tokens, then converging on code and a human-review tray; no people, no text -->

The review queue also gives question design a feedback loop. When moderators override `credible_threat` to `targeted_harassment`, store the case. When `other` fills with the same pattern, revise the taxonomy. When reviewers disagree about Score level 3, fix the rubric before tuning a threshold.

This is slower than writing “analyze carefully.”

It is much faster than debugging a policy hidden inside a paragraph.

The longer, weekly version is on [oguzhan.co](https://www.oguzhan.co/typesafe-jev-system-one-decision-model/).

*Part 2 of 7 in Smart If-Statements. Previous: [The day the model answered “Billing.” with a period](https://oguzhankocakli.medium.com/the-day-the-model-answered-billing-with-a-period-539ee9dc38a8). Next: Your threshold is a product decision.*
