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

## Final checks

- Exactly eight article files are present, plus this notes file.
- Every article has the seven expected front-matter fields and a linked Sources or Kaynaklar section.
- Word counts including front matter: 4701 EN 1,119; 4700 TR 1,020; 4708 EN 1,960; 4707 TR 1,747; 4720 EN 1,180; 4721 TR 1,068; 4728 EN 1,196; 4729 TR 1,067.
- Total article word count including front matter: 10,357.
- English and Turkish prohibited-language scans pass; the single natural sentence `Demek ki mesele sektörün para vermesi değil` was manually reviewed and is not a repeated rhetorical scaffold.
- `git diff --check` passes.

