# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-09-26
**Status:** 🟢 2 new locality pages shipped this run (Mahim → Santacruz, Wagle Estate → Thane), both self-sourced candidates (not from a queued list — the queue was empty going into this run). Site grew from 45 to 47 pages. 1 candidate logged as too geographically ambiguous to confidently assign (Jogeshwari), 1 confirmed over the 10km threshold (Uttan). No other technical/schema/AEO/E-E-A-T issues found; full 47-page verification sweep clean.

Site: 47 pages (1 homepage + 5 store pages + 41 locality pages) generated from `data/stores.json` via `generate.py`.

**Housekeeping:** checkout was clean and already up to date with `origin/main` (`9e35843`) at run start — no reconciliation needed.

**Network access note — still open, second consecutive run:** WebFetch to `nominatim.openstreetmap.org` and to the live site (`helmetstorenearme.in`) both returned `EGRESS_BLOCKED` again this run, same as 2026-09-25. This is a different, tool-level block from the sandbox-VM issue the task prompt describes (that one was fixed; this is the environment's own egress proxy denying these specific domains to WebFetch). WebSearch continues to work and was used as the geocoding substitute again — coordinates cross-referenced across multiple sources (Wikipedia, findlatitudeandlongitude.com, coordinatesfinder.com) before computing distance. Live-site verification (confirming the deployed site matches the repo) remains skipped for the second run in a row; everything else was verified against local generated output. Flagged again below — this should get a human look if it's still blocking a third day running.

---

## 1. Technical GEO/SEO

| Check | Result |
|---|---|
| Sitemap vs actual pages | ✅ 47/47 match exactly, no drift, no missing/extra URLs either direction |
| robots.txt bot coverage | ✅ `*`, GPTBot, ChatGPT-User, PerplexityBot, ClaudeBot, Google-Extended all `Allow: /`, sitemap referenced |
| JSON-LD parses | ✅ 0 errors across all 47 pages (programmatic parse of every `<script type="application/ld+json">` block) |
| Broken internal links | ✅ 0 found (every `href` resolves to a file on disk, fragments handled correctly) |
| Image alt text | ✅ Every `<img>` has non-empty alt text |
| Title tag length | ✅ All 47 ≤60 chars, all unique |
| Meta description length/uniqueness | ✅ All 47 unique, all ≤140 chars (decoded-entity length) |
| Canonical tags | ✅ Present and correct on every page |
| Live-site check (helmetstorenearme.in) | ⚠️ Not performed — WebFetch to the live domain returned `EGRESS_BLOCKED` this run again (see network note above) |

## 2. Schema & Structured Data

- `SportingGoodsStore` + `FAQPage` + `BreadcrumbList` + `openingHoursSpecification` present on all 46 store/locality pages; `Organization` + 5×`SportingGoodsStore` on the homepage.
- Re-scanned all 47 pages' JSON-LD for any `Review` node carrying a `reviewRating` field (the fabrication pattern fixed 2026-09-16) — **0 found**, fix holds.
- `AggregateRating` correctly present only where `reviews.rating` is a real, non-null value (Malad, Thane). Correctly absent for Santacruz, Mira Road and Navi Mumbai (`rating: null` in source data).
- New locality entries (Mahim, Wagle Estate) carry only `name`, `slug`, `km`, `minutes`, `blurb` — same four fields as every existing locality. No new field fabricated; distance/minutes computed, not invented.

## 3. AI Citability / AEO

- Entity-coverage re-check (programmatic): all 6 categories, all 3 brands (LS2, Crank1, MadDog), the EMI policy sentence, and the 7-day return policy sentence each still appear on 5/5 store pages after regeneration. No gap.
- Both new locality pages state a real, specific named landmark/route and a concrete distance/ride-time — no generic filler (Mahim Causeway/Mahim Junction station/dargah-church stretch for Mahim; Wagle Estate Road/TCS Neptune campus for Wagle Estate).
- `llms.txt` regenerated and spot-checked: both new locality names now appear in their correct store's "Serves:" line; phone numbers and `maps_url`s unchanged and correct.

## 4. Content E-E-A-T / Brand Authority

- Reviews, ratings, gallery photos and `youtube_id`s untouched this run — no changes made to any of these (bucket C).
- NAP consistency re-verified programmatically across all 47 pages: all 5 stores' phone numbers appear byte-for-byte on every page including the 2 new locality pages.
- Authoritativeness (press/backlinks): `audits/backlink-citation-plan.md` unchanged since 2026-09-17 — still the human's active research doc, not touched.

## 5. Platform Optimization

- FAQs unchanged this run; still cover the full natural buying-decision set (certification, try-before-buy, stock-check, EMI/returns, brands carried, exact location) on every page, including the 2 new locality pages (which reuse each store's FAQ set, same as every other locality page).

## 6. Local Reach Gaps

Queue was empty going into this run (all 10 prior candidates resolved 2026-09-25). Per the revised process, scanned each store's existing `localities` array for well-known nearby Mumbai localities not yet covered and attempted to resolve new candidates directly (Part 2 step 3 — no need to log-then-wait when a candidate can be resolved same-run). Method: WebSearch for coordinates (Nominatim/WebFetch still blocked — see network note), haversine distance to the assigned store's lat/lng, ×1.3 road-estimate, minutes derived from that store's existing km→minutes ratios, hand-written blurb naming a real, specific route/landmark.

Checked 4 candidates: Jogeshwari, Mahim, Uttan, Wagle Estate. **2 resolved and shipped, 1 logged as too ambiguous to confidently assign, 1 confirmed over threshold.**

### Added this run

| Locality | Store | Straight-line km | Road-est km (×1.3) | Minutes | Source |
|---|---|---|---|---|---|
| Mahim | Santacruz | 5.38 | 7.0 | 22-25 | Coordinates cross-checked across Wikipedia and findlatitudeandlongitude.com (both ~19.038/72.842, consistent). Minutes scaled up from the Andheri East (4.9km/16-19min) and Bandra East (4.6km/15-18min) entries, the closest existing ratio analogs for this store |
| Wagle Estate | Thane | 2.54 | 3.3 | 10-13 | Coordinates cross-checked across findlatitudeandlongitude.com, coordinatesfinder.com and distancesto.com (all ~19.198/72.951, consistent). Road-est km came out almost identical to the existing Kalwa entry (3.3km), so its 10-13min range was reused directly rather than re-derived |

Both blurbs are hand-written and name a real, specific landmark: the Mahim Causeway, Mahim Junction station and the dargah-church stretch by the bay for Mahim (with the SV Road-through-Bandra-and-Khar route to Santacruz); Wagle Estate Road and the TCS Neptune campus for Wagle Estate (with the short LBS Marg connection to the Khopat store). Neither is a template with only the name swapped.

### Logged — not resolved this run

| Locality | Store (candidate) | Reason not added |
|---|---|---|
| Jogeshwari | Malad or Santacruz (ambiguous) | Two independent coordinate sources disagreed on which store it's actually closer to: Jogeshwari railway station coordinates (19.1365/72.8490) put it closer to Malad (6.33km road-est) than Santacruz (7.45km), but the general/Wikipedia-area coordinate (19.12/72.85) puts it closer to Santacruz (5.22km) than Malad (8.68km). Both distances are under the ~10km ceiling either way, but I'm not confident enough which store's catchment it actually belongs to (Jogeshwari spans a wide east-west stretch) to assign it without guessing. Logged for a future run or human call rather than picking one arbitrarily. |
| Uttan | Mira Road | Coastal village near Bhayandar West; closest store is Mira Road but road-est comes to ~12.6km (9.69km straight-line ×1.3), over the ~10km ceiling. Not added. |

### Verification performed before shipping

- `python3 generate.py` re-run: 45 → 47 pages, zero errors.
- Re-ran the full technical checklist (titles/descriptions, JSON-LD, broken links, alt text, sitemap-vs-files parity, llms.txt) against the regenerated output — all pass, see Section 1.
- Re-ran entity-coverage and NAP checks — both still pass with the new pages included.
- Confirmed sibling-page diffs (areaServed schema, cross-linked "nearby localities" blocks on other pages in the same store) were the expected knock-on effect of adding a locality, not a regression — spot-checked one diff (`near/santacruz/andheri-east/index.html`) to confirm.

---

## Candidate localities awaiting human geocoding

| Locality | Candidate store | Note |
|---|---|---|
| Jogeshwari | Malad or Santacruz | Ambiguous — see Section 6 above. Needs either a more precise sub-area decision (e.g. Jogeshwari East vs West) or a human call on which store's page it should live on. |

---

## Action Plan

| Finding | Category | Action Taken | Notes |
|---|---|---|---|
| 2 new well-known localities identified as missing (Mahim, Wagle Estate) | Local Reach | Geocoded via WebSearch (Nominatim/WebFetch blocked, see network note), added as new locality pages | See Section 6 for sources and distances |
| Jogeshwari and Uttan checked as candidates | Local Reach | Jogeshwari logged as ambiguous (conflicting store assignment across coordinate sources); Uttan confirmed over the 10km threshold, not added | See Section 6 tables |
| Full technical/schema/AEO/E-E-A-T sweep across all 47 pages | All | Re-verified, 0 issues found | Titles/descriptions, JSON-LD, links, alt text, canonicals, robots.txt, entity coverage, NAP, llms.txt all clean post-regeneration |
| WebFetch blocked for all tested domains (Nominatim, the live site) — second consecutive run | Technical GEO/SEO | Flagged again, not fixable from this session — environment-level egress proxy | Adapted to WebSearch-only geocoding again; live-site verification skipped for the 2nd run running |

## Carried over from previous runs

| Finding | Category | Status | First flagged |
|---|---|---|---|
| No third-party press/citations/backlinks (Authoritativeness) | E-E-A-T / Brand Authority | Strategic, not mechanical — human actively working this via `audits/backlink-citation-plan.md` | 2026-09-15 |
| `generate.py`'s sitemap `lastmod` is stamped to the run date on every invocation rather than tracking real per-page content changes | Technical GEO/SEO | Noted, not fixed — needs a human call on the right approach (e.g. hash-based or data-driven lastmod) since it changes generator behavior, not just data | 2026-09-18 |
| WebFetch returns `EGRESS_BLOCKED` for external domains in this environment (Nominatim, the live site itself), despite being expected to work per the task prompt | Technical GEO/SEO / Local Reach | Open, now 2 consecutive runs — worked around via WebSearch each time; live-site checks remain unavailable until this is fixed at the environment level | 2026-09-25 |
| Jogeshwari — ambiguous store assignment | Local Reach | Open — see Candidate table above | 2026-09-26 |
