# The Day the Model Answered "Billing." With a Period

## When your LLM classifier returns confident paragraphs but your switch statement needs clean choices

**Tags:** Artificial Intelligence, Software Engineering, LLM, Programming, Machine Learning

---

Picture this. You have a support ticket classifier running in production. The LLM reads an angry email about a double charge and your code waits for a category string to route it.

The model returns: "Billing."

Your switch statement breaks. Was it supposed to be `"billing"` lowercase? Did training examples have periods? You patch it with `.strip().lower()`. Two days later the model returns: "I believe this falls under billing issues, though there may be account-related aspects."

Your beautiful routing logic is now wrapped in substring checks and fallback heuristics. The LLM is doing frontier-level reasoning but your code treats it like an unreliable intern who can't fill out a form.

This is the gap that makes you question every LLM integration you ship. You wanted a decision. You got prose.

## What if the model spoke the language of your switch statement?

On September 15, 2026, [TypeSafe launched System One](https://typesafe.ai/blog/introducing-system-one-models-and-jev), a decision model trained for two years in stealth by ex-OpenAI researchers. The pitch is simple: unstructured state in, typed probabilistic decisions out.

No paragraphs. No "I think." No string-matching prayer.

They call the output format **Jev**, and it has three primitives that map to how software actually makes choices.

**Choice** returns an option from your enum plus probabilities for each. If you ask "refund or escalate?" with a messy ticket transcript, you get back `choice: "refund"`, `probabilities: {"refund": 0.87, "escalate": 0.13}`, and a calibrated `confidence` score. [The primitives](https://www.oguzhan.co/jev-primitives-choice-score-noul/) are designed so your switch statement never sees a type error.

**Score** returns a continuous value on a rubric you define. "How urgent is this bug report on a scale from routing-logic tweak to production-down fire?" The model gives you a `score`, a `legend` explaining the anchors, probabilities across discrete bins, and confidence again.

**Noul** returns a 0-to-1 probability with no confidence score. It is for yes/no gates where calibration is already baked into your threshold. "Is this message spam?" gives you a float. You decide if 0.92 is high enough to auto-delete.

Here is what calling it looks like in Python:

```python
from typesafe import TypeSafeClient

client = TypeSafeClient(api_key="your_key")

questions = [
    {
        "type": "choice",
        "question": "Route this ticket: billing, technical, or sales?",
        "options": ["billing", "technical", "sales"],
        "context": ticket_text
    },
    {
        "type": "score",
        "question": "Rate urgency from 0 (can wait) to 10 (production down)",
        "context": ticket_text
    }
]

decisions = client.system_one(questions)
```

You get back structured decisions you can route on. No parsing. No "the model returned markdown instead of JSON" incident reports. [Your confidence thresholds](https://www.oguzhan.co/jev-confidence-rlcd-calibrated-decisions/) can trigger review queues or escalation paths without string surgery.

[IMAGE 1: Split-screen showing messy JSON-mode LLM output with inconsistent fields on left, clean Jev Choice object with probabilities array on right]

## Why this matters for if-statements that route real stakes

Every software team I have worked with has at least one place where an LLM result feeds into a decision branch. Content moderation. Fraud scoring. Document routing. Refund approvals.

The pattern is always the same. The model is brilliant until you need to act on what it said. Then you write parsing code, fallback logic, and retry handlers for hallucinated fields. The decision boundary gets buried under string cleanup.

Jev flips this. The decision is the output. You ask a question the way a switch statement would ask it. The model returns the type your code expects.

TypeSafe's [speed and cost numbers](https://www.oguzhan.co/jev-speed-cost-parallel-sampler/) show 70 to 500 milliseconds per decision versus 3 to 329 seconds for frontier chat models on their workflow evals. Input costs $0.042 per million tokens. Output is free because it is just the structured decision object. They claim 193.6x to 444.6x faster on the higher end of their tested scenarios. Batching 13 questions in one call is 11.5x cheaper and 9.6x faster than serial requests.

You can fit this into latency-sensitive paths. A Doom agent running at 10 queries per second on text state costs about $7 per hour. That is the kind of unit economics that make real-time decision loops viable in production, not just demos.

[IMAGE 2: Timeline graphic comparing frontier model latency (3-329 seconds) versus System One latency (70-500ms) for decision tasks]

## The naming is a thesis

TypeSafe named the model family **System One** after Daniel Kahneman's fast, instinctive decision mode from *Thinking, Fast and Slow*. The output format **Jev** comes from William Stanley Jevons, the 19th-century economist who built a mechanical computer to solve logic problems.

That pairing tells you what they think typed decisions are for. Not multi-turn reflection. Not chain-of-thought essays. Snap judgments that software can act on immediately, the way a human routes an email in two seconds or an operator decides "safe to proceed" from a dashboard reading.

System One models are trained with RLCD (Reinforcement Learning from Calibrated Distributions). The confidence scores are not vibes. They reflect the probability distribution shape the model learned during training. When the model says it is 91% sure, it has been penalized in training for overconfident mistakes at that probability level.

The [awesome-jev](https://github.com/cobanov/awesome-jev) community list hit 155 entries by September 20, 2026. Projects like LitJev, kev, and minojev are independent implementations, not verified reproductions. The ecosystem is loud about one thing: schema-valid output is not the same as a correct decision. You still test your prompts. You still need labeled eval sets. But you stop debugging type errors when the model returns a decision.

## What this series will test

I have been running Jev against seven real-world problems over the past week. Content moderation queues. Document classifiers that drift when label definitions change. Cost napkins for a million events a day. Designing thresholds that are product decisions, not magic numbers copied from blog posts.

Each part of this series will take one of those problems and show what breaks, what works, and where typed decisions belong versus where a chatbot still wins. I am not selling anything. I am testing whether this model category is a step function or just a faster JSON mode.

Part 2 will cover question design. The gap between prompts that work for humans and questions a machine can answer cleanly. If you have ever written "analyze this and decide" and gotten back three paragraphs of hedging, you know the problem I mean.

I write the longer, weekly version of this on [oguzhan.co](https://www.oguzhan.co/typesafe-jev-system-one-decision-model/).

---

**Part 1 of 7** in *Smart If-Statements: typed questions for LLM-era software*. Next: **Write questions a machine can answer** (designing decision prompts that bypass paragraph hedging).
