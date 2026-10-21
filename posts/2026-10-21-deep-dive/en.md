---
title: "MiniMax M3.1 Flash: Space Bunny's tokens got cheaper"
slug: "minimax-m3-1-flash-space-bunny-price"
focus_keyphrase: "MiniMax M3.1 Flash"
yoast_title: "MiniMax M3.1 Flash: Price, Specs and the Space Bunny Link"
meta_description: "MiniMax M3.1 Flash lists $0.15 input and $0.60 output per million tokens. Space Bunny was the early version. Thinking stays on, so the task bill can rise."
excerpt: "On October 19, 2026 MiniMax released MiniMax M3.1 Flash and said Space Bunny was an early version. The list rate is $0.15 input and $0.60 output per million tokens, and thinking stays on."
---

## Space Bunny has a name

On October 19, 2026, [MiniMax](https://www.minimax.io/blog/minimax-m31f) released MiniMax M3.1 Flash and said Space Bunny, the anonymous model listed on [OpenRouter](https://openrouter.ai/stealth/space-bunny-alpha) since September 23 as Space Bunny Alpha, was an early version of it. [MiniMax's pricing page](https://platform.minimax.io/docs/guides/pricing-paygo) lists $0.15 per million input tokens, $0.60 per million output tokens, and $0.015 for cached input. The [model guide](https://platform.minimax.io/docs/guides/text-generation) gives MiniMax-M3.1-Flash a 1,000,000 token context window, with text, image, and video in. Calls go through the MiniMax API, the M Plan, and the MiniMax Code desktop app, and the announcement says the weights will be released later.

## No name from September 23 to October 19

I read MiniMax's announcement, the API docs, the pricing page, OpenRouter's stealth page, and Plotly's write-up. I did not run the model, and I interviewed nobody. Every score below is either MiniMax's claim or Plotly's single test.

[OpenRouter's stealth page](https://openrouter.ai/stealth/space-bunny-alpha) describes Space Bunny Alpha as an anonymous model with fast inference, strong coding, native multimodal input, adjustable reasoning effort, a 1 million token context window, text, image, and video in, and text out. The listing date is September 23, 2026. The page now says the model was revealed as MiniMax M3.1 Flash. The free stealth period has ended. Prompts and completions may have been retained by the provider, and they are not used for training.

My reading stops at that sentence. Retention is possible, training use is excluded, and a training exclusion is narrower than deletion.

[MiniMax](https://www.minimax.io/blog/minimax-m31f) says the anonymous run processed more than 200 trillion tokens. [TokenPost](https://www.tokenpost.com/news/technology/34757), writing on October 19, reports that the preview appeared on OpenRouter on September 23 and that by September 24 it held the top spot in OpenCode's daily token-usage ranking. [OpenCode's data page](https://opencode.ai/data/minimax/minimax-m3-1-flash) lists the named model second by tokens across OpenCode last week, and at 16 percent of tokens over the past two months.

A quiet traffic window before a public name is a lab habit. That sentence is opinion. The fact MiniMax published is the token count.

## MiniMax M3.1 Flash on MiniMax's own sheet
<!-- INLINE_IMAGE_1 -->

According to [MiniMax's announcement](https://www.minimax.io/blog/minimax-m31f), the release is "a generational leap in agentic tasks, coding, Computer Use and cybersecurity," online inference is "nearly three times faster," and overall usage cost on agentic tasks is 70 percent lower than its predecessor. The speed line names no baseline. I am leaving "predecessor" as MiniMax's word and pricing MiniMax-M3 from its own card.

Benchmarks from the same post, all MiniMax's claims:

- DeepSWE v1.1 at 73.7 percent
- OSWorld V2 at 61.7
- Agents' Last Exam at 29.6, and MiniMax says first among Chinese models on both OSWorld V2 and ALE
- BankerToolBench at 76.2
- CyberGym at 82 percent, for vulnerability discovery and validation
- AutomationBench-AA, "among the top performers" on enterprise SaaS workflows in sales, marketing, operations, customer service, finance, and HR

MiniMax adds that its internal security experts find the model strong in code auditing, vulnerability patching, penetration testing, malware analysis, and reverse engineering. That line is their characterization.

Speed, same announcement: "more aggressive sparsity," output that can pass 200 tokens per second, and a median (P50) above 170 tokens per second.

These percentages are vendor scores. Plotly's 43 questions, further down, are a separate test.

The [model guide](https://platform.minimax.io/docs/guides/text-generation) calls MiniMax-M3.1-Flash a "frontier multimodal coding model" with tunable thinking depth, built for agentic reasoning, tool use, coding, and structured task execution. A separate note covers [what the frontier label is doing](https://www.oguzhan.co/what-is-a-frontier-model/). The same guide also calls the model "an ultra-efficient open-weight model for everyday work," which clashes with the "later" on weights.

MiniMax-M3 remains on the guide, also with a 1 million token context window.

[MiniMax's OpenAI SDK page](https://platform.minimax.io/docs/api-reference/text-openai-api) lists the file rules. Images: JPEG, PNG, GIF, or WEBP, up to 10 MB. Videos: MP4, AVI, MOV, or MKV. Default sampling is 1 frame per second, allowed from 0.2 to 5. URL or base64 video tops out at 50 MB. Files API video tops out at 512 MB. Audio input is not supported.

## What does it cost?

US dollars per 1 million tokens. Flash and M3 come from [MiniMax's pay-as-you-go page](https://platform.minimax.io/docs/guides/pricing-paygo). DeepSeek comes from [DeepSeek's pricing page](https://api-docs.deepseek.com/quick_start/pricing), where deepseek-flash is DeepSeek-V4.1-Flash-1017, with a 1 million token context window.

| Model | Input | Output | Cached input |
|---|---|---|---|
| MiniMax M3.1 Flash | $0.15 | $0.60 | $0.015 |
| MiniMax M3 (standard, ≤512k input) | $0.30 | $1.20 | $0.06 |
| DeepSeek V4.1 Flash (off-peak / peak) | $0.15 / $0.30 | $0.60 / $1.20 | $0.003 / $0.006 |

On input and output, MiniMax M3.1 Flash is half of MiniMax-M3's standard rate at or under 512k of input. Cached input on Flash is $0.015, a tenth of Flash's $0.15 input price and a quarter of M3's $0.06 cache price at that tier.

Above 512k of input, M3 is priced at $0.60, $2.40, and $0.12. The page also lists a priority tier at 1.5x for M3. Flash's published line stays flat at $0.15 / $0.60 / $0.015.

MiniMax's 70 percent figure measures usage cost on agentic tasks against its predecessor. The sticker moves the invoice only once token volume, call count, and cache share are known.

Off-peak, DeepSeek matches Flash on input and output at $0.15 and $0.60. Peak hours on DeepSeek's page are 01:00 to 04:00 UTC and 06:00 to 10:00 UTC, Monday to Friday, and in those hours input and output double to $0.30 and $1.20. Cache hits stay lower than Flash in both windows, $0.003 off-peak and $0.006 peak, against $0.015. The October 19 digest covered DeepSeek-V4.1-Flash-1017 [among three open-weight releases](https://www.oguzhan.co/openai-misalignment-reports-claude-ecdsa-seeds/). This row compares rates. Flash weights are still unreleased. The $0.15 / $0.60 pair also sits on the cheap-tier floor from the [Haiku 5.5 and GPT-6 Luna note](https://www.oguzhan.co/claude-haiku-5-5-gpt-6-luna-price-floor/), with one extra rule on Flash: thinking stays on.

## Cheap tokens, long thinking
<!-- INLINE_IMAGE_2 -->

[MiniMax's chat completion reference](https://platform.minimax.io/docs/api-reference/text-chat-openai) says M3.1 Flash always thinks. Setting thinking to disabled returns HTTP 400. The trace comes back on its own, in `reasoning_content`. Effort is called `reasoning_effort` there and `effort` in the model guide. The accepted values are low, medium, high, xhigh, and max. The default is max.

MiniMax-M3, on that same page, uses adaptive thinking, and disabled skips thinking. Flash sells the cheaper token and refuses a silent call. M3 still accepts silence, at the higher rate. A request body copied from M3 with thinking disabled will get HTTP 400 from Flash.

[Plotly's October 20 write-up](https://plotly.com/blog/minimax-m3-1-flash-plotly-data-analytics-bench/) is the one independent test I read. Forty-three data-analytics questions. Space Bunny in September against MiniMax M3.1 Flash in October. I did not run them. The write-up leaves the effort level unstated, so I am leaving it unstated too.

September, then October:

- Score: 38 of 43, then 41 of 43
- Hidden patterns: 2 of 5, then 5 of 5
- Model calls per question: 15, then 45
- Tokens read per question: 0.7 million, then 4.2 million
- Tokens written per question: 8,500, then 32,000
- Median time per question: 36 seconds, then 3 minutes
- Full run at MiniMax list prices: $0.82, then $4.09

Plotly also says 98 percent of input was cached, and gives that share once. Calls went from 15 to 45, three times. Tokens written went from 8,500 to 32,000, close to four times, and tokens read from 0.7 million to 4.2 million. OpenRouter was serving M3.1 Flash for free for now, so Plotly priced the October run at list price and put it at about 10 cents a question.

On score, 41 of 43 ties Claude Opus 5.5, Gemini 4 Argon, Muse Wonder, and GPT-6 Sol. Plotly calls that the best score they have seen from a Chinese lab. Next on their list: GLM 5.3 Flash and Qwen 3.8 27B, both at 38. September's Space Bunny, at 38 of 43, was "as well as any open-weight model we'd tested." October added three correct answers and all five hidden patterns.

Plotly puts this 41 of 43 at about a third of the cost of Claude Opus 5.5 and Gemini 4 Argon for the same score. GPT-6 Sol scored 41 for $2.61, and GPT-6.1 Sol scored 43 of 43 for that same $2.61. I am keeping both comparisons inside this one suite.

The clock is the other bill. Three minutes median is the slowest mark on Plotly's leaderboard. They observed about 150 tokens per second per call. MiniMax cites a P50 above 170 and peaks above 200. Plotly's check against that median: even at 170 tokens per second, writing 32,000 tokens takes about three minutes. Their judgment: fine for analysis that runs in the background, and slow for someone waiting on an answer.

Effort is the dial I would budget. Default is max, disabled is rejected, and I have no measurement of low against max. Plotly's October model still called more and wrote more than the September preview on the same questions. Background work can live with a three-minute median. A person waiting on a chat answer will notice the wait first.

OpenRouter's stealth page says the free stealth period has ended. Plotly's "for now," dated October 20, is why they priced a free endpoint at list price. I would budget the list price after that post.

## What changes if you were on M2.5 or M2.7?

[MiniMax's model list](https://platform.minimax.io/docs/faq/models) gives the M2.5 and M2.7 families two dates. From October 19, 2026, new users cannot start on them. On November 18, 2026, they are retired and API requests stop working.

Pay-as-you-go customers who already had access keep it until November 18. M Plan and Token Plan users are redirected. From October 19, requests to M2.5 or M2.7 route automatically to MiniMax M3.1 Flash. Old model names keep working. Plan allowances stay unchanged.

A plan user can change models without changing a line of code. Outputs, latency, and tokens per task can still shift, because the model behind the old name now always thinks, and thinking disabled returns HTTP 400. The allowance figure stays. How many tasks it covers depends on tokens per task. I would re-run evals on the work I actually ship, and I would treat old M2.7 logs as a different model.

MiniMax-M3 remains available, including the switch that skips thinking, at M3's higher rates.

## Open weights, eventually
<!-- INLINE_IMAGE_3 -->

MiniMax's announcement says "Model weights will be released later." Pro, which "pushes the boundaries of intelligence," will also arrive later. No date, no parameter count, and no license in the pages I read.

The docs already use a stronger phrase. The model guide calls MiniMax M3.1 Flash "an ultra-efficient open-weight model," the announcement says later, and [OpenCode](https://opencode.ai/data/minimax/minimax-m3-1-flash) lists open weights as No. As of October 21, 2026, I have no downloadable weights, and no license to plan a self-hosted copy around.

China's October 16 draft is a separate track, covered in the note on [export controls and model weights](https://www.oguzhan.co/china-ai-export-controls-model-weights/). Already-published open weights are out of scope. New open-source releases get automatic licensing. If the draft becomes final, a future MiniMax M3.1 Flash weights release would take that route. Parameter count is unpublished, so the note stops at the route.

## Before you switch

- Run the same tasks at two or three effort levels and log calls, tokens, and time. The default is max. Choose it on purpose.
- Watch the cached share of input. At $0.015 against $0.15, that share moves the input side of the bill and leaves output tokens and extra calls untouched.
- Check the pipe. MiniMax Code, the MiniMax API, and an OpenRouter route can share a brand and still differ.
- Mark November 18 if anything in production still says M2.5 or M2.7. Plan traffic is already redirected. Pay-as-you-go calls on those names stop that day.
- Wait for weights and a license before a self-hosting plan.

The rate card is the easy page. The thinking is what the invoice counts.

## Sources

- [MiniMax announcement, October 19, 2026](https://www.minimax.io/blog/minimax-m31f)
- [MiniMax model invocation guide](https://platform.minimax.io/docs/guides/text-generation)
- [MiniMax create chat completion](https://platform.minimax.io/docs/api-reference/text-chat-openai)
- [MiniMax OpenAI SDK page](https://platform.minimax.io/docs/api-reference/text-openai-api)
- [MiniMax model list and retirement notice](https://platform.minimax.io/docs/faq/models)
- [MiniMax pay-as-you-go pricing](https://platform.minimax.io/docs/guides/pricing-paygo)
- [OpenRouter stealth page for Space Bunny Alpha](https://openrouter.ai/stealth/space-bunny-alpha)
- [TokenPost, October 19, 2026](https://www.tokenpost.com/news/technology/34757)
- [OpenCode data page for MiniMax M3.1 Flash](https://opencode.ai/data/minimax/minimax-m3-1-flash)
- [Plotly data analytics write-up, October 20, 2026](https://plotly.com/blog/minimax-m3-1-flash-plotly-data-analytics-bench/)
- [DeepSeek API pricing](https://api-docs.deepseek.com/quick_start/pricing)
