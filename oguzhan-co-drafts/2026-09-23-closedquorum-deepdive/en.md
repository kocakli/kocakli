---
title: "CLOSEDQUORUM malware: when four LLMs vote on the next steal"
slug: "closedquorum-malware-llm-c2-quorum"
yoast_title: "CLOSEDQUORUM malware: four LLMs vote on attacks"
yoast_metadesc: "Inside CLOSEDQUORUM malware: four-model voting, commercial LLM APIs as tactical C2, Discord exfiltration, CAIRN hunting, and defender signals."
focus_keyphrase: "CLOSEDQUORUM malware"
excerpt: "CLOSEDQUORUM turns four commercial LLM APIs into a post-compromise decision panel. Its design shows how attackers can move a bounded phase of an intrusion away from a human operator, and why defenders need correlation rather than another domain blocklist."
---

CLOSEDQUORUM malware is the first publicly documented Windows implant to use commercial LLMs as tactical command-and-control infrastructure, according to [Cisco Talos](https://blog.talosintelligence.com/the-closed-quorum-inside-the-first-reported-autonomous-ai-c2-implant/). It asks up to four models what to do after compromise, takes a plurality vote, and can steal credentials, inject code, or establish persistence without waiting for an operator to answer. There is no confirmed campaign in the wild, and the public distribution build is inert. The important part is the architecture, not a victim count that does not exist.

I covered the initial finding [earlier today](https://www.oguzhan.co/closedquorum-ai-malware-four-model-vote/). The deeper story is stranger than “malware uses AI.” It is about where attacker effort goes, what replaces a conventional C2 listener, and which traces remain when the attacker borrows infrastructure from DeepSeek, Qwen, Mistral, Google, and Discord.

## 🧩 What CLOSEDQUORUM malware actually does

Talos found CLOSEDQUORUM through its Cognitive Artifact Intelligence Research Network, or CAIRN. The specimen is a 16.4MB, 64-bit Windows executable written in Go with CGO enabled. That last detail matters because the program uses CGO for direct Windows syscalls rather than staying inside the usual Go runtime boundaries.

At startup, `gatherSystemInfo()` collects the hostname, operating-system architecture, CPU count, Windows version, and whether the current context has administrator rights. Those details enter the model prompt as `TARGET:%s`. A target process value is refreshed on every decision cycle. The implant then waits five minutes before its first contact and uses randomized polling intervals of five to 15 minutes afterward.

The public sample cannot simply be switched on and aimed at a machine. It contains `dummy_api_key` and `dummy_webhook_url`, so its LLM and Discord paths are inert as distributed. Talos also found no evidence confirming deployment in a live campaign. Artifacts do, however, connect its developer to carding-forum posts reaching back to 2025. An internal name, BALZAK, survived in the history before the project was renamed CLOSEDQUORUM on July 3, 2026.

That distinction is worth keeping clean. This is a documented implant design with working capability code and dummy service credentials, not proof that an autonomous campaign is currently roaming corporate networks.

## 🌐 The C2 address is a service everyone else uses

Conventional C2 infrastructure gives defenders something concrete to chase: an attacker-controlled domain, IP address, listener, or redirector. The attacker pays for it, rotates it when exposed, and risks attribution every time an analyst follows the trail.

CLOSEDQUORUM changes that cost. Its `ModelOrchestrator` calls commercial model APIs used by thousands of legitimate applications every day. DeepSeek, Qwen from Alibaba, Mistral, and Google Gemini become the tactical decision channel. Blocking any one provider at the perimeter could break real business software long before it solves the malware problem.

This does not make the implant invisible. It changes the unit of detection. A connection to a model API is weak evidence. An unexpected Windows process contacting several model providers within a short period, touching LSASS, creating a suspended process, installing WMI persistence, and then posting to a Discord webhook is quite a different event.

The same principle applies to AI agent security outside malware. Tool access turns generated text into action. My [practical MCP and AI agent checklist](https://www.oguzhan.co/mcp-ai-agents-practical-checklist/) focuses on that seam: identity, permissions, tool scope, logs, and failure behavior. CLOSEDQUORUM is hostile software, but its model-to-tool boundary creates a familiar engineering problem.

## 🗳️ Four answers enter, one action leaves

The orchestrator queries providers in a fixed sequence: DeepSeek, Qwen, Mistral, then Gemini. Each response is parsed into an `LLMDecision`, and `interModelDiscussion()` counts the `Decision` field. The most common valid answer wins.

The system prompt is blunt: “You are an advanced malware strategist. Provide ONLY executable decisions.” Output is constrained to JSON, with four permitted decision values:

- `steal`
- `inject`
- `persist`
- `move`

Calling this a discussion flatters it. The models do not conduct a rich debate. Their answers are collected, reduced to a field, and plurality-counted. If two choices tie, submission order decides the winner because the max-finding code uses a strict less-than comparison. DeepSeek therefore has first priority, followed by Qwen, Mistral, and Gemini.

Multiple providers still buy the developer something useful. One model may refuse, another may time out, and a third may produce malformed JSON. The panel can keep going. If every provider fails, though, the fallback string is `consensus`. No capability handler exists for it, so the implant sleeps and tries again rather than launching some default attack.

That failure mode is revealing. “Autonomous” here does not mean unlimited initiative. The models choose among a small menu, and ordinary software decides whether the result maps to code. CLOSEDQUORUM has a bounded decision loop, not a model freely inventing Windows operations.

## 🧨 The menu is short; each item is heavy

The `steal` path is a bundle, not a gentle probe. It runs `lsassDump()`, `dumpBrowserCredentials()`, and `extractCryptoWallets()` together. The browser routine targets Chrome, Edge, and Firefox. Wallet collection looks for the MetaMask Chrome extension, Exodus, and an Ethereum path. In ATT&CK terms, the credential activity includes LSASS memory access (T1003.001) and browser credential stores (T1555.003).

For `inject`, CLOSEDQUORUM generates shellcode and chooses between two established techniques. The default is Early Bird APC injection (T1055.004). If `exploit_type` is `process_hollow`, it uses process hollowing (T1055.012).

Persistence has three routes: a Registry Run key with a `WindowsUpdate` value, a scheduled task, and a permanent WMI event subscription installed through PowerShell at `C:\Windows\Temp\wmi.ps1`. Other staging also sits under `C:\Windows\Temp\`, while Windows Update naming supplies the cover.

Then there is `move`. The prompt allows it. The distribution build has no handler for it. Any account of CLOSEDQUORUM performing lateral movement would be filling in code that Talos did not find.

The implant also patches `EtwEventWrite` with a return instruction, delays execution, and carries an encrypted secondary payload protected with a time-derived key. These are recognizable evasive mechanics, not model magic. The LLM layer sits above them and selects a route.

## 📦 A build-time service for buyers

Talos infers a credentials-as-a-service model from the sample and its surrounding artifacts. The developer would insert a buyer’s LLM API keys and Discord webhook during compilation. The buyer would handle delivery. Once the implant ran on a target, its model panel could select post-compromise actions even while the operator was offline.

That is effort displacement.

Most discussion of offensive AI gets sorted into speed and scale. Models can produce phishing material faster, or generate more variants. CLOSEDQUORUM demonstrates a third axis: transfer a bounded phase of the attack from a person to a loop that keeps polling while the person sleeps.

The winning model decision, its reasoning, and target telemetry are sent to the operator through Discord. Collected data follows the same route. CLOSEDQUORUM encrypts exfiltrated material with AES-256-GCM, Base64-encodes it, splits it into chunks of roughly 1,900 bytes, and spaces posts one second apart.

Encryption sounds reassuring until the key design appears. The symmetric key is derived from the date. That is not genuine confidentiality between developer and operator. It is packaging around the data stream, with a predictable input available to anyone who knows the scheme.

## 🔎 CAIRN hunts for the ideas left inside code

The companion story is how Talos found this specimen. [CAIRN](https://blog.talosintelligence.com/introducing-cairn-frontier-tracking-for-ai-integrated-malware/) is an open-source toolkit that starts with metadata. Its hunting layer does not require an analyst to download or execute every binary.

CAIRN looks for “cognitive artifacts”: prompt templates, provider endpoints, API key prefixes, jailbreak text, strings meant to evade AI analysis, and tool-call syntax. Acquisition filters include categories such as provider API integration, Python AI scripts, local LLM runtimes, agentic tooling, and AI-analysis evasion.

Those observations feed a three-tier YARA ontology. Tier 1 catches primitive AI artifacts. Tier 2 adds behavioral context. Tier 3 describes operational families. An Explorer graph and semantic clustering with UMAP and HDBSCAN help analysts find nearby samples.

Clusters are leads, not attribution. Talos explicitly warns that PyInstaller, Tauri, and some Go PE structures can inflate Tier 1 and Tier 2 matches. A bundled application can carry provider strings or packaging traits without being malicious. The method becomes useful when weak artifacts combine into a specific behavioral story.

CAIRN also traced natural-language suppression text intended to frustrate AI analysis from a red-team instructor into independent actor samples within 12 months. That kind of textual reuse is precisely what a metadata-first system can surface. It tells an analyst where to look next; it does not name an operator by itself.

## 🚨 Defenders need a sequence, not a blocklist

The practical detection opportunity is correlation. Start with an unusual executable reaching several model providers in a short window. Add host behavior: LSASS access, suspended-process injection, a Registry Run key, a scheduled task, or permanent WMI subscription. Then check whether the same process talks to a Discord webhook.

Network controls can contribute more context where policy and visibility allow it. Structured prompts containing host details and offensive instructions are distinctive under TLS inspection or at the provider. Endpoint telemetry supplies the actions that make those prompts dangerous.

No single signal is comfortable:

- DeepSeek, Qwen, Mistral, and Gemini endpoints have legitimate clients.
- Discord webhooks have legitimate automation uses.
- Go and CGO appear in ordinary Windows software.
- WMI and scheduled tasks are administration tools.

Together, in one process lineage and one time window, they tell a much sharper story. This is also why sandbox boundaries and tool permissions matter in legitimate agent systems, a topic connected to the [AI agent sandbox breakout digest](https://www.oguzhan.co/ai-digest-20-sep-2026-ai-agent-sandbox-breakout/). Generated intent is cheap. The consequential part is which operating-system actions the surrounding program permits.

Providers have a defensive role too. Repeated prompts carrying `TARGET:` host context, the extracted strategist instruction, or the tiny `steal`/`inject`/`persist`/`move` schema may be visible on their side even when an enterprise cannot inspect encrypted traffic. Provider-side detection will have to distinguish research and testing from abuse, but the service sees a part of the exchange that the endpoint defender may not.

## ⏱️ Autonomy arrives one bounded phase at a time

Talos places CLOSEDQUORUM at the far end of an escalation visible since the mid-2025 LAMEHUG and CERT-UA era: from an LLM as an optional feature to a multi-model consensus orchestrator controlling post-compromise behavior. That progression took roughly one calendar year in the samples CAIRN tracks.

The phrase “fully autonomous” needs a fence around it. CLOSEDQUORUM depends on four commercial APIs, buyer-supplied credentials, network access, accepted requests, valid JSON, and hard-coded handlers. Provider refusals, rate limits, malformed responses, or revoked keys can stall it. Its tie-break is predictable. One advertised decision has no implementation. Its exfiltration key is date-derived.

Yet dismissing it because the public build is inert would miss the design shift. The developer has moved tactical selection into a replaceable service layer and left execution to deterministic Windows code. No science-fiction intelligence is required. Current APIs and a very small decision schema are enough to remove the operator from part of the loop.

That is the useful warning from CLOSEDQUORUM malware. Defenders are not facing an omniscient model. They are facing conventional credential theft, injection, persistence, and exfiltration wired to a cheap decision panel that can operate without a human watching every poll. Hunt the wiring, the sequence, and the permitted actions. The model names will change.

## 📚 Sources

- Cisco Talos, [“The CLOSED QUORUM: Inside the first reported autonomous AI C2 implant”](https://blog.talosintelligence.com/the-closed-quorum-inside-the-first-reported-autonomous-ai-c2-implant/), September 22, 2026.
- Cisco Talos, [“Introducing CAIRN: Frontier tracking for AI-integrated malware”](https://blog.talosintelligence.com/introducing-cairn-frontier-tracking-for-ai-integrated-malware/), September 22, 2026.
