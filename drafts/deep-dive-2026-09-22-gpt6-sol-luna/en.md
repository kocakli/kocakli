---
title: "GPT-6 Sol and Luna: OpenAI's cost curve after Astra"
slug: gpt-6-sol-luna-deep-dive
focus_keyphrase: GPT-6 Sol
yoast_title: "GPT-6 Sol and Luna deep dive: pricing, coding, agents"
yoast_metadesc: "Technical deep dive on GPT-6 Sol and Luna — $2/$10 and $0.10/$0.50 pricing, 1.05M context, coding and agent gains after GPT-6 Astra."
excerpt: "OpenAI expands GPT-6 beyond Astra with Sol and Luna. Here is the price ladder, what Sol is for, when Luna wins, and how this lands next to Claude Opus 5.5."
lang: en
---

OpenAI shipped GPT-6 Sol and GPT-6 Luna on September 22, 2026. Both models cut prices by 50% compared to GPT-5.6 promotional rates while delivering measurable gains on coding, agent, and factuality benchmarks. **GPT-6 Sol** costs $2 per million input tokens and $10 per million output tokens. It slots between Astra (the flagship) and Luna (the volume workhorse) in a three-tier lineup that now covers everything from high-stakes cyber work to parallel subagent runs. The [official announcement](https://openai.com/index/introducing-gpt-6-sol-and-luna/) frames Sol and Luna as cost-intelligence frontier pushers, built from the same training lineage as Astra but tuned for price-sensitive workflows where Astra would burn budget and Luna would sacrifice too much capability.

Same-day context matters. Anthropic released Claude Opus 5.5 a few hours earlier at $4 input and $20 output per million tokens. That puts **GPT-6 Sol** at half the input price and half the output price of Opus 5.5, while OpenAI's vendor benchmarks claim Sol xhigh beats Opus 5 max on professional automation tasks at roughly one-ninth the cost per task. Artificial Analysis published fresh evaluations for both **GPT-6 Sol** (across all reasoning-effort levels) and Opus 5.5 on September 22, and their Intelligence Index headline now shows Opus 5.5 at the top. We will discuss the competitive frame later without inventing head-to-head scores.

## Price ladder and context

Here is the full GPT-6 pricing table (per 1M tokens, standard tier):

| Model | Input | Output | Context | Max output | Knowledge cutoff |
|---|---|---|---|---|
| **GPT-6 Sol** | $2 | $10 | 1,050,000 | 128,000 | April 20, 2026 |
| **GPT-6 Luna** | $0.10 | $0.50 | 1,050,000 | 128,000 | May 18, 2026 |
| GPT-6 Astra | $10 | $50 | 1,050,000 | 128,000 | (flagship) |

Every tier shares the same 1.05M token context window. That is enough for dozens of long files, full repo snapshots, or multi-turn agent sessions without repeated re-ingestion. Max output is 128,000 tokens across the board.

Cache discounts apply to both Sol and Luna. Cached input reads cost 10% of uncached (Sol $0.20, Luna $0.01). Cache writes cost 1.25x uncached input (Sol $2.50, Luna $0.125). Prompts over 272K tokens trigger a 2x multiplier on input and cache costs plus 1.5x on output for the full request. Batch API and Flex mode deliver 50% off standard pricing; Fast mode doubles the rate.

OpenAI claims higher default cache hit rates now, and they added a Prompt Caching Dashboard with diagnostics. GitHub Copilot saw a reduction of more than 50% in fresh-processed prompt share over several months after rolling out caching optimizations. That matters when you multiply agent loops by hundreds of parallel runs.

## GPT-6 Sol for coding and agents

**GPT-6 Sol** is OpenAI's new workhorse for complex coding and agentic workflows. It sits at $2/$10, half the cost of Opus 5.5, and delivers substantial gains over GPT-5.6 Sol in the same price tier.

### Coding benchmarks (OpenAI-reported)

**FrontierCode:** Sol shows substantial improvement over GPT-5.6 Sol and matches Claude Fable 5.1 xhigh at much lower cost (OpenAI claim; exact numbers not published).

**DeepSWE v1.1:** GPT-6 Sol max scores 68.8%, close to Fable 5 xhigh at 69.9%, but Sol runs at roughly 80% lower cost per task according to OpenAI's comparison table.

Luna also performs well. GPT-6 Luna max hits 66.6%, comparable to Claude Opus 5 and Fable 5 medium, while costing 93 to 96 percent less per task in those comparisons.

### Agent and automation benchmarks (vendor-reported)

**AutomationBench (professional tasks):** GPT-6 Sol xhigh scores 33.2% at $0.27 per task. That beats Claude Opus 5 max (26.9%) at roughly 9% of Opus 5 max cost per task. OpenAI's table reports Opus 5 max as 11.1x Sol xhigh cost. Sol xhigh also exceeds Astra low (30.3%) at far lower total cost.

Luna high delivers a +5.4 percentage-point gain over its predecessor at 58% lower cost per task.

**Agents' Last Exam:** Sol max scores 56.4%, above Claude Opus 5's highest effort level in that eval, and does so at 60% lower cost per task.

**Computer use (OSWorld 2.0 offline):** Sol xhigh reaches approximately 60.5%, similar to Opus 5 medium at 60.3%, but at roughly 80% lower cost. Luna max exceeds GPT-5.6 Sol medium at one-tenth the cost.

All numbers in this section are OpenAI-reported. Treat them as vendor claims pending independent replication.

### Factuality

OpenAI evaluated factuality on error-flagged ChatGPT conversations (a skewed sample by definition). Sol makes roughly half the mistakes of its predecessor and approaches Astra reliability at lower cost. Luna high effort can match GPT-5.6 Sol factuality at approximately 1/100 the cost, according to OpenAI.

### Communication improvements

Astra introduced clearer communication, less jargon, and shorter responses without losing substance. Sol and Luna port those improvements. You get Astra-style output at Sol and Luna prices.

## Luna for volume and subagents

**GPT-6 Luna** costs $0.10 input and $0.50 output per million tokens. That is 50% below GPT-5.6 Luna promotional pricing and 95% cheaper than Sol on input. Luna is built for high-volume workloads, parallel subagent runs, focused single-turn tasks, and any workflow where you need thousands of requests per hour without burning through budget.

Luna shares the same 1.05M context and 128K max output as Sol and Astra. It supports the same reasoning-effort ladder (none, low, medium default, high, xhigh, max) and the same [Responses API](https://developers.openai.com/api/docs/models/gpt-6-luna) tool surface (web search, file search, image generation, code interpreter, hosted shell, apply patch, skills, computer use, MCP, tool search). The only functional difference is capability and speed. Luna is faster and cheaper; Sol is more capable.

Use Luna when:

- You need to fan out hundreds of parallel classification, extraction, or search tasks.
- Each task is well-scoped and does not require deep reasoning.
- You are orchestrating multi-agent systems where subagents handle narrow subtasks and a coordinator (running Sol or Astra) synthesizes results.
- Cost per task matters more than marginal accuracy gains.

Luna high can match GPT-5.6 Sol factuality at 1/100 the cost. Luna max delivers coding and agent performance comparable to prior-generation flagship-tier models at a fraction of the price. That makes Luna viable for code review, test generation, and documentation work when you tune prompts carefully and accept slightly lower ceiling performance.

## Reasoning effort, caching, and Responses API tools

Both Sol and Luna expose six reasoning-effort levels: none, low, medium (default), high, xhigh, and max. Higher effort consumes more tokens and takes longer but improves performance on hard tasks. The Chat Completions API supports function calling only when `reasoning_effort` is set to `none`. For tool-rich workflows, use the [Responses API](https://developers.openai.com/api/docs/models), which bundles tool calling natively.

The Responses API surface includes:

- Web search
- File search (vector retrieval over uploaded files)
- Image generation (DALL·E integration)
- Code interpreter (Python sandbox)
- Hosted shell (persistent container)
- Apply patch (code edits)
- Skills (reusable agent modules)
- Computer use (GUI automation via OSWorld-style interface)
- MCP (Model Context Protocol for third-party integrations)
- Tool search (discover and invoke available tools)

All tools work on Sol and Luna. Astra gets the same set. The difference is cost and capability, not access.

Caching preserves state across effort-level and tool toggles. If you switch from medium to high effort on the same cached prompt, the cache hit still applies. That makes it cheaper to experiment with effort levels during development.

## Same-day competitive frame: GPT-6 Sol vs Claude Opus 5.5

Anthropic shipped Claude Opus 5.5 on September 22, 2026, a few hours before OpenAI announced Sol and Luna. Opus 5.5 costs $4 input and $20 output per million tokens. **GPT-6 Sol** costs $2 input and $10 output. Both models support large context windows (Opus 5.5 at 1M+, Sol at 1.05M). Both claim gains in coding, reasoning, and agent tasks over prior generations.

Artificial Analysis published fresh evaluations for GPT-6 Sol (across all reasoning-effort levels, including non-reasoning mode) and Claude Opus 5.5 on September 22. Their Intelligence Index headline now lists Opus 5.5 at the top. We do not have Artificial Analysis numerical scores for Sol yet beyond that headline result. Do not invent Index scores. Independent evaluation matters, and the September 22 AA drop is the current authoritative third-party signal.

OpenAI's vendor benchmarks claim Sol xhigh beats Opus 5 max on AutomationBench at one-ninth the cost per task. But that comparison uses Opus 5, not Opus 5.5. Anthropic has not published Opus 5.5 AutomationBench scores. We cannot make a direct Sol-vs-5.5 claim on that eval yet.

Here is what we do know:

- **Price:** Sol is half the cost of Opus 5.5 on input and output.
- **Context:** Both support ~1M+ tokens.
- **Tools:** Both expose web search, file handling, code execution, and computer use in some form.
- **Coding:** OpenAI reports DeepSWE v1.1 Sol max at 68.8%. Anthropic has not published Opus 5.5 DeepSWE scores.
- **Computer use:** Sol xhigh scores ~60.5% on OSWorld 2.0 offline. Opus 5.5 computer-use benchmarks are not yet public.

The competitive frame is price-performance positioning, not a direct head-to-head knockout. Sol undercuts Opus 5.5 by 50% on price. Opus 5.5 leads the Artificial Analysis Index. Both models advanced the frontier. Choose based on your cost tolerance, tool ecosystem lock-in, and whether you need the absolute best (Opus 5.5 or Astra) or the best value (Sol or Luna).

For practical migration guidance, see the next section.

## Migration advice: when to use Astra, Sol, or Luna

**Use Astra** when absolute capability matters more than cost. Astra is the flagship. It leads OpenAI's lineup on challenging evals (cyber Critical, math, computer use at max difficulty). If you are building a production system where errors are expensive or where you need the highest reliability OpenAI ships, pay the $10/$50 rate and use Astra. Typical use cases: high-stakes cyber defense, formal verification, research-grade math, and critical infrastructure automation.

**Use GPT-6 Sol** for complex coding, agent orchestration, and workflows where you need strong reasoning but cannot justify Astra pricing. Sol costs one-fifth of Astra on input ($2 vs $10) and output ($10 vs $50). It delivers Astra-style communication improvements and approaches Astra factuality. OpenAI's benchmarks show Sol xhigh beating Astra low on AutomationBench while costing far less. Sol is the workhorse tier. Typical use cases: production code generation, PR review, test synthesis, multi-step agent workflows, customer support automation, and document analysis at scale.

**Use GPT-6 Luna** when you need volume, speed, or parallel subagent runs. Luna costs $0.10/$0.50, twenty times cheaper than Sol on input and twenty times cheaper on output. Luna high can match GPT-5.6 Sol factuality at 1/100 the cost. Luna max delivers coding performance comparable to prior flagship-tier models. Typical use cases: batch classification, entity extraction, summarization pipelines, subagent fan-out in hierarchical agent systems, A/B test generation, and any workflow where you run thousands of requests per hour and cost-per-task dominates total expense.

**Cache aggressively.** All three tiers offer 90% discounts on cached input reads. If you are running agent loops, caching the system prompt, repo context, or conversation history can cut costs by an order of magnitude. Use the Prompt Caching Dashboard to monitor hit rates and identify cache-unfriendly prompt patterns.

**Tune effort levels.** Sol and Luna default to medium reasoning effort. Dropping to low or none speeds inference and reduces token consumption. Raising to high, xhigh, or max improves accuracy on hard tasks but costs more. Profile your workload, measure task success rate at each effort level, and pick the lowest level that meets your quality bar.

**Mix tiers in the same system.** A common pattern: Astra or Sol runs the main agent loop and makes high-stakes decisions; Luna handles parallel subtasks like file parsing, data normalization, or candidate generation; Sol or Astra synthesizes Luna's output into a final result. This hybrid approach keeps total cost low while preserving quality where it matters.

## What just shipped

OpenAI expanded GPT-6 from a single flagship (Astra) to a three-tier lineup. **GPT-6 Sol** delivers strong coding and agent performance at $2/$10, half the cost of Claude Opus 5.5 and one-fifth the cost of Astra. GPT-6 Luna pushes the volume tier to $0.10/$0.50, enabling subagent-heavy workflows and high-throughput batch processing. Both models share Astra's 1.05M context, 128K max output, six reasoning-effort levels, and full Responses API tool surface. Caching discounts are 90% on reads, and OpenAI reports higher default hit rates now.

Artificial Analysis evaluated both Sol and Opus 5.5 on September 22. Opus 5.5 leads their Intelligence Index. OpenAI's vendor benchmarks claim Sol xhigh beats Opus 5 max on professional automation at one-ninth the cost per task. Independent replication will clarify where each model truly lands.

The tier expansion matters. Before Sol and Luna, you chose between Astra at $10/$50 and GPT-5.6-generation models at higher prices than today's equivalents. Now you can run production agentic systems on Sol, fan out subagent work to Luna, and reserve Astra for the hardest 5% of tasks. That cost structure makes [AI agent workflows](https://www.oguzhan.co/mcp-ai-agents-practical-checklist/) viable at scale and opens budget for iterating on [agent tooling](https://www.oguzhan.co/ai/) without burning through runway.

## Bibliography

Primary sources:

- [Introducing GPT-6 Sol and Luna](https://openai.com/index/introducing-gpt-6-sol-and-luna/), OpenAI, September 22, 2026.
- [GPT-6 Astra](https://openai.com/index/gpt-6-astra/), OpenAI (updated September 22, 2026 with family context).
- [GPT-6 Sol model documentation](https://developers.openai.com/api/docs/models/gpt-6-sol), OpenAI API Docs.
- [GPT-6 Luna model documentation](https://developers.openai.com/api/docs/models/gpt-6-luna), OpenAI API Docs.
- [OpenAI Models Overview](https://developers.openai.com/api/docs/models), OpenAI API Docs.
- [Artificial Analysis](https://artificialanalysis.ai/), September 22, 2026 evaluation drop (Opus 5.5 and GPT-6 Sol).
