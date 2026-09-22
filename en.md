---
title: "MCP for AI agents: the practical checklist before you wire tools"
slug: "mcp-ai-agents-practical-checklist"
focus_keyphrase: "MCP AI agents"
yoast_title: "MCP AI agents: practical checklist for tools and governance"
yoast_metadesc: "What Model Context Protocol does for AI agents, why enterprises put policy on MCP, Plugin4Shell pinning risk, and a desk checklist before you wire tools."
excerpt: "MCP moved from “nice tool bus” to the place enterprises enforce agent limits. Here is a desk checklist before you connect coding agents to the real world."
lang: en
---

MCP AI agents can look deceptively tidy on a diagram: a model, a protocol, a row of tools. Then the agent receives a real identity, reaches a repository, and runs code with somebody's privileges. September supplied the missing labels for that diagram. Enterprises put policy controls on the MCP layer, Microsoft showed how to remove nested model loops, and Plugin4Shell exposed a pin that did not really pin. The useful question is no longer whether an agent can call a tool. It is what must be true before that call is allowed.

## What MCP actually carries

Model Context Protocol is a common way to expose tools and resources to an AI application through JSON-RPC. It began at Anthropic. [Forkast's account of the CNCF discussion](https://forkast.news/cncf-evaluates-mcp-as-the-cloud-native-agent-wire-spec-and-the-standardization-arc-just-reached-infrastructure/) says MCP is hosted by the Linux Foundation's Agentic AI Foundation and describes JSON-RPC 2.0 over HTTPS or streamable HTTP. CNCF's Technical Oversight Committee is evaluating it as a wire specification for distributed agent systems on Kubernetes. That is an ongoing evaluation, not a finished coronation.

The protocol standardizes the wire. It does not decide whether `delete_repository` should exist, which agent may invoke it, how narrow its token should be, or whether fetched plugin code matches the commit the operator approved. Those decisions remain with the people building and operating the system.

That distinction matters. A neat tool schema can make a dangerous operation easier to discover. It cannot make the operation safe.

## MCP AI agents acquired a policy layer

[Forkast reported three enterprise releases in one September week](https://forkast.news/mcp-is-becoming-the-governance-surface-three-enterprise-vendors-shipped-policy-enforcement-through-the-protocol-this-week/). Read together, they point in the same direction: policy is moving onto the route between an agent and its tools.

On September 10, ServiceNow AI Gateway v3.4 added MCP runtime enforcement and server lifecycle controls. Administrators can define which MCP servers, tools, and resources an agent may use at the gateway layer.

Around September 15, Rubrik introduced an MCP offering co-engineered with Anthropic. Forkast describes guardrails aligned with the OWASP MCP Top 10, scoped short-lived tokens for each tool call, and Rubrik Agent Identity federation with Okta or Entra. Its stated access model gives agents the same RBAC boundaries as people.

On September 17, Microsoft announced the Entra Agent ID MCP Firewall in Global Secure Access. It discovers MCP servers, blocks unknown ones, and permits granular policies at the method level. That discovery step is important. An allowlist cannot govern a server the security team does not know exists.

Forkast, citing a 2026 Okta survey, also reports that 67% of workers use unapproved AI tools and 92% of executives say autonomous agents are in widespread use. The article does not provide survey methodology in the material cited here, so those figures are a signal, not a risk model. The product sequence is more concrete. ServiceNow controls the available surface, Rubrik narrows identity and credentials, and Entra looks for the unregistered route.

Cisco's Agent Runtime SDK sits on the build-time side in Forkast's broader account, while NVIDIA OpenShell and WSO2 Agent Manager address runtime concerns. That larger stack may grow. The immediate operator job is smaller: know every MCP route and put an enforceable decision in front of it.

## A specialist may not need another model loop

Microsoft published a second useful pattern on September 16. In [Tommaso Stocchi's Agent Framework demonstration](https://devblogs.microsoft.com/agent-framework/from-specialist-agents-to-distributed-skills-over-mcp/), a specialist publishes a description, a `SKILL.md` file, and typed MCP tools. The parent advisor loads the instructions and calls those tools inside its own model context.

Domain services remain distributed. Reasoning moves back to the advisor.

In the example, the skills path loads `weather` and `lift-traffic`, makes direct MCP calls, and writes the final answer. It does not start nested specialist model loops. Microsoft Agent Framework implements the pattern with `SkillsProvider`, `MCPSkillsSource`, and `SkillToolsMiddleware`.

The demo's exact prompt was: “considering weather and waiting time, where should i start?” Here is the author's three-pair illustration:

| Pair | A2A model calls | A2A elapsed | Native MCP skills calls | Native MCP skills elapsed |
|---|---:|---:|---:|---:|
| 1 | 6 | 16.416 s | 3 | 8.661 s |
| 2 | 6 | 12.835 s | 3 | 5.866 s |
| 3 | 7 | 17.188 s | 3 | 4.517 s |
| Mean | | 15.480 s | | 6.348 s |

The tempting headline is “half the latency.” Do not ship that claim.

These runs used `gpt41`, reused processes, and were affected by cache state. The author says the illustration does not isolate architecture from credential initialization, language runtime, caching, or unequal work. It is not a controlled study or a billable-dollar comparison. Tokens even moved the other way: the skills route consumed 13,533 tokens across three runs versus 11,134 for A2A, roughly 22% more.

There is a versioning footnote too. The demo follows a pinned historical SEP-2640 draft using `skill://index.json`. At the author's September 10 check, newer `skills/list` and `skills/get` methods were still unsettled. Treat distributed skills as a draft extension track, not universal core MCP behavior.

The pattern is still worth testing. Fewer model loops can mean fewer independent reasoning boundaries to inspect. But measure your own latency, token use, initialization cost, and failure paths. Microsoft's table is a hypothesis generator, not a capacity plan.

## Plugin4Shell: when a SHA is read as a branch

Plugin4Shell attacks the gap between what an agent records and what Git checks out. According to [The Hacker News report on Air Security's research](https://thehackernews.com/2026/09/plugin4shell-lets-repository-owners.html), affected coding agents pin a plugin to a commit SHA but fail to verify that the resulting working tree matches that commit.

On Git hosts that permit a branch name shaped like a commit hash, a repository owner can create such a branch and point it to different code. Bitbucket and self-hosted instances may allow the name. GitHub blocks hash-shaped branch and tag names, which narrows the GitHub-hosted case. Gemini CLI has a related variant involving the `FETCH_HEAD` branch name.

The loaded plugin runs with the user's privileges. Built-in marketplaces hosted on GitHub auto-update by default, while non-GitHub plugin hosts retain the relevant exposure described in the report. “Pinned” is therefore not enough evidence. The checkout has to be verified.

The status as reported on September 18 was uneven:

| Coding agent | Plugin4Shell status |
|---|---|
| Claude Code | Fixed in 2.1.179 and later, according to Air Security; Anthropic release notes may not mention it |
| Codex | Fixed in 0.146.0; the OpenAI pull request describes Git interpreting a SHA as a branch name |
| GitHub Copilot | No fix reported in the article |
| Gemini CLI | Will not be fixed; Google points users to Antigravity, the consumer CLI stopped in June, and the enterprise CLI may continue |

Air found the issue in May 2026, disclosed it in June, and the research became public around September 17 to 18. The Hacker News found no CVE, no vendor advisories, and no known exploitation in the wild at its September 18 check. Do not turn absence of a CVE into absence of risk. Also do not turn a proof of concept into an incident that the source did not report.

## The pre-wire desk checklist

Before connecting an agent to production tools, I would require a written answer for each line:

1. **Inventory the route.** Record every MCP server, owner, transport, tool, and resource. Add discovery for unregistered or “shadow” MCP servers, then block unknown endpoints.
2. **Allowlist at tool and method level.** Approving a server is too broad if one harmless read sits beside a destructive write. Keep the callable set small.
3. **Give the agent its own identity.** Do not hide agent traffic inside a shared human credential. Apply the same RBAC boundary a human would receive for the task.
4. **Scope credentials per call.** Prefer short-lived tokens restricted to the selected tool and operation. A token that outlives the job becomes spare authority.
5. **Pin and verify code.** Update Claude Code to 2.1.179 or later and Codex to 0.146.0 or later where applicable. For every plugin source, resolve the intended object and verify the working tree matches it. Treat non-GitHub hosts as a separate review case.
6. **Test the failure path.** Deny an unknown server, a forbidden method, and an expired token. Confirm the agent stops cleanly instead of finding another route.
7. **Log the decision, not just the call.** Keep the agent identity, server, method, credential scope, policy result, and code revision that actually ran.
8. **Benchmark the full job.** Count model calls, tool calls, elapsed time, tokens, initialization, and retries. If adopting distributed skills, compare against the nested-agent design under matched cache and process conditions.
9. **Set an update owner.** Plugin marketplaces and MCP servers change. Name the person or team that reviews new versions, advisories, and permission drift.

For adjacent operational controls, the [AI hub](https://www.oguzhan.co/ai/) collects the wider thread. The recent [agent sandbox breakout digest](https://www.oguzhan.co/ai-digest-20-sep-2026-ai-agent-sandbox-breakout/) covers why process isolation still matters after tool policy, while the [misalignment reporting framework for operators](https://www.oguzhan.co/openai-misalignment-reporting-framework-for-operators/) addresses escalation when behavior crosses a defined line.

## What the protocol cannot clean up for you

A perfect allowlist still permits an approved tool to receive a bad argument. A valid identity can hold excessive rights. A verified plugin can contain intentionally harmful code. A short-lived token can be dangerous for every second of its life.

MCP is useful because it creates a visible junction. That junction can host discovery, identity checks, method policy, and audit records. September's releases make that operational model easier to see. Plugin4Shell supplies the counterexample: a control label such as “SHA pinned” means little when the system does not verify the object underneath it.

Wire fewer things. Name their owners. Verify what ran. Then let the agent call.
