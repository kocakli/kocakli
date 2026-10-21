# Notes for the 2026-10-21 deep dive

Both uploads were read in full before drafting: the voice pack and the fact brief. The brief is the only fact source. No other repo files were edited.

## Body word counts

Whitespace-separated tokens in the markdown body, YAML front matter excluded.

- EN: 2048
- TR: 1720

The same count after replacing markdown links with their visible text and dropping the image comments is EN 2039 and TR 1711. Both sit inside the requested ranges (EN 1700-2100, TR 1450-1750).

## Internal links

EN (`en.md`):

- https://www.oguzhan.co/what-is-a-frontier-model/
- https://www.oguzhan.co/claude-haiku-5-5-gpt-6-luna-price-floor/
- https://www.oguzhan.co/openai-misalignment-reports-claude-ecdsa-seeds/
- https://www.oguzhan.co/china-ai-export-controls-model-weights/

TR (`tr.md`), the `/tr/` URLs only:

- https://www.oguzhan.co/tr/frontier-model-ne-demek/
- https://www.oguzhan.co/tr/claude-haiku-5-5-gpt-6-luna-fiyat-tabani/
- https://www.oguzhan.co/tr/openai-misalignment-raporlari-claude-ecdsa-tohumlari/
- https://www.oguzhan.co/tr/cin-yapay-zeka-ihracat-kontrolu-model-agirliklari/

No Jev hub link. Jev and TypeSafe are not mentioned.

## Left out or not upgraded past the brief

Every required brief fact is in both drafts. The items below were deliberately not turned into extra claims.

- Plotly's effort level is not in the brief. Neither draft assumes the 43-question run used `max`.
- MiniMax's "predecessor" in the 70 percent usage-cost claim is not identified as MiniMax-M3. The word stays MiniMax's. M3 prices are compared from the pricing page on their own.
- The "nearly three times faster" line has no named baseline in the brief, so none was added.
- Whether `reasoning_content` tokens are billed as output is not in the brief, so billing of the thinking trace is not asserted.
- M2.5 and M2.7 thinking behavior is not in the brief. Drafts do not claim those clients already send `thinking: disabled`. They do say Flash returns HTTP 400 when thinking is disabled, and that plan traffic to the old names is now routed to a model that always thinks.
- Parameter count is unpublished. The China export-control paragraph does not place MiniMax M3.1 Flash over or under any threshold. It only restates the brief's hedged route for a future weights release if the October 16 draft becomes final.
- Weights are not described as downloadable. The drafts follow the announcement ("released later"), the model guide's "open-weight" sentence, and OpenCode's "No". No extra mirror was searched.
- OpenRouter's "free stealth period has ended" and Plotly's October 20 "for now" are both reported. They are not collapsed into one OpenRouter price on October 21.
- DeepSeek peak hours stay in UTC, as published. They were not converted to Europe/Istanbul.
- Plotly's $4.09 was not split into input, output, and cache dollars. The September $0.82 run was not given a derived per-question price. "About 10 cents a question" is Plotly's figure for the October run priced at list price.
- "Three times the calls" is 45 against 15. "Close to four times" the tokens written is 32,000 against 8,500. Tokens read, 4.2 million against 0.7 million, is six times. Those readings sit next to Plotly's pairs. No other multiple was added.
- "Four weeks" is not used as an exact duration. The drafts give September 23 and October 19.
- No hands-on run, no benchmark of my own, no interview, no company reaction, no parameter count, no license name.
