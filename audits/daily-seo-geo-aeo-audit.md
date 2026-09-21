# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-09-20
**Status:** 🟢 Clean run — zero issues found across all six categories. No auto-fixes needed. Two new candidate localities logged (Khar East near Santacruz, Panchpakhadi near Thane); the 5 existing candidates remain unresolved, carried over — not duplicated.

Site: 30 pages (1 homepage + 5 store pages + 24 locality pages) generated from `data/stores.json` via `generate.py`. Live network access to `helmetstorenearme.in` and `nominatim.openstreetmap.org` remains categorically blocked in this sandbox (failing since 2026-09-13) — audit performed entirely against the local generated output and source data, per the revised process.

**Housekeeping note:** local checkout started on a detached HEAD at `60e790a` (yesterday's commit), matching `origin/main` after fetch, but the local `main` branch ref was 2 commits behind (`7036c7e`). Fast-forwarded local `main` to `origin/main` (`60e790a`) and checked it out — no lost work, nothing to reconcile beyond that.

**Generator note:** `python3 generate.py` was re-run to confirm zero drift between source data and committed HTML. All 30 pages matched byte-for-byte except `sitemap.xml`, which unconditionally re-stamps every `<lastmod>` to the run date regardless of whether content changed (see carried-over item below). Reverted the sitemap-only diff (`git checkout -- sitemap.xml`) rather than commit it, consistent with every prior clean run.

---

## 1. Technical GEO/SEO

| Check | Result |
|---|---|
| Sitemap vs actual pages | ✅ 30/30 match exactly, no drift (content-wise; see generator note above on `lastmod` churn) |
| robots.txt bot coverage | ✅ `*`, GPTBot, ChatGPT-User, PerplexityBot, ClaudeBot, Google-Extended all `Allow: /`, sitemap referenced |
| JSON-LD parses | ✅ 0 errors across all 30 pages (programmatic parse of every `<script type="application/ld+json">` block) |
| Broken internal links | ✅ 0 found (every `href="/..."` resolves to a file on disk) |
| Image alt text | ✅ Every `<img>` has non-empty alt text; all gallery files referenced in `data/stores.json` verified present on disk |
| Title tag length | ✅ All 30 ≤60 chars, all unique |
| Meta description length/uniqueness | ✅ All 30 unique, all ≤140 chars (decoded-entity length) |
| Canonical tags | ✅ Present and correct on every page |

## 2. Schema & Structured Data

- `SportingGoodsStore` + `FAQPage` + `BreadcrumbList` + `openingHoursSpecification` present on all 29 store/locality pages; `Organization` + 5×`SportingGoodsStore` on the homepage.
- Re-scanned all 30 pages' JSON-LD for any `Review` node carrying a `reviewRating` field (the fabrication pattern fixed 2026-09-16) — **0 found**, fix holds.
- `AggregateRating` correctly present only where `reviews.rating` is a real, non-null value (Malad 4.7, Thane 4.5); correctly absent for Santacruz, Mira Road and Navi Mumbai, whose source data has `rating: null` (Justdial/Google listings with a review count but no aggregate star value surfaced yet). This is honest missing data, not a bug — no value fabricated to fill it.
- No other plausible-looking-guess values found in schema; every field traces to an explicit value in `data/stores.json`.

## 3. AI Citability / AEO

- Entity-coverage re-check (programmatic, HTML-entity-aware, across all 5 store pages): all 6 product categories, all 3 brands (LS2, Crank1, MadDog), ISI/ECE/DOT certification, EMI policy, and 7-day return policy each appear on 5/5 store pages. No gap found.
- Every store and locality page states a real, specific address, phone number, named landmark, and real distance/ride-time — no generic filler.
- `llms.txt` cross-checked field-by-field against current `data/stores.json` — every phone number, every `maps_url`, and every locality name across all 5 stores confirmed present — 100% accurate, no drift.

## 4. Content E-E-A-T / Brand Authority

- Reviews are real and sourced (`source` + `source_url` present for all 5 stores' review blocks — Google/Justdial/Magicpin).
- Real store photos: all gallery files referenced in `data/stores.json` verified present on disk for all 5 stores.
- Real videos: a distinct YouTube store-tour `youtube_id` present for all 5 stores.
- NAP consistency: verified programmatically — all 5 stores' phone numbers appear byte-for-byte on all their store/locality pages.
- Authoritativeness (press/backlinks): `audits/backlink-citation-plan.md` unchanged since 2026-09-17 — still the human's active research doc. No repo state change to note this run; remains human-executed outreach work, not touched by this routine.

## 5. Platform Optimization

- FAQs cover the full natural buying-decision set: certification, try-before-buy, stock-check, EMI/returns, brands carried.
- No further gaps found against the "what would an AI Overview/ChatGPT/Perplexity want to quote" checklist this run.

## 6. Local Reach Gaps

- Network egress to `nominatim.openstreetmap.org` and `helmetstorenearme.in` remains blocked — no live geocoding attempted, per the revised process. Bucket (B) not used this run.
- The 5 candidates logged 2026-09-17/2026-09-19 (Malad East, Santacruz East, Kapurbawdi, Kharghar, Dahisar) are **still not present** in `data/stores.json` — still awaiting human geocoding, carried over below (not duplicated).
- Two new candidates identified this run, both following the same well-known-adjacency pattern already used for Malad East/Santacruz East: **Khar East** (Santacruz store — Khar West is already covered; Khar East is the standard Western-line station-pair locality directly across the tracks) and **Panchpakhadi** (Thane store — a well-known, long-established locality immediately adjacent to Thane railway station and the already-covered Naupada). Both added to the candidate list below, no distance claimed.

---

## Candidate localities awaiting human geocoding

None currently queued — see the 2026-09-21 update below, which resolved all 7 candidates logged as of the previous run.

---

## 2026-09-21 update (human session, live network access)

**All 7 queued candidates: resolved.** Same handoff pattern as the 2026-09-17 batch — the cloud routine's sandbox still can't reach `nominatim.openstreetmap.org` (blocked since 2026-09-13), so it correctly logged plausible candidates rather than guessing coordinates. Geocoded all 7 from an interactive session with live network access:

| Locality | Store | Distance | Verified via |
|---|---|---|---|
| Malad East | Malad | 2.9 km | Nominatim, live (suburb node) |
| Santacruz East | Santacruz | 2.8 km | Nominatim, live (no suburb-level node returned for this one — anchored to a named building inside the Santacruz East/Vakola area instead) |
| Khar East | Santacruz | 2.6 km | Nominatim, live (no locality node for "Khar East" itself — anchored to Khar Road station, which straddles both sides) |
| Kapurbawdi | Thane | 2.5 km | Nominatim, live (anchored to the Majiwada–Kapurbawdi flyover junction) |
| Panchpakhadi | Thane | 1.6 km | Nominatim, live (locality node) |
| Kharghar | Navi Mumbai | 5.3 km | Nominatim, live (anchored to Kharghar station) |
| Dahisar | Mira Road | 5.6 km | Nominatim, live (anchored to Dahisar station) |

All 7 added as real locality pages (hand-written blurbs, real landmarks — Malad subway/Pathanwadi bridge, Vakola/Kalina/BKC, Khar subway/Linking Road, the Ghodbunder Road–EEH junction, Thane station/Panchpakhadi naka, CIDCO/Central Park, the Dahisar Toll Naka). Site is now 37 pages (was 30). Distances above are straight-line-to-road estimates (~1.3×) consistent with how every other locality on this site states its distance — not a guarantee.

No further action needed on this queue until the routine logs new candidates.

---

## Action Plan

| Finding | Category | Action Taken | Notes |
|---|---|---|---|
| Full technical/schema/AEO/E-E-A-T sweep across all 30 pages | All | Re-verified, 0 issues found | Titles/descriptions, JSON-LD, links, alt text, canonicals, robots.txt, entity coverage, NAP, llms.txt all clean |
| `generate.py` re-run produced a `sitemap.xml`-only diff (all 30 `<lastmod>` bumped to today) despite no actual content change | Technical GEO/SEO | **Reverted**, not committed | Same recurring behavior as every prior clean run — see carried-over item below |
| Two new candidate localities identified (Khar East near Santacruz, Panchpakhadi near Thane) | Local Reach | Logged to candidate list, no page written | Awaiting human geocoding, per revised process |

## Carried over from previous runs

| Finding | Category | Status | First flagged |
|---|---|---|---|
| No third-party press/citations/backlinks (Authoritativeness) | E-E-A-T / Brand Authority | Strategic, not mechanical — human actively working this via `audits/backlink-citation-plan.md` | 2026-09-15 |
| `generate.py`'s sitemap `lastmod` is stamped to the run date on every invocation rather than tracking real per-page content changes | Technical GEO/SEO | Noted, not fixed — needs a human call on the right approach (e.g. hash-based or data-driven lastmod) since it changes generator behavior, not just data | 2026-09-18 |
