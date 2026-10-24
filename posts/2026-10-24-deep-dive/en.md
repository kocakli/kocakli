---
title: "Claude Duet: Anthropic's proactive agent and the limits it admits"
slug: "claude-duet-proactive-agent-approvals-limits"
focus_keyphrase: "Claude Duet"
yoast_title: "Claude Duet: How Anthropic's Proactive Agent Works"
meta_description: "Claude Duet is Anthropic's proactive agent in research preview. It checks every few hours, shares plan limits, and asks before it sends, pays, or deletes."
excerpt: "Anthropic opened Claude Duet on October 21, 2026 as a research preview for Pro and Max subscribers in the US. It works on a cloud computer while you are away, then waits for approval before it sends, pays, signs, or deletes."
---

## What is Claude Duet?

Claude Duet is a research preview Anthropic opened on October 21, 2026. It is a standalone app on iOS, Android, and the web at claude.ai, where Claude works as a proactive agent. It brings you what needs attention, keeps working on its own cloud computer while you are away, and asks before it sends a message, makes a payment, signs a document, or deletes anything. [Anthropic's announcement](https://claude.com/resources/articles/claude-duet) says the preview is waitlist only, starting with Pro and Max subscribers in the US, and that it is designed around [Claude Opus 5.5](https://www.oguzhan.co/what-is-a-frontier-model/). The [help center article](https://support.claude.com/en/articles/17631495-get-started-with-claude-duet) adds that, during the preview, it is included with Pro and Max at no extra cost and spends plan limits at the same rate as chats.

I read that announcement, the help center article, the [safety, privacy, and security post](https://claude.com/resources/articles/claude-duet-safety-privacy-and-security), the [product page](https://claude.com/product/claude-duet), and [Ashley Capoot's CNBC report](https://www.cnbc.com/2026/10/21/anthropic-preview-of-claude-duet-personal-ai-agent-take-on-muse-dots.html) from the same day. I have not used Claude Duet. The waitlist stops at the US, so nothing below is a test, and I interviewed nobody.

## It comes to you first
<!-- INLINE_IMAGE_1 -->

The product page states the split in Anthropic's words: "The Claude app waits for you to open a chat, and you work on something alongside Claude. Claude Duet comes to you."

Mornings open with a short brief on the most important items across connected apps. The help center says that brief looks across email and calendar, and that it can start first steps such as drafting replies. Quiet threads get a follow-up. The announcement says it messages you only when something needs your attention.

One thread, typed or spoken. Channels share memory, and Duet chats plus Claude chats outside projects are searchable. Each task has a page. Only you can mark it completed, and you can steer mid-task. The Make tab holds finished files: a research brief, a financial model, a slide deck, a dashboard. The announcement also names scheduling, dashboards built with dozens of tools, forecasts, prototypes, and web apps. The help center cites a small business plugin.

Memory, skills, and connectors carry over from your Claude account. A cloud virtual machine with its own browser keeps working after you close the app, so the laptop or phone can be off. A notification arrives when a task is done or needs review. Sites with no connector open in that browser.

The Claude Marketplace holds over 6,000 connectors and plugins, the [announcement](https://claude.com/resources/articles/claude-duet) says. The [product page](https://claude.com/product/claude-duet) says more than 6,000. Anthropic's examples include missed Gmail and Slack messages, unpaid QuickBooks or Stripe invoices with a draft reminder, Gusto payroll, and a LinkedIn job post only after you edit and approve it.

Disconnect any app and new access stops. What it already learned stays until you reset its memory. Deleting the account wipes everything Claude Duet stored.

## Why does Claude Duet only check every few hours?
<!-- INLINE_IMAGE_2 -->

[Anthropic's announcement](https://claude.com/resources/articles/claude-duet) says Claude Duet checks connected accounts every few hours, because checking nonstop would use up your plan's limits much faster. I am not turning "every few hours" into a clock time.

The help center says checks run at set intervals, "so something urgent can arrive between checks." The product page adds the judgment problem: "It may misread a thread or miscalibrate what's urgent, and it can miss something that arrives between checking in with you."

It spends the five-hour session limit and the weekly limit at the same rate as chats. Background work counts, so the morning brief and the check-ins can hit those limits sooner. A financial model or a deck needs more model turns on top.

The [help center](https://support.claude.com/en/articles/17631495-get-started-with-claude-duet) says admission brings one full reset of both limits, available until November 30, 2026. You can say what you want to hear about, and how often. Anthropic says it is still testing when to message you.

My reading of the announcement beside the help center: the polling interval is a cost decision dressed as a product decision. Proactivity is metered by the same plan limits as chat. For an inbox that needs minute-level reaction, a client emergency, Claude Duet is not the alarm. Something urgent can arrive between checks. The sources used here do not say what the app does once a limit is fully spent.

## Claude Duet on its own, with approval, and off-limits

| What Claude Duet does on its own | Asks first, every time it matters | Off-limits even with approval |
|---|---|---|
| Reads, drafts, prepares. Morning brief | Send a message, pay, sign, or delete | Trading securities |
| Checks connected accounts every few hours | A one-time card purchase you approve in Link | Moving money between accounts, or accessing someone else's account |
| Briefs, models, decks, dashboards as files | Paying or sending money, deleting an order, creating an account: never under "don't ask me again" | Credentials, full card and bank numbers, government ID numbers, even if you ask |

Before a send, a payment, a signature, or a deletion, the announcement says it shows exactly what it is about to do and waits. The safety post says the card carries the action, the destination, and the content, including every recipient. If you cannot approve right away, the help center says the rest of the task still finishes and the approval returns later. A number or summary is tied to the email, file, or spreadsheet it came from.

A second check, built on Claude Code's auto mode classifier, runs outside the model doing the work. The safety post says that is so instructions hidden in a page cannot affect the outcome. "No defense is perfect, which is one reason consequential actions need your approval," the help center says. Routines that run while you are away keep the same safeguards. Paying or sending money, deleting an order, and creating an account stay outside "don't ask me again."

"Approval fatigue is a serious issue, because too many requests teach people to tap through them." The safety post says calibration continues.

Sign-in credentials, full card and bank account numbers, and government ID numbers are never shared, even if you ask. Health and personal finances need consent, and your own request counts. The announcement says those topics come up only when you explicitly instruct it. Blocked text can be rewritten without the sensitive part and returned for approval. Safeguards "will occasionally miss something or flag a harmless message."

A one-time card can come from Link, Stripe's digital wallet, or from Shop Pay. The [safety post](https://claude.com/resources/articles/claude-duet-safety-privacy-and-security) says a Link card is limited to that merchant and amount, and that you approve it in the Link app. The real card number is not shared. The help center says each card works for that purchase only.

Credentials follow the [Claude Managed Agents](https://www.oguzhan.co/claude-managed-agents-dynamic-workflows/) design: a placeholder in the agent's machine, a proxy outside that puts in the real value as the request is made. Passwords, browser cookies, and sign-in tokens stay unseen. That matches the safety post: a classifier on drafted messages, you in control, credentials out of reach.

The password form appears only inside the app, during a sign-in you asked for. Never as a link, a text, an email, or any site other than claude.ai. A single-use key on the secure cloud browser machine encrypts what you type into a separate form on your device, and that value is sent straight to the browser.

Anthropic earlier cut live web access in internal evaluations after Claude submitted real forms on live sites, which I covered in [Claude internet access](https://www.oguzhan.co/claude-internet-access-anthropic-evaluations/). I read that as context for this fenced browser.

I did not watch the tests. The safety post lists three variants of routine-shaped tasks (innocent, injected instructions, tempting to overreach), shadow traffic, red teams, an external penetration test with source code access, a follow-on engagement on the cloud browser and sign-in form that it says is running now, and a HackerOne bug bounty. The announcement puts the external test under the public bug bounty.

## The browser you can't watch
<!-- INLINE_IMAGE_3 -->

The browser runs in its own cloud virtual machine, separate from the model and from the agent's other cloud computers. Commands are a fixed set: open this page, click here, type this. Site code and cookies stay on the browser machine. Page text and downloads come back, which is why the other checks exist. Uploads through the browser get the same sensitive-info check.

It sends a distinct User-Agent header, and Anthropic publishes the IP addresses it browses from. Before launch, several large websites were offered a block option, and some took it.

You cannot watch that browser or take it over. The announcement's line: it can't yet show you its browser.

What this preview leaves out:

- US only, Pro and Max, opening in waves. The waitlist email must match your Claude account and the Apple or Google account on your phone.
- No Team or Enterprise yet. Both the help center and the product page say that comes later.
- No model choice. Claude Opus 5.5 only, and it decides the effort.
- Microsoft 365 is not available yet.
- Slack works with limits.
- No phone calls or texts to other people. Email from a connected account still needs approval.
- It cannot see files on your computer or all of your projects. It can read your Claude work and cannot change it.
- Personal errands such as booking tickets "aren't quite as strong."
- A separate app from the main Claude app.
- 1Password sign-in is "coming soon."

Broad agent access has already pushed permission redesigns, the subject of the [Apple Full Disk Access](https://www.oguzhan.co/apple-full-disk-access-ai-agents/) note. Duet's published answer is the card, the outside check, and the off-limits list.

## Muse, dots and now Duet

[Ashley Capoot at CNBC](https://www.cnbc.com/2026/10/21/anthropic-preview-of-claude-duet-personal-ai-agent-take-on-muse-dots.html), writing on October 21, 2026, says Claude Duet will likely challenge OpenAI's dots and Meta's Muse. Capoot is the one drawing that matchup.

Meta's Muse, a personal AI agent, launched last month and went to the top of Apple's App Store. Meta mainly markets it to consumers. On the third-quarter call, Mark Zuckerberg told analysts that more than 10 million people in the US and Canada set up Muse personal agents over the past month and a half. The number is his, via [CNBC](https://www.cnbc.com/2026/10/21/anthropic-preview-of-claude-duet-personal-ai-agent-take-on-muse-dots.html).

OpenAI introduced dots, its "always-on agents," at its developer conference, which CNBC places weeks after Muse. The [DevDay notes](https://www.oguzhan.co/openai-devday-2026-dots-sol-pro-500-takeaways/) cover that launch. CNBC says OpenAI's product straddles enterprise and consumer use. The consumer read of Muse is in the [Muse and Wonder](https://www.oguzhan.co/muse-wonder-gemini-4-argon-frontier-agents/) piece.

Anthropic aims Claude Duet at work: professionals and small business owners. My reading: Anthropic chose the workplace lane and wrote its caution into the docs. No ranking from me on who is ahead.

## Before you join the waitlist

Anthropic built it, in the announcement's words, "for professionals and small business owners with more on their plates than they can track."

Jess Provencher, broker and owner of Pro Homes, is quoted in the [announcement](https://claude.com/resources/articles/claude-duet). I did not speak to her. A property showing sat on her calendar for the wrong day. Claude Duet flagged it without being asked. "[This is] exactly the kind of thing I want caught without having to ask."

Amin Ebrahimi owns Shahs of Kabob in South Florida, about 110 employees. Accounting, customer support, marketing, invoices store by store. "It brings it all together. I don't need to open up 100 tabs."

If the waitlist actually opens, the docs suggest a plain check before you connect anything:

- Which accounts you would connect, and which stay off.
- Which approvals you want to read in full, every recipient included.
- What stays out of its hands: trading securities, moving money between accounts, someone else's account.
- How hard the morning brief and the check-ins press the weekly limit.
- When to use the one reset, available until November 30, 2026.

Outside the US, Turkey included, the preview is closed. Reading material, for now. The product page says Claude Duet comes to you. Worth reading beside that: how often it looks, and what it still has to ask.

## Sources

- [Introducing Claude Duet](https://claude.com/resources/articles/claude-duet), Anthropic, October 21, 2026
- [Get started with Claude Duet](https://support.claude.com/en/articles/17631495-get-started-with-claude-duet), Anthropic Help Center
- [Claude Duet Safety, Privacy, and Security](https://claude.com/resources/articles/claude-duet-safety-privacy-and-security), Anthropic
- [Claude Duet product page](https://claude.com/product/claude-duet), Anthropic
- [CNBC report](https://www.cnbc.com/2026/10/21/anthropic-preview-of-claude-duet-personal-ai-agent-take-on-muse-dots.html), Ashley Capoot, October 21, 2026
