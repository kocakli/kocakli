---
title: "Jev Real-Time: Doom, Wikiracing, and Browser Loops Without Pixels"
slug: "jev-realtime-doom-wikiracing-browser"
yoast_title: "Jev Real-Time Demos: Doom, Wikiracing & Browser Loops | TypeSafe Structured State"
yoast_metadesc: "TypeSafe's Doom bot and Wikiracing demos show Jev running at game speed on structured text state. Browser and mobile stacks follow the same pattern: indexed DOM, not pixels."
focus_keyphrase: "Jev real-time"
---

## Jev Goes Real-Time: Structured State, Not Pixels

TypeSafe's [Jev launch demos](https://typesafe.ai/blog/introducing-system-one-models-and-jev) put a decision model in 10 Hz loops: Doom at ~10 queries per second, Wikiracing through hundreds of Wikipedia links per hop, browser agents picking DOM targets in under eight seconds. The hook is structured text input, not framebuffer vision. Doom passes game state as lines (health, ammo, positions, available moves). Wikiracing passes on-page link anchors. Browser stacks serialize the accessibility tree or indexed DOM. Every loop ends in a [Choice call](https://www.oguzhan.co/jev-primitives-choice-score-noul/) and a millisecond-fast response.

Spectacular? Yes. Best player? No. The [TypeSafe team admits](https://typesafe.ai/blog/introducing-system-one-models-and-jev) a non-AI Doom bot would outperform their agent; the goal is reactive instruction-following at loop cadence. Rate limits and the Choice-255 ceiling shape real designs. Community browser and mobile projects inherit the same tradeoffs.

## Doom: Text State at $7 Per Hour

TypeSafe's Doom agent queries Jev around 10 times per second. Game state arrives as structured text: player position, nearby enemies, health, ammo, four-directional movement, shoot, strafe. The model picks one action. The loop repeats. Published early-access pricing runs ~$0.042 per million input tokens; output is free. Sustained gameplay costs roughly $7 per hour.

<!-- INLINE_IMAGE_1 -->

The team frames it as instruction-following under time pressure, not optimal play. A handcoded pathfinding bot would clear rooms faster. But Jev responds in 70 to 500 milliseconds per query (covered in [Day 3's speed essay](https://www.oguzhan.co/jev-speed-cost-parallel-sampler/)), fast enough to feel reactive when a human watches. The architecture is simple: observe structured state, ask a typed question (Choice), act. No pixel decoding, no OCR lag.

Rate math matters. Early-access limits sit at ~250,000 tokens per second throughput and 1,200 requests per minute (20 per second). One 10 Hz agent uses half the rpm budget. Multiple agents or concurrent requests hit the ceiling quickly. That constraint pushes real designs toward host-side timeouts and fallback actions when Jev is late.

## Wikiracing and the Choice-255 Ceiling

Wikiracing is a cleaner stress test for high-cardinality decisions. Start article, target article, only on-page links allowed. Each hop can present hundreds or thousands of Wikipedia anchors. The game showcases Choice at scale without inventing URLs or free-form guessing.

The catch: [Choice supports up to 255 options](https://www.oguzhan.co/jev-primitives-choice-score-noul/). Above that, you need a two-stage pattern. Score or shortlist independently (filtering down to 48 or 60 strong candidates), then Choice on the subset. TypeSafe notes occasional slowdown when the shortlist step runs. Community implementations like [jev-agent.com/wikirace](https://jev-agent.com/wikirace) report ~48 links per hop after filtering, keeping Choice under the ceiling.

The lesson applies beyond Wikipedia. Browser DOM trees, app menus, autocomplete dropdowns all overflow 255 options. The two-stage pattern becomes standard: prune to the top tier, then decide.

<!-- INLINE_IMAGE_2 -->

## Browser and Mobile Stacks: DOM Tables, Not Screenshots

Community browser agents followed the same structured-state playbook. [jev-ultrafast](https://github.com/cobanov/awesome-jev) indexes the DOM into an action space: clickable elements, text fields, navigation targets. One Jev request picks operation and target (click button #12, scroll down, navigate to tab). TYPE_TEXT actions go to a small LLM, not Jev. The author reports Zürich to London flight searches in ~7.1 seconds, start to booking screen.

[jev-browser-use](https://awesomejev.vercel.app/c/browser-and-computer-use/) splits the loop differently. Jev handles navigate, click, and scroll. The Codex skill keeps typing and verification logic. The hybrid claims ~5 to 10× faster browser steps compared to pure generative approaches, though exact benchmarks vary by task.

Mobile follows the Android accessibility tree, not screenshots. [mobile-jev](https://github.com/cobanov/awesome-jev) and peers like xinwang-nwpu's jev-mobile serialize the A11Y hierarchy into a table: buttons, text fields, scroll containers. One request picks action and element. The author reports nine Uber actions in ~21 seconds (mobile-jev) and a Bilibili task in ~18 seconds (jev-mobile). Treat these as author-reported timing; reproduction depends on device, network, and rate limits.

Other tools apply the pattern to specific contexts. jkudish/jev-browser wraps Playwright with an MCP server. imanshu03's jev-browser-use adds a confidence gate on top of Chrome DevTools Protocol. typesafe-computer-use (also called jev-use) targets macOS accessibility APIs, still avoiding pixels. The common thread: serialize the interface state into a structured question, ask Jev for a typed decision, execute.

## Demos Are Not Best Players

Real-time Jev is state serialization plus typed questions in the hot path. The model answers fast. The host code owns timeouts, defaults when the response is late, and shortlisting when cardinality overflows 255.

This architecture produces striking demos. Doom gameplay looks fluid. Wikiracing solves puzzles in seconds. Browser agents book flights faster than a human can click. But none of these demos optimize for best-in-class performance. A Doom speedrunner or a search heuristic would win. The tradeoff is instruction-following at loop speed: you describe the goal, the agent reacts, and the loop stays tight.

Rate limits and cost frame real deployments. $7 per hour for Doom is sustainable for a demo, expensive for a 24/7 service. 1,200 rpm supports a handful of concurrent agents, not a thousand. Production designs layer host logic around Jev: shortlists, caching, fallback heuristics, partial tool calls to smaller models. The decision model stays fast; the scaffolding keeps it from burning budget or hitting limits.

The browser and mobile stacks prove the pattern scales beyond games. DOM and A11Y trees are just more structured state. Jev's speed and typed outputs fit any loop where the environment can serialize itself and 255 options cover most decisions. When they don't, two-stage Score-then-Choice fills the gap.

That's the Day 6 lesson. Real-time Jev works because the environment does the hard serialization, the model picks from a typed menu, and the host handles the edge cases. Pixels optional.
