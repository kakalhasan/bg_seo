# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-09-16
**Status:** 🟡 Minor fix applied — found and corrected a fabricated per-review star rating in the Malad store's schema (present since the site's original build, never flagged before). Everything else re-verified clean. No new locality page (network to nominatim/site blocked again).

Site: 26 pages (1 homepage + 5 store pages + 20 locality pages) generated from `data/stores.json` via `generate.py`. Live network access to `helmetstorenearme.in` and `nominatim.openstreetmap.org` was blocked by the sandbox's egress policy this run (connection failures on both) — audit performed against the local generated output and source data instead.

**Housekeeping note:** local `main` was found on a detached HEAD at the start of this run, matching `origin/main`'s tip exactly (no unpushed work, no divergence — just a detached checkout). Switched to `main` and fast-forwarded 6 commits with `git merge --ff-only`; nothing was lost or discarded.

---

## 1. Technical GEO/SEO

| Check | Result |
|---|---|
| Sitemap vs actual pages | ✅ 26/26 match exactly, no drift |
| robots.txt bot coverage | ✅ `*`, GPTBot, ChatGPT-User, PerplexityBot, ClaudeBot, Google-Extended all `Allow: /` |
| JSON-LD parses | ✅ 0 errors across all 26 pages (re-checked after today's fix) |
| Broken internal links | ✅ 0 found |
| Image alt text | ✅ All images have specific, non-generic alt text naming the store; all gallery files referenced in `data/stores.json` verified present on disk |
| Title tag length | ✅ All 26 ≤60 chars, all unique (SuperSEO threshold) |
| Meta description length/uniqueness | ✅ All 26 unique, all ≤140 chars (decoded-entity length; SuperSEO threshold) |
| Canonical tags | ✅ Correct, self-referencing on every page |
| Sitemap `lastmod` bump | Expected — reflects today's real content change (the reviewRating fix below), not committed on quiet days |

## 2. Schema & Structured Data

- `SportingGoodsStore` + `FAQPage` + `BreadcrumbList` present on all 25 store/locality pages; `Organization` + 5×`SportingGoodsStore` on the homepage.
- `openingHoursSpecification` (11am–9pm, all 7 days) present on every store's schema, mirroring `data/stores.json`.
- `postalCode` present in every store's `PostalAddress` schema.
- `aggregateRating` re-checked against `data/stores.json` for all 5 stores — no mismatches:
  - Malad: 4.7 / 2445 reviews ✅ · Thane: 4.5 / 34 ✅ · Santacruz / Mira Road: count only, no rating → correctly omitted ✅ · Navi Mumbai: 6 quotes, no rating/count → correctly omitted ✅
- **Fixed this run:** `generate.py`'s `review_schema_fields()` was assigning the store's *aggregate* rating (e.g. 4.7) as the `reviewRating` on each individual `Review` object for Malad's 4 named quotes — asserting a specific per-reviewer star value that doesn't exist in the source data (only the store-wide aggregate across 2445 reviews is sourced). This has been present since the original site build (commit `c203bb6`) and was never previously flagged. It directly matches the audit's "never fabricate a field to fill a schema gap — omit rather than guess" rule, so `reviewRating` is now omitted from individual reviews; the legitimately-sourced `aggregateRating` block is untouched. Verified: JSON-LD still parses on all pages, no other fields changed (diff confirmed to 4 `reviewRating` removals on Malad's store/homepage/4×near-page schema blocks only).
- `priceRange` intentionally absent — fabricated placeholder removed previously, correctly stays omitted (SKU range too wide to state meaningfully).

## 3. AI Citability / AEO

- Every store and locality page states a real, specific address, phone number, named landmark, and real distance/ride-time — no generic filler.
- FAQs (6 per store) cover: ISI/DOT/ECE certification, try-before-buy, exact location, stock-check, EMI/returns, and brand names.
- Entity-coverage re-check (programmatic grep across all 5 store pages): all 6 product categories, EMI policy, 7-day return policy, ISI marking, ECE/DOT certification, MadDog brand name, and visible "11 am" hours text each appear on 5/5 store pages. No gap found.
- `llms.txt` cross-checked field-by-field against current `data/stores.json` (phones, addresses, brands, policies, localities served) — 100% accurate, no drift.

## 4. Content E-E-A-T / Brand Authority

- Reviews are real, sourced (Google, Justdial, Magicpin, each with a `source_url`), rendered only where the underlying data has them — no fabrication or embellishment of review text, rating, or count found. (Today's fix removed a fabricated *per-review* rating derived from the real aggregate — see §2; the underlying review text and store-level rating were never wrong.)
- Real store photos: all files referenced in `data/stores.json` verified present on disk.
- Real videos: a distinct YouTube store-tour `youtube_id` present for all 5 stores.
- NAP consistency: verified programmatically — the identical 5-phone-number set (and shared footer) appears byte-for-byte across all 26 pages. Single source of truth, no drift possible by construction.
- Authoritativeness (third-party press/citations/backlinks): still a strategic gap, not a mechanical one — no action taken, needs human outreach.

## 5. Platform Optimization

- FAQs cover the full natural buying-decision set: certification, try-before-buy, stock-check, EMI/returns, and brands carried.
- No further gaps found against the "what would an AI Overview want to quote" checklist this run.

## 6. Local Reach Gaps

- Network egress to `nominatim.openstreetmap.org` and `helmetstorenearme.in` was blocked again this run — no new locality page added, bucket (B) skipped per instructions rather than guessing coordinates.
- Same candidate localities as prior runs, still worth geocoding-checking once network access is available: Charkop (near Malad), Juhu (near Santacruz), Bhayandar West (near Mira Road), Ghodbunder Road corridor (near Thane).

---

## Action Plan

| Finding | Category | Action Taken (auto-fixed / new page added / needs human) | Notes |
|---|---|---|---|
| Detached HEAD at session start, matching `origin/main` tip exactly | Housekeeping | **Fast-forwarded** | No divergence, nothing lost — `git checkout main && git merge --ff-only origin/main` |
| Individual `Review.reviewRating` in Malad's schema fabricated a per-reviewer star value from the store's aggregate rating | Schema & Structured Data | **Auto-fixed** | Edited `generate.py` to omit `reviewRating` on individual reviews (no per-review rating exists in source data); regenerated; re-verified JSON-LD parses on all 26 pages and no other fields changed |
| Full technical/schema/AEO/E-E-A-T sweep | All | Re-verified, no other new issues | 0 broken links, 26/26 unique titles ≤60 chars, 26/26 unique descriptions ≤140 chars, all other schema valid, NAP consistent site-wide |
| No new locality page this run | Local Reach | Not attempted — blocked | Network to nominatim/site unavailable in sandbox this run |

## Carried over from previous runs

| Finding | Category | Status | First flagged |
|---|---|---|---|
| No third-party press/citations/backlinks (Authoritativeness) | E-E-A-T / Brand Authority | Strategic, not mechanical — needs human-approved outreach, in progress (see below) | 2026-09-15 |

## 2026-09-17 update (human session, live network access)

**Candidate localities: resolved.** The cloud routine's sandbox has hit a hard "connection failed / 403" wall on `nominatim.openstreetmap.org` and `helmetstorenearme.in` on every single automated run since 2026-09-13 — this looks like a categorical egress-allowlist policy on the CCR sandbox, not a transient outage, so waiting for it to "become available" isn't a real plan. Geocoded all 4 queued candidates directly from an interactive session (which has normal network access) instead:

| Locality | Store | Distance | Verified via |
|---|---|---|---|
| Charkop | Malad | 3.3 km | Nominatim, live |
| Juhu | Santacruz | 2.5 km | Nominatim, live |
| Bhayandar West | Mira Road | 3.4 km | Nominatim, live (note: "Bhayandar West" needed a more specific query — a bare query returned Bhayandar **East** coordinates) |
| Ghodbunder Road (corridor) | Thane | 7.5 km | Nominatim, live |

All 4 added as real locality pages (hand-written blurbs, real landmarks — Charkop Market, JVPD Scheme/Juhu Circle, Jesal Park/Maxus Mall, Kasarvadavali/Waghbil/Hiranandani Estate). Site is now 30 pages (was 26).

**Going forward — the routine's Local Reach instructions are changing** (see updated prompt): since live geocoding from the sandbox isn't realistically going to start working, the routine should stop attempting it and instead just **log** any new candidate locality names it reasons are plausible (from general knowledge, unverified) under a queue in this file, for a human to geocode and add in a session like this one — the same handoff pattern that just resolved this batch. This keeps the daily routine honest about what it can't do rather than repeating a failing action indefinitely.

**Backlinks/citations: work started, not delegated to the routine.** This is outreach-shaped work (external sites, in some cases real emails sent as the business) — it needs human review before anything goes out, so it's being handled in interactive sessions, never added to the unattended daily job.
