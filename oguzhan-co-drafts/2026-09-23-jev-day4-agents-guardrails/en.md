---
title: "Jev agent guardrails: schema-valid is not the same as safe"
slug: jev-agent-guardrails-schema-valid-not-safe
yoast_title: "Jev guardrails: schema-valid ≠ safe for agents | oguzhan.co"
yoast_metadesc: "Jev powering coding-agent tool gates, evidence ledgers, wake checks, and pre-run scans. Schema-valid calls still need host policy."
focus_keyphrase: Jev guardrails
lang: en
word_count_target: 900-1400
---

Jev guardrails matter most when the consumer is an agent loop, because a schema-valid tool call can still be wrong, destructive, or outside the user's request. Jev returns calibrated probabilities for typed questions. The host application, its permission UI, and the operating-system sandbox still own the decision to allow, ask, deny, and perform side effects.

I reached that hard line while reading the Agents section of [awesome-jev](https://github.com/cobanov/awesome-jev), the project READMEs around it, and OpenRouter's cookbook. The catalog puts it plainly: “A model judgment does not establish safety or replace the host application's permission checks.” That sentence is more useful than any promise of an agent that can safely run on autopilot.

## 🛡️ The useful order for Jev guardrails

Start with what code can prove. Ask Jev only about the part that requires judgment. Then let host policy turn the answer into an action.

[OpenRouter's refund example](https://openrouter.ai/docs/cookbook/building-agents/gate-tool-calls-with-jev) makes the sequence concrete. Its static HITL gate becomes a per-call check carrying the support ticket and refund policy. Before any Decisions call, ordinary code verifies that the order belongs to the ticket and that the requested amount does not exceed the remaining balance. A bad amount is blocked there. No probability is needed.

The surviving request gets three Noul questions: did the customer ask for this, is it the right order, and does policy cover the case? The sample uses 0.9 as the approval threshold and 0.1 as the blocking threshold. Results between those edges go to human review.

The captured fixtures are refreshingly mundane. Late kettle shipping is approved. An espresso order that belongs to somebody else is blocked. A crushed box with disputed policy coverage goes to review. An over-balance refund never reaches Jev because arithmetic already settled it. In those runs, a Decisions request cost less than $0.0001 and took under roughly 600 ms. A broken check throws instead of silently approving.

That is the pattern: deterministic checks, typed probabilities, host policy. Type safety keeps the judgment shaped and parseable. It does not make the proposed refund correct or permitted. I covered the model's primitives earlier in the [series hub](https://www.oguzhan.co/typesafe-jev-system-one-decision-model/); the important part today is where their authority stops.

## ⛔ jev-guard checks every tool call

[jev-guard](https://github.com/leepokai/jev-guard) applies that pattern to coding agents through an auto-mode style PreToolUse hook. Its README lists Claude Code, Codex, Copilot CLI, Gemini CLI, Cursor, pi, OpenCode, and ACP. Before a tool runs, Jev assigns a `risk` Score from 0 to 3, from read-only to destructive, and estimates `approval`, `user_requested`, and `from_untrusted` as Noul probabilities over session context.

The policy remains regular code. Roughly, it denies when risk reaches 2.5 or `from_untrusted` reaches 0.7. It asks when risk reaches 1.5 or `approval` reaches 0.75. Strong evidence that the user requested an action, at 0.85 or above, can turn ask into allow. It can never lift a deny.

That last rule is the bit I would circle. User intent is evidence, not a skeleton key.

The hook also looks after execution. It scans tool results for prompt injection and canaries, flags a finding, and remembers it for the session. Skills, plugins, and instruction files can be checked for unexpectedly hostile content too. The project reports about 1,000 tokens and roughly $0.00004 for a typical call at the $0.042-per-million-input-token list price. Its measured wall time was about 580 to 750 ms through Gateway from Taiwan, a separate measurement from TypeSafe's 70 to 500 ms West Coast figure.

None of that means jev-guard stops every injection or makes a destructive command safe. It is a judgment input wired into explicit thresholds. The host still enforces the result.

## 📒 Canny makes “done” produce evidence

Tool approval is only half the agent problem. An agent can run permitted commands and still declare victory without a passing check.

[Canny](https://github.com/qkal/Canny) handles that with an append-only evidence ledger for each session. Deterministic hooks record facts such as a file edit, command exit codes, repeated identical failures, or AWS-key-looking text in a pending write. Jev is reserved for questions code cannot settle cleanly: is this message claiming the job is done, or does this diff violate a stated project rule?

The distinction is unusually sharp: Jev never blocks in Canny. If a “done” message is refused, the ledger lacks a passing check. A probability did not cross some hidden line. When Jev is unsure or no API key is present, the judgment layer fails open. The underlying record remains available through `canny replay`, and Claude Code or Codex can install the hooks through `init`.

I like this design because it separates testimony from evidence. Jev can notice a completion claim; the ledger can answer whether the session has earned it.

## ⏰ Wake only when something changed

Long-running agents create a quieter waste: waking the full model to discover that nothing happened.

[wakegate](https://github.com/shitianfang/wakegate) asks one Jev question before resuming a sleeping agent: given `waitingFor`, an optional event or observation, and the skipped count, is this wakeup worth a full LLM turn? A message from the user always wakes it. Errors wake it too, and the default `maxSkips` of 10 eventually forces a turn. The gate fails open.

The project targets Workers, Durable Objects, and long-running Node agents, and reports about 250 ms in its runs. It does not decide how long the agent should sleep. It only judges whether the new event deserves an expensive resume.

This is a small control surface, which is precisely why it works. Day 5 will look at context compaction. For now, wakegate shows that the cheapest context may be the turn you do not start.

## 🦠 Scan the unfamiliar tree before running it

The riskiest time to inspect a repository is after its setup command has already executed. [is-malicious](https://github.com/luantak/is-malicious) offers a pre-run pass over source, configuration, build, and CI text with Jev. Its report includes file and line range, category, probability, confidence, and reason. GitHub Actions examples can apply the same idea to pull-request diffs.

The caveats belong beside the feature. A clean report is not proof of safety. The tool is not antivirus, a dependency CVE audit, or a secret scanner. Telemetry findings are reported as information and do not fail the exit by themselves. It also requires `TYPESAFE_API_KEY` and consumes paid input tokens.

So I would use it before running an unfamiliar tree, then keep the normal controls: inspect suspicious files, constrain permissions, and execute uncertain code in a sandbox. No scan result should erase those steps.

## The boundary is the feature

Jev makes cheap, typed judgment practical enough to place at more agent boundaries: before a tool, after its result, before a completion claim, before a wakeup, and before unfamiliar code runs. The [TypeSafe launch post](https://typesafe.ai/blog/introducing-system-one-models-and-jev) described verification, guardrails, and jailbreak detection as System One use cases. These projects show what that can look like without pretending the model owns security policy.

The compact rule is still the best one. Code proves what code can prove. Jev advises on ambiguous cases. Host policy decides, humans handle the uncertain middle, and sandboxes contain side effects.

That boundary also connects today's examples to the [Day 3 speed and cost discussion](https://www.oguzhan.co/jev-speed-cost-parallel-sampler/). Fast, inexpensive judgment makes frequent gates feasible. It does not make them infallible. Day 5 will move inward to context compaction, where deciding what an agent carries forward creates a different kind of gate.
