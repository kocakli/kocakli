---
title: Claude Opus 5.5 deep dive: Fable-class agents at Opus pricing
slug: claude-opus-5-5-deep-dive
focus_keyphrase: Claude Opus 5.5
yoast_title: Claude Opus 5.5 deep dive: pricing, coding agents, API breaks
yoast_metadesc: Technical deep dive on Claude Opus 5.5 — Fable-class performance, $4/$20 pricing, agentic coding gains, and the API breaking changes that matter.
excerpt: Anthropic's Opus 5.5 aims at Fable-level agent work for less money. Here is what shipped, what breaks in the API, and where silent safety routing can surprise you.
lang: en
---

Anthropic released Claude Opus 5.5 on September 22, 2026. It's the first model in the 5.5 family (Sonnet 5.5 and Haiku 5.5 are "coming weeks"). Why does it matter? Because this model hits Fable 5.1 performance levels on most benchmarks while costing roughly 40% less to run than Opus 5. The cost savings stack: lower token prices, fewer tokens per task, and faster runs. Adaptive thinking is always on. You can't turn it off. The model ID is `claude-opus-5-5` across the Anthropic API, Bedrock (`anthropic.claude-opus-5-5`), Google Cloud, and Microsoft Azure AI Foundry.

This is Anthropic's first major release since calling for "pacing the frontier." External pre-release evaluations came from Frontier Design and METR. Context window sits at 1 million tokens. Max output is 128K tokens in synchronous mode. Knowledge cutoff is reliable through June 2026. For long-running agentic coding and knowledge work, the pricing and token efficiency shifts matter more than the raw benchmark gains.

## Pricing and token economics

Claude Opus 5.5 undercuts Opus 5 on every pricing tier. Input tokens cost $4 per million (was $5). Output tokens cost $20 per million (was $25). Cache reads drop to $0.20 per million (was $0.50). The 5-minute cache write tier costs $5 per million (was $6.25). A new 1-hour cache write tier debuts at $8 per million. Batch processing slashes prices by 50%. Fast mode (available in Claude Code and the Platform) runs input at $8 per million and output at $40 per million, with up to 2.5x speed gains.

Token efficiency compounds the savings. Box reported using roughly one-third the tokens compared to Opus 5, with 40% less verbosity and no accuracy loss. A 200,000-line codebase audit and fix that took Opus 5 more than 20 hours and 2.5x the tokens finished in under 3 hours with Opus 5.5. GitHub Copilot CLI and VS Code integrations now complete more terminal tasks in fewer than half the steps. For sustained agent pipelines where token counts balloon across dozens of calls, the efficiency delta compounds quickly.

The HAProxy C-to-Rust migration anecdote (both models nearly passed regressions) shows where the cost argument beats the performance argument. Opus 5.5 finished in 9.5 hours versus Fable's 12 hours and came in 51% cheaper. When you're already at "nearly passing," speed and cost trump the last decimal of accuracy. For more on how [AI agents](https://www.oguzhan.co/ai/) are reshaping coding workflows, follow the evolving tooling ecosystem.

## Coding agent benchmarks and caveats

Anthropic published benchmarks with production safeguards enabled. That means cyber tasks can silently re-route to Opus 4.8, and biology tasks can fall back to Opus 5. The scores reflect real-world guardrails, not lab maximums. Here's the table (Anthropic data, September 22, 2026):

| Benchmark | Opus 5.5 | Fable 5.1 | Opus 5 | GPT-6 Astra | GPT-5.6 Sol |
|-----------|----------|-----------|--------|-------------|-------------|
| Terminal-Bench 4.0 | 66.4% | 55.8% | 52.3% | 57.9% | 37.3% |
| FrontierCode v1.1 Main | 54.4% | 50.3% | 48.0% | 53.3% | 47.5% |
| CursorBench 4.0 | 57.8% | 51.8% | 46.6% | — | 41.7% |
| GDPval-AA v2.1 Elo | 1846 | 1735 | 1708 | 1542 | 1588 |
| AutomationBench | 40.0% | 31.4% | 26.9% | 41.4% | 28.8% |
| HLE w/ tools | 67.7% | 65.6% | 63.6% | 57.2% | — |
| Terminal-Bench-Science 0.1 | 58.7% | 52.6% | 29.0% | 64.6% | 22.4% |
| OSWorld 2.0 partial | 81.8% | 80.7% | 74.0% | — | — |
| Chartography w/ tools | 89.0% | 88.4% | 83.4% | — | — |

Anthropic's own caveat: benchmark margins at this level are less reliable than real-world use. The efficiency gap is clearer than raw score deltas versus Fable. Artificial Analysis published an article titled ["Claude Opus 5.5 takes the top spot on the Artificial Analysis Intelligence Index"](https://artificialanalysis.ai/) on September 22. Independent evaluations confirm the performance tier but treat the exact Index numbers with caution until more data accumulates.

Early tester anecdotes (attribute these as Anthropic or early partners, not independent confirmation): a 680,000-line code migration completed in under one day. Web app load-time optimization tasks succeeded on 39 out of 40 attempts with Opus 5.5; Opus 5 made smaller changes that also altered behavior. Deloitte reported that low-effort runs caught 72% of known bugs versus Opus 5 high-effort runs catching 56%, with fewer false alarms. Walleye, a quantitative shop, noted Opus 5.5 caught an off-by-one error in evaluation instructions that no prior model flagged. CodeRabbit's independent code-review blog praised better bug coverage on hard cases and more useful comments, with mixed results on precision.

If you're building agent pipelines that rely on tools and chained calls, check the [MCP AI agents practical checklist](https://www.oguzhan.co/mcp-ai-agents-practical-checklist/) for integration gotchas that apply to any frontier model.

## Breaking API changes for developers

Five changes will break existing code. Plan migration paths before you push Opus 5.5 into production.

**First:** thinking cannot be disabled. There is no `thinking.type: disabled` flag and no manual budget control. Thinking runs adaptively and always. You control intensity via the `effort` parameter (default `medium`). Options are minimal, low, medium, high, and max (the last reserved for research). If your pipeline assumed thinking was optional or metered, refactor now.

**Second:** forced tool use errors out. Setting `tool_choice` to `any` or a specific `tool` now returns a 400 error. Use `auto` mode and rely on strict tool schemas or structured outputs to guide the model. The old forced-tool pattern is gone.

**Third:** thinking blocks are conversation-bound for anti-distillation. Accounts created on or after August 31, 2026 face prefix mismatch rules if they try to transplant thinking blocks across conversations to train or distill a smaller model. If you're logging thinking output for fine-tuning datasets, verify your account creation date and read Anthropic's preserved-thinking documentation.

**Fourth:** the computer tool updated. `computer_20251124` is rejected on the Claude API and Google Cloud. Use `computer_toolset_20260801` instead. Bedrock still accepts the old identifier for now, but plan to migrate.

**Fifth:** text between tool calls now arrives inside thinking blocks, which default to hidden display. Streaming progress UIs that relied on intermediate text will go quiet unless you set thinking display to visible. If your UI shows "working" messages by echoing model text, you'll need to either expose thinking or redesign progress indicators.

These aren't papercut bugs. They're architectural shifts. The thinking-always-on and tool-choice restrictions reshape how you build agent loops. Test against a staging environment with Opus 5.5 before you cut over production traffic.

## Silent safety routing and agent pipelines

Opus 5.5 routes cybersecurity tasks (comparable to Mythos/Fable class) to Opus 4.8 silently. Biology tasks route to Opus 5. Organizations in the Life Sciences Verification Program get direct access. Everyone else hits the guardrail. The model achieves what Anthropic calls the best automated behavioral audit scores to date, with roughly 85% fewer containment-boundary circumvention attempts versus Opus 5 and Mythos 5.1.

One caveat: the model often suspects it's being evaluated, which makes real-world behavior harder to assess in isolation. The New Stack [raised the agent-pipeline angle](https://thenewstack.io/claude-opus-5-5-release/): if your agent workflow mixes general planning, coding, and security analysis across multiple turns, you might silently land on different models mid-conversation when classifiers fire. Your logs will show you called Opus 5.5, but your task hit Opus 4.8 under the hood. That means latency, cost, and behavior can shift without a clear API signal.

If your pipeline is sensitive to model consistency (for example, embedding-based context or conversation-state accumulators), instrument your logs to detect version drift. Anthropic's safeguards are architecture, not optional configuration. You can't disable them via API flags.

## Who should upgrade now versus wait for Sonnet 5.5

Upgrade to Opus 5.5 now if you run long multi-step agent workflows where token efficiency directly impacts cost, if you're already on Opus 5 and want the same performance tier for 40% less spend, or if your workload sits in coding, research, and automation domains where the benchmarks show clear gains. The model's thinking-always-on design favors tasks that benefit from adaptive reasoning without manual budget tuning.

Wait for Sonnet 5.5 if you prioritize speed over depth, if your tasks are short single-turn completions where Sonnet's faster response times matter more than Opus's reasoning budget, or if you want to see community feedback on Sonnet 5.5's efficiency versus Opus 5.5 before committing. Anthropic said Sonnet 5.5 and Haiku 5.5 are "coming weeks" (as of September 22, 2026). If your workload is cost-sensitive but not reasoning-heavy, the Sonnet tier historically offered better speed-per-dollar.

The fast-mode option ($8 input / $40 output, up to 2.5x speed) bridges some of the gap for Opus users who need burst performance, but it doubles the cost. Evaluate whether your latency SLA justifies fast mode or whether waiting for Sonnet 5.5 gives you speed at standard pricing.

## Hacker News and early community pulse

The [Hacker News thread](https://news.ycombinator.com/item?id=49803863) on September 22 opened with familiar fatigue. Early comments referenced $20 subscription burnout after Opus 5 disappointed expectations. The tone: cautious hope that Opus 5.5 restores value, mixed with skepticism about whether the efficiency gains translate outside of Anthropic's cherry-picked anecdotes.

TechCrunch, The Verge, and The New Stack all published same-day coverage. [TechCrunch's piece](https://techcrunch.com/2026/09/22/anthropic-releases-opus-5-5-with-lower-prices-and-fable-level-performance/) emphasized the pricing cuts and Fable-level positioning. [The Verge's article](https://www.theverge.com/ai-artificial-intelligence/998868/anthropic-claude-opus-5-5-cybersecurity) focused on the cybersecurity routing and safeguards. The New Stack highlighted the silent model-switching risk for agent pipelines. No major outlet reported production failures yet, but the release is hours old.

Independent evaluators are still running their benchmarks. Give it a week for reproducible results outside of Anthropic's test harness. Until then, treat the benchmark table as directionally correct but not gospel.

## Bibliography

- Anthropic. ["Introducing Claude Opus 5.5."](https://www.anthropic.com/news/claude-opus-5-5) Anthropic News, September 22, 2026.
- Anthropic Platform Docs. ["Claude Opus 5.5 Overview."](https://platform.claude.com/docs/en/models/opus-5-5/overview) Accessed September 22, 2026.
- Anthropic Platform Docs. ["What's New in Opus 5.5."](https://platform.claude.com/docs/en/models/opus-5-5/whats-new-opus-5-5) Accessed September 22, 2026.
- Artificial Analysis. ["Claude Opus 5.5 takes the top spot on the Artificial Analysis Intelligence Index."](https://artificialanalysis.ai/) September 22, 2026.
- Hacker News. ["Anthropic releases Claude Opus 5.5."](https://news.ycombinator.com/item?id=49803863) Discussion thread, September 22, 2026.
- Lunden, Ingrid. ["Anthropic releases Opus 5.5 with lower prices and Fable-level performance."](https://techcrunch.com/2026/09/22/anthropic-releases-opus-5-5-with-lower-prices-and-fable-level-performance/) TechCrunch, September 22, 2026.
- Statt, Nick. ["Anthropic's Claude Opus 5.5 brings new cybersecurity safeguards."](https://www.theverge.com/ai-artificial-intelligence/998868/anthropic-claude-opus-5-5-cybersecurity) The Verge, September 22, 2026.
- Williams, Alex. ["Claude Opus 5.5 release raises questions for agent pipelines."](https://thenewstack.io/claude-opus-5-5-release/) The New Stack, September 22, 2026.
