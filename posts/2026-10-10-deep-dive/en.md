---
title: "Claude Managed Agents: what dynamic workflows actually change"
slug: "claude-managed-agents-dynamic-workflows"
focus_keyphrase: "Claude Managed Agents"
yoast_title: "Claude Managed Agents: Dynamic Workflows"
meta_description: "Claude Managed Agents now run dynamic workflows in public beta. Here are the limits, costs, failure cases, and production checks."
excerpt: "Anthropic has moved agent-written workflows into its managed service. The useful part is parallel work in phases. The catch is a new control surface with hard limits, token costs, and several non-obvious failure modes."
---

## What Anthropic shipped on October 9

On October 9, 2026, Anthropic put dynamic workflows for Claude Managed Agents into public beta. A lead agent can now write a workflow program that launches many agents in phases, combines their results in code, and keeps the whole run moving on Anthropic's servers while the main session remains available for conversation. The headline ceiling is large: up to 64 threads working concurrently and 1,000 agents over the life of one run.

That does not make every prompt a candidate for a swarm. Dynamic workflows are meant for work that can be split into independent units and then recombined by an explicit rule. They also bring a less glamorous set of facts: the workflow code is not visible while it runs, an interrupted turn does not stop the run, and a run marked `completed` may still contain failed thread work.

Anthropic's [release notes](https://platform.claude.com/docs/en/release-notes/overview) describe this as a beta feature used with the `managed-agents-2026-04-01` beta header. The multi-agent setting is `{"type": "multiagent_20261001", "workflows": {"type": "enabled"}}`. Builders guide the feature through the system prompt and observe it through `workflow_run.*` events. There is no separate API call that directly starts a workflow run.

## Three handoffs: subagents, dynamic workflows, and advisor
<!-- INLINE_IMAGE_1 -->

The label "multi-agent" hides three different handoffs. Choosing among them matters more than simply turning the feature on.

**Subagents** are direct delegates. The session agent gives a task to a child thread, receives the result, and can send a follow-up. Anthropic caps this path at 25 child threads, one level deep. It fits work where the lead agent needs to inspect an answer, ask for a correction, or change direction before moving on.

**Dynamic workflows** are programs assembled by the agent. The program runs in the background, creates phases, starts working threads, and combines outputs. A thread's result goes back to that program, not straight to the agent running the session. The lead agent cannot send follow-up messages into those threads. Only the primary thread can start a run, so workflows cannot nest.

That separation is the central trade. The main agent is free to keep talking while the server executes a broader plan, but it has given the plan a degree of independence. Dynamic workflows suit audits, migrations, deep research, and cross-checking, according to Anthropic's [multi-agent orchestration guide](https://platform.claude.com/docs/en/managed-agents/multiagent-orchestration). In each case there are many pieces to inspect and a known way to merge their outputs.

**Advisor** is the lighter option. It lets an agent consult another agent during a turn without setting up a background workflow. Under `multiagent_20261001`, subagents and workflows are enabled by default. Advisor remains off until explicitly enabled.

There are two more configuration details worth keeping close. Inline agents use the session agent's model. Predefined agent lists can contain up to 20 definitions each for subagents and workflows. That makes predefined agents the place to constrain roles and, where appropriate, assign cheaper models to bulk phases, a choice that connects directly to the broader [price floor for smaller models](https://www.oguzhan.co/claude-haiku-5-5-gpt-6-luna-price-floor/).

## How Claude Managed Agents run a workflow
<!-- INLINE_IMAGE_2 -->

A run begins with a `user.message`. The lead agent decides whether to write and start a workflow; the application cannot invoke one through a dedicated start endpoint. The server then executes the generated program in the background.

Think of the program as plan-as-code. One phase might split a repository or document set into independent slices. Threads work on those slices, then their results return to the program. A later phase can cross-check, filter, or combine them. This is more structured than asking 20 agents the same broad question and hoping consensus appears.

The primary session does not have to sit silent during that process. Its agent can continue the conversation, while `workflow_run.*` events provide the application with run updates. The distinction is easy to miss: the session agent talks to the user, but each worker reports to the workflow program. It cannot receive a conversational nudge halfway through.

Claude Code has offered dynamic workflows since May 28, and they are now generally available there. The operating model is different. Claude Code produces a script on the local machine, where it can be read and edited. Claude Managed Agents creates a server-side program that the agent starts. The operator can supply guidance, set a budget, observe events, and ask the agent to stop a run, but cannot inspect the live workflow source. The practical workaround is to ask the agent to print the program afterward. That is an audit trail after execution, not control during execution.

This difference should shape the choice between products. A readable local script is easier to review before it touches tools. A managed run removes local orchestration work and can continue in the background. Convenience moved to the server. So did part of the control surface.

## What does a workflow run cost?

A workflow run has no separate sticker price. The bill has two parts: model tokens at the applicable model rates, plus the Claude Managed Agents session charge while the session remains in `running` status. A background run keeps that session running even during a period when no worker thread is active.

The comparable limits and charges are:

- Up to 64 threads can work at once, though the API does not guarantee that level of concurrency.
- Up to 1,000 agents can be created over one run's lifetime. Crossing that cap produces a `thread_limit_error`.
- A run has a default lifetime of 24 hours.
- A session has a default limit of 10 open runs.
- Session time costs $0.08 per hour while the session is running.
- A full 24 hours is about $1.92 in session time alone, before model tokens.
- Anthropic reported in 2025 that multi-agent systems used about 15 times the tokens of chats.
- In January 2026, Anthropic gave a range of 3 to 10 times the tokens of a single agent for equivalent tasks.
- The Batch API discount does not apply to Managed Agents sessions.

The token range is more useful than the session-hour charge when planning. Sixty-four concurrent threads are not a discount. They are 64 opportunities to make model requests quickly.

Budget behavior needs equal attention. A session budget must be set when the session is created; it cannot be added later. Runs pause when the budget is reached, but the final total can overshoot by one request for every thread that was working at that moment. With many active threads, the gap between the target and final spend can therefore be material even though the budget mechanism worked as documented.

This is where a simple question helps: can the work units and their combining rule be named before the run begins? If not, paying several times the token count may only produce several versions of the same uncertainty.

## The details that bite
<!-- INLINE_IMAGE_3 -->

The awkward cases are not buried edge conditions. They change how an application should report state, grant access, and recover from failure.

First, `completed` describes the workflow program's status. It does not certify that every worker succeeded or that the final result passed a quality check. Applications need their own acceptance checks and must inspect thread outcomes rather than turning the status label into a green badge.

Second, interrupting the agent turn does not interrupt the workflow run. The conversation can appear stopped while server-side work continues to consume time and tokens. Stopping has to be part of the operating procedure, not inferred from a cancelled response.

Third, the workflow program is invisible during execution. Event streams reveal activity, not the exact source now making decisions. That is a meaningful contrast with Claude Code's editable local script. Asking for the program after the fact helps diagnosis, but it does not provide preflight review.

Fourth, permission policies apply to the tools agents call. They do not govern the decision to start a workflow run. If starting a high-fan-out job needs approval in an application, that control must live outside the tool permission policy. This resembles a broader pattern in [agent failure modes](https://www.oguzhan.co/ai-agent-failure-modes-openai-review/): a control attached to individual actions does not necessarily constrain the process that schedules those actions.

Migration deserves a separate warning. Moving from `coordinator` without explicit settings enables workflows and inline agents by default under `multiagent_20261001`. A configuration change can therefore broaden behavior even if no prompt was rewritten. State the settings rather than inheriting them.

Finally, workers share a sandbox and work may run twice. Tool calls should be idempotent where possible, and each worker needs a separate output path. Otherwise a retry can duplicate an external action, or two correct workers can overwrite each other's files. The sandbox question is not cosmetic. Access boundaries are part of agent design, as the [Full Disk Access discussion](https://www.oguzhan.co/apple-full-disk-access-ai-agents/) shows in a different agent setting.

## When does a run earn its tokens?

Anthropic points to audits, migrations, deep research, and cross-checking. The common feature is not task size alone. It is separability.

A useful run has independent units such as files to audit, records to migrate, sources to research, or findings to verify. It also has a combining rule: deduplicate the findings, apply the migration in phases, compare citations, or require agreement before accepting a claim. Without both pieces, concurrency mostly buys speed in generating material that somebody still has to untangle.

One Anthropic test, reported by [The Decoder](https://the-decoder.com/anthropics-claude-can-now-orchestrate-up-to-1000-ai-agents-in-parallel-through-dynamic-workflows/), gives a striking example. Seventy bugs were hidden in a 116,000-line codebase. A single agent found 14 to 27 bugs per run; the dynamic workflow consistently found 66. The result is attributed to Anthropic, not an independent benchmark, and The Decoder says it is unknown whether the gain carries across task types. Test the workload you actually have.

The same report cites a senior OpenAI engineer calling agent swarms a massive waste of tokens, without naming the engineer. That criticism and Anthropic's bug hunt can both be true. Parallel search can pay when coverage matters and the search space divides cleanly. It can waste money when a [chatbot is already enough](https://www.oguzhan.co/what-is-agentic-ai-when-chatbot-enough/), when workers depend on each other's intermediate answers, or when no automated check can distinguish a good merge from a fluent one.

My rule of thumb is deliberately plain: write down the independent units and the combining rule in one sentence each. If either sentence stays vague, keep the run small or use a subagent. Agent count is not a quality metric.

## Before the first production run

- Enable `multiagent_20261001` explicitly and state whether workflows, subagents, and advisor are on.
- Put guidance for when to create a workflow in the system prompt.
- Set the session budget at creation time, with room for one-request-per-working-thread overshoot.
- Start below the concurrency ceiling and test the actual workload.
- Define success independently of the `completed` status.
- Consume `workflow_run.*` events and expose run state to operators.
- Give every worker a distinct output path in the shared sandbox.
- Make external tool operations idempotent, because work can execute twice.
- Add an explicit procedure to stop the run; cancelling a turn is not enough.
- Decide whether server-side, temporarily invisible workflow code meets the review requirement. Use Claude Code when an editable local script is the better fit.
- After a trial, inspect the printed workflow, thread failures, token use, session time, and output quality before raising limits.

Public beta is the right label. The mechanism can turn a carefully divisible job into a controlled background program, and Anthropic has supplied substantial ceilings for it. Production readiness, though, comes from the smaller controls around that program: budget set early, permissions understood correctly, outputs isolated, and completion verified rather than assumed.

## Sources

- [Anthropic, Claude Platform release notes](https://platform.claude.com/docs/en/release-notes/overview)
- [Anthropic, Multi-agent orchestration](https://platform.claude.com/docs/en/managed-agents/multiagent-orchestration)
- [Vanja Petreski, Managed Agents dynamic workflows](https://vanja.io/managed-agents-dynamic-workflows/)
- [The Decoder, Anthropic's Claude can orchestrate up to 1,000 agents](https://the-decoder.com/anthropics-claude-can-now-orchestrate-up-to-1000-ai-agents-in-parallel-through-dynamic-workflows/)
