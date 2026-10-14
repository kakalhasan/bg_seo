# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-10-14
**Status:** 🟢 Clean sweep — zero issues across all six categories, no data changes needed. Re-checked the one open candidate (Rai); still not confidently resolvable. No new candidate localities surfaced.

Site: unchanged at **59 pages** (1 homepage + 5 store pages + 53 locality pages). No pages added or removed this run.

**Housekeeping:** Git checkout started clean — `main` already checked out and up to date with `origin/main` (tip `e492d75`), working tree clean. No reconciliation needed.

**Network access note — WebFetch still non-functional, 19th consecutive run:** Directly re-tested at run start against three different hosts — `https://helmetstorenearme.in/`, `https://nominatim.openstreetmap.org/search`, and `https://en.wikipedia.org/wiki/Mira_Road` — **all three failed immediately with `getaddrinfo ENOTFOUND <host>`**, the same failure mode reported every run since 2026-10-08 (and `EGRESS_BLOCKED` before that, since 2026-09-13). This directly contradicts this run's own task brief, which asserts WebFetch runs on Anthropic infrastructure outside the sandbox's egress block and should now work. It does not, in this sandbox, for any external host tried. WebSearch continues to work normally and was used for all research this run — including a fresh attempt at Rai's coordinates via a postal-code directory site surfaced through WebSearch rather than a direct Nominatim query.

---

## 1. Technical GEO/SEO

| Check | Result |
|---|---|
| Sitemap vs actual pages | ✅ 59/59 match exactly |
| robots.txt bot coverage | ✅ `*`, GPTBot, ChatGPT-User, PerplexityBot, ClaudeBot, Google-Extended all `Allow: /`, sitemap referenced |
| JSON-LD parses | ✅ 0 errors across all 59 pages |
| Broken internal links | ✅ 0 found |
| Image alt text | ✅ Every `<img>` has non-empty alt text |
| Title tag length | ✅ All 59 ≤60 chars, all unique |
| Meta description length/uniqueness | ✅ All 59 unique, all ≤140 chars |
| Canonical tags | ✅ Present and correct on every page |
| Live-site check (helmetstorenearme.in) | ⚠️ Not performed — WebFetch failed with `getaddrinfo ENOTFOUND` (see network note above) |

Verified via a programmatic sweep script (written this run, parses every generated HTML file against `data/stores.json`) rather than spot checks.

## 2. Schema & Structured Data

- `SportingGoodsStore` + `FAQPage` + `BreadcrumbList` + `openingHoursSpecification` present on all 58 store/locality pages; `Organization` + 5×`SportingGoodsStore` confirmed on the homepage.
- Re-scanned all 59 pages' JSON-LD for the reviewRating-fabrication pattern (fixed 2026-09-16) — **0 found**, fix holds.
- `AggregateRating` programmatically checked on all 5 store pages: present with correct `ratingValue`/`reviewCount` only where `reviews.rating` is a real, non-null value (Malad 4.7/2445, Thane 4.5/34); correctly absent for Santacruz, Mira Road and Navi Mumbai, since `rating` is null for all three in source data even though Santacruz (count 434) and Mira Road (count 317) carry a review *count*. No change from prior runs.

## 3. AI Citability / AEO

- Entity-coverage re-check: all 6 categories and all 3 brands (LS2, Crank1, MadDog) appear verbatim on all 5 store pages; the EMI policy sentence and the 7-day return policy sentence both appear on all 5 store pages. No gap.
- `llms.txt` re-checked line-by-line against current `data/stores.json`: store count (5), every phone number, and all 53 locality names match exactly. No drift.

## 4. Content E-E-A-T / Brand Authority

- Reviews, ratings, gallery photos and `youtube_id`s untouched this run (bucket C, no changes).
- NAP consistency re-verified programmatically across all 58 store/locality pages: each store's phone number appears byte-for-byte on every page belonging to that store.
- Authoritativeness (press/backlinks): `audits/backlink-citation-plan.md` unchanged since 2026-09-17 — still the human's active research doc, not touched this run.

## 5. Platform Optimization

- FAQs unchanged this run; no new buying-decision gap surfaced.

## 6. Local Reach Gaps

**No locality pages added this run.**

- **Rai (Mira-Bhayandar) — re-checked, still open, one new partial data point found.** A postal-code directory site (surfaced via WebSearch, not a direct geocoder — Nominatim remains unreachable) lists "Rai B.O" (the Rai post office under pincode 401101) at approximately 19.298, 72.825. The source itself doesn't state how that figure was derived and isn't an authoritative survey, so treated as approximate at best. Computed anyway for reference: straight-line ≈5.7 km from the Mira Road store (19.2843751, 72.8772246) → road-est ≈7.4 km, which *would* be inside the 10 km ceiling if the coordinate is trustworthy. But the blurb-writing requirement is still unmet: searched again this run for a confirmed, specific landmark inside Rai village itself (temple, church, junction) and found none — only the single uncorroborated "Walchand Palace" mention already in the candidate table, plus general East-Indian-village context (Rai, Murdha, Morva, Uttan, Tarodi formed under Portuguese-era Vasai) that doesn't amount to a quotable, specific route or landmark. Left unresolved — same conclusion as every run since 2026-10-11, now with one additional (low-confidence) coordinate on record for whoever resolves this next.
- **No new candidate localities surfaced.** Checked the areas immediately around each store against the existing locality lists (14 for Malad, 13 for Santacruz, 13 for Thane, 7 for Navi Mumbai, 6 for Mira Road) and against the full history of previously-examined names in this file's git history (Kasarvadavali, Aarey Colony, Airoli, Ulwe, Mira Road West, Koparkhairane, Ghansoli, Uttan, Dahisar West, Balkum, Kanakia, Nerul East/West, Panvel, Poonam Sagar, Hiranandani Estate, BKC, Teen Hath Naka/Khopat/Kopri — all previously rejected as either too far, already covered as a named landmark inside an existing blurb, or overlapping the store's own immediate address). Specifically re-verified Uttan and Balkum's old distance rulings held (Uttan: ≈9.15 km straight-line from Mira Road → ≈11.9 km road-est, confirms it's over threshold). Nothing new found this run; the five stores' coverage appears to be approaching saturation for genuinely distinct, in-range localities.

### Verification performed before closing out this run

- Full technical sweep via a new programmatic script (`python3 generate.py` re-run first to confirm idempotency, then parsed all 59 generated HTML files): titles/descriptions length and uniqueness, JSON-LD validity and reviewRating-fabrication scan, broken internal links, alt text, sitemap-vs-files parity, canonical correctness, llms.txt drift, entity coverage, NAP consistency, AggregateRating correctness — **0 issues found**.
- Git state confirmed clean and already up to date with `origin/main` at run start — no reconciliation needed.
- WebFetch directly re-tested against three different hosts at run start — confirmed still non-functional (`getaddrinfo ENOTFOUND`) for all three, 19th consecutive run.
- Recomputed haversine distances for Rai (new candidate coordinate) and re-confirmed Uttan's prior rejection, both by hand in Python.

---

## Candidate localities awaiting human geocoding

| Locality | Nearest store | Notes |
|---|---|---|
| Rai | Mira Road | Genuine, distinct East Indian village in Mira-Bhayandar (separate postal code 401101), but still no reliably-sourced coordinates, distance, or corroborated landmark after four runs of WebSearch-only research. This run found one additional low-confidence coordinate (a postal-directory site, ≈19.298, 72.825, undocumented derivation) giving a road-est ≈7.4 km if trusted — inside the radius, but the still-missing piece is a confirmed, specific, non-generic landmark inside Rai itself to write an honest blurb around. Needs either working geocoding/Nominatim access, a Marathi-language local source, or a human-supplied landmark to resolve safely. First logged 2026-10-11, re-checked 2026-10-12 through 2026-10-14 with no resolution yet. |

---

## Action Plan

| Finding | Category | Action Taken | Notes |
|---|---|---|---|
| Full technical/schema/AEO/E-E-A-T sweep across all 59 pages | All | Verified via a new programmatic sweep script, 0 issues found | Titles/descriptions, JSON-LD, links, alt text, canonicals, robots.txt, entity coverage, NAP, llms.txt, AggregateRating correctness all clean |
| Rai (Mira-Bhayandar) — re-checked this run | Local Reach | Found one additional low-confidence coordinate; still no confirmed landmark for an honest blurb | Left in candidate table, updated with new partial data point |
| Uttan / Balkum — re-verified prior rejections still hold | Local Reach | Uttan distance recomputed (≈11.9 km road-est, over threshold) | No change, not re-logged |
| No new candidate localities found | Local Reach | Checked all 5 stores' surrounding areas against full prior-rejection history | Coverage appears close to saturation for genuinely distinct, in-range localities |
| WebFetch non-functional, 19th consecutive run, despite this run's brief asserting it should work | Technical GEO/SEO / Local Reach | Re-tested directly against 3 different hosts at run start — all failed with `getaddrinfo ENOTFOUND` | All research this run used WebSearch only |
| Git state at run start | Housekeeping | Already clean and up to date with `origin/main` — no action needed | — |

## Carried over from previous runs

| Finding | Category | Status | First flagged |
|---|---|---|---|
| No third-party press/citations/backlinks (Authoritativeness) | E-E-A-T / Brand Authority | Strategic, not mechanical — human actively working this via `audits/backlink-citation-plan.md` (unchanged since 2026-09-17) | 2026-09-15 |
| `generate.py`'s sitemap `lastmod` is stamped to the run date on every invocation rather than tracking real per-page content changes | Technical GEO/SEO | Noted, not fixed — needs a human call on the right approach (e.g. hash-based or data-driven lastmod) since it changes generator behavior, not just data | 2026-09-18 |
| WebFetch cannot reach any external host from this session (`getaddrinfo ENOTFOUND`) | Technical GEO/SEO / Local Reach | Open, now 19 consecutive runs — worked around via WebSearch each time; live-site checks and precise Nominatim geocoding remain unavailable until this is fixed at the environment level | 2026-09-25 |
