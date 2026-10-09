# NOTES: Clef vs Jev drafts (EN + TR)

Drafted 2026-10-09 by a Cursor Cloud Agent. Status: drafts only. Not published, not merged.

Files:
- `drafts/en-clef-vs-jev.md` (English, original)
- `drafts/tr-clef-vs-jev.md` (Turkish, written separately in the Dünya Halleri register, not a line translation)

Fact source: `RESEARCH.md` (compiled 2026-10-09) only. Nobody at oguzhan.co ran Clef or Jev; both drafts say so in the intro and use first person only for framing ("My read", "My take", "Bana sorarsanız").

## Brief conflicts and how I resolved them

| Topic | CLOUD_AGENT_BRIEF.md | User request | Used |
|---|---|---|---|
| File names | `en-cloudflare-vs-jev.md`, `tr-cloudflare-vs-jev.md` | `en-clef-vs-jev.md`, `tr-clef-vs-jev.md` | User request |
| EN length | 1500 to 2200 | 1400 to 2000 | Overlap, 1500 to 2000 |
| TR length | 1300 to 1900 | 1100 to 1600 | Overlap, 1300 to 1600 |
| Meta length | ≤155 | 130 to 155 | 130 to 155 |

## Counts and SEO checks

Word counts cover the body including the table and exclude front matter, image placeholders and Sources (`wc -w`).

| | EN | TR |
|---|---|---|
| Body words | 1935 | 1598 |
| Body words without table | ~1750 | ~1415 |
| Focus keyphrase | "Clef vs Jev" (first 3 words) | "Clef ve Jev" (first 100 words) |
| Yoast SEO title | 53 chars | 54 chars |
| Yoast meta description | 149 chars | 152 chars |
| Question H2s | "What does Clef cost compared with Jev?", "Is Clef really a drop-in replacement for Jev?" | "Clef ve Jev ne kadar tutuyor?", "Clef, Jev'in yerine doğrudan geçer mi?" |
| Hub link | https://www.oguzhan.co/ai/ | https://www.oguzhan.co/tr/yapay-zeka/ |
| Other internal links | ecosystem, speed/cost, confidence (EN) | ecosystem, speed/cost, confidence (TR) |
| Image placeholders | cover + 4 inline | cover + 4 inline |
| Alt text length | 106 to 112 chars | 106 to 119 chars |

Automated checks run on both files:
- EN: no em or en dash; none of delve, landscape, robust, leverage, underscore, pivotal, tapestry, testament, realm, "it's worth noting", "not only".
- TR: no em or en dash; no -maktadır/-mektedir; no masa/masada; no kapsamında, bağlamında, doğrultusunda, noktasında; no Günümüzde, Sonuç olarak, Kısacası; no "organ".

## Required flags: where they appear

- **The latency numbers can't be compared.** EN: the table's last row, then the paragraph right after Cloudflare's 2.5x/13x claim (Flavio Copes citing the leaderboard methodology: Cloudflare's numbers are on-network, Jev's are an internet round trip), plus the limits list and the latency bullet in "When to pick which". TR: the "Latency rakamları neden kıyaslanamaz" H3 directly after the claim, plus the same follow-ups. The 13x figure never appears without this caveat.
- **Small tests and conflicts of interest.** EN H3 "Small samples, and everyone has a stake"; TR H3 "Testler küçük, herkesin bir çıkarı var". Covered: Startrise is a consultancy selling related services; Construct runs on Cloudflare; Cloudflare benchmarked its own model; TypeSafe publishes no public benchmarks and says its own evals may be biased; this site covers Jev a lot (intro disclosure).
- **Vendor claims vs independent tests.** Each vendor figure names the vendor in the same sentence ("According to the changelog", "TypeSafe's docs list", "Workers AI pricing lists"). Each independent figure names the tester (Startrise, Construct, DEV Community, Flavio Copes). HN and X are labelled anecdotes.

## Claims I softened or reframed

- "Fully Jev-API compatible": always attributed to Cloudflare. In the table it reads "System One compatible (per Cloudflare)".
- "Nearly six times": attributed to The Register.
- "Clef-flash is a little over twice Jev's list price": my arithmetic from list prices ($0.09 / $0.042 ≈ 2.1x).
- Workflow evals: Cloudflare says "Clef beats Jev in 3 of 4 areas". I added that the margins are 3 points or less (from the card: 2.9, 0.3/1.0, 1.2) and that Jev takes the fourth. The arithmetic is mine; the numbers come from the Hugging Face card.
- Construct with per-model thresholds: given as a range (90.6% to 93.2%), because RESEARCH.md doesn't say which number goes with which model.
- Video input: described as a property of the open weights only, per RESEARCH.md section 5. Hosted Workers AI is described as images only (max 4).
- Jev's "can't hallucinate": narrowed to TypeSafe's own meaning, which is no type errors.
- "Open source": described as open weights with closed training data.
- Almeida's X quote: EN quotes it up to "reliability", which leaves out the clause "that, by definition, doesn't show up on benchmarks". TR paraphrases the whole sentence. A coordinator can restore the full quote in EN if preferred.
- Startrise's references: described as "AI-reviewed references" (RESEARCH.md: "post-hoc AI-reviewer references").

## Uncertain items (RESEARCH.md section 5)

- OpenRouter's note that Workers AI reads only ~2K tokens of long text state: EN mentions it, explicitly labelled unverified, next to Cloudflare's own wording. TR drops it to stay within length.
- Jev "questions per request": left out, and the row is removed from both tables.
- Unofficial wiki rate limits: not used. The official 100K tok/s and 80 rps are used.
- "A quarter of Fortune 500" (GIGAZINE): not used.
- Red Hat Developers guardrail comparison (secondhand via Startrise, Clef not included): not used.

## Facts in RESEARCH.md I did not place (length)

Both languages:
- Threat-intel example: Clef with Browser Run took 2.2 s vs 4.7 s for gpt-oss-120b.
- p95 latencies (238.6 / 122.4 / 536.0 ms).
- Benchmark rows BFCL, CLINC150+OOS, When2Call, BRIGHT, BBH, HoVer, PhishNChips, and Home appliances. EN keeps BANKING77, GPQA Diamond and MMLU-Pro; TR keeps BANKING77 and GPQA Diamond.
- Decision Index overall scores (Clef 61.2, Jev 57.9, Clef-flash 57.1).
- Workers AI Neurons pricing (10,000/day free; $0.011 per 1,000 Neurons).
- RL fine-tuning pipeline details (AI Gateway datasets, Containers RL sandbox, "Trainer", BYO Model redeploy).
- Architecture details: two-stage attention routing, rank-256 LoRA, label-smoothed cross-entropy (EN keeps the last one).
- Jev up to 255 choice options; endpoint path and SDK names; Jev "40x-200x faster" and "444.6x cheaper" claims; founder's ex-OpenAI background.
- Launch post authors (Chen, Reneau, Flansburg). Only Michelle Chen is named, as the source for The Register.
- Workers AI image limits in detail (4 MiB / 16 MP each, 8 MiB total, no remote URLs). Only "up to 4 images" is used.
- Startrise "disagreed on 12 of 168"; Construct's 95% CI (-1.1 to +8.8); Construct's 3.8x cost ratio wording.
- HN anecdotes: p50 350 ms vs 1.9 s; 41% coin vision test; "low-hanging fruit"; the human-in-the-loop question; wongarsu's latency-curve comment (it was in an earlier EN cut and was removed for length).
- X: @Lonely__MH's 100-question test and @_mantaroh_'s ECE remark.
- Flavio Copes' own latency measurements from Italy.

TR only (kept in EN):
- DEV confidence figures (0.99/0.71, 0.81/0.74); Clef-flash confusing look-alike company names; MMLU-Pro; workflow-eval margins; specific HN/X anecdotes; label-smoothed cross-entropy and Brier loss; the 32k state budget in prose (it stays in the table).

## Images

Placeholders follow IMAGES.md: `[[IMAGE: role | filename; alt: ... | caption]]`. The cover sits at the top; inlines 1 to 4 sit right after these H2s:
1. `decision-model-state-questions-diagram.webp`: "How Clef and Jev work under the hood" / "İki model nasıl çalışıyor"
2. `hosted-vs-self-hosted-fork.webp`: "Open weights, hosted API and lock-in" / "Açık ağırlık, kapalı kutu"
3. `vendor-benchmarks-vs-independent-tests.webp`: "Cloudflare's numbers vs independent tests" / "Cloudflare'in rakamları, bağımsız testlerin rakamları"
4. `threshold-dial-two-models.webp`: "Is Clef really a drop-in replacement for Jev?" / "Clef, Jev'in yerine doğrudan geçer mi?"

Captions and alts are the IMAGES.md text with one change: the TR caption for inline-4 now says "threshold'lar" instead of "eşikler", to match the body. The inline-2 captions ("Jev is only available as a hosted API", ~85 GB VRAM) match the drafts and The Register.

## Coordinator checklist before publish

- [ ] Pair EN and TR in Polylang (slugs are in front matter).
- [ ] Upload WebP files under their current descriptive filenames and insert them with the `wp-image-{ID}` class.
- [ ] Turn markdown tables into `wp-block-table`.
- [ ] Re-check prices and model status on the day of publishing (Workers AI pricing and TypeSafe docs can change; Jev rate limits are explicitly dynamic).
- [ ] Optional: ask TypeSafe and Cloudflare for comment on the latency-method caveat.
