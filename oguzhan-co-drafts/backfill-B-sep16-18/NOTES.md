# Backfill B rewrite notes

## Scope

Eight published oguzhan.co posts from 16 through 18 September 2026 were rebuilt as four English and Turkish pairs.

| Date | English | Turkish | Format |
| --- | --- | --- | --- |
| 16 Sep | `4701-en.md` | `4700-tr.md` | Daily digest |
| 16 Sep | `4708-en.md` | `4707-tr.md` | Deep dive |
| 17 Sep | `4720-en.md` | `4721-tr.md` | Daily digest |
| 18 Sep | `4728-en.md` | `4729-tr.md` | Daily digest |

## Source provenance

The requested `uploads/BRIEF.md` and `uploads/AGENT_VOICE.md` files were not mounted in this run, were not present on `main`, and were not present on the latest remote `main`.

The rewrite therefore used two verifiable substitutes:

1. The exact eight published WordPress records, fetched by post ID from the public oguzhan.co REST API.
2. The full `oguzhan.co agent voice pack` preserved on the existing remote draft branch `origin/cursor/weekly-en-tr-drafts-55c0`.

No unavailable brief text is represented as reviewed.

## Editorial rules applied

- English drafts use uneven sentence rhythm, concrete names and numbers, and no template essay scaffolding.
- Turkish drafts are separate compositions, not line translations of the English versions.
- Turkish institutional language uses `standartlar kuruluşu`, `standartlar kurumu`, or `özdenetim kuruluşu`; the calque `standart organı` was removed.
- Each article includes WordPress-ready SEO front matter and direct source links.
- Claims from company-run measurements are identified as such and separated from independent verification.
- Decorative em/en dashes and the voice pack's banned brochure language were removed.

