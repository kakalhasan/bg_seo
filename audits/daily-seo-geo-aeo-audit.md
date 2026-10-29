# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-10-29
**Status:** 🟢 Clean sweep, no changes needed. Full programmatic re-sweep of all 62 pages (technical, schema, entity-coverage, NAP, llms.txt) found 0 issues. No new locality pages added — one new lead (Liberty Garden, Malad) was investigated and correctly excluded as a non-issue (too close to/overlapping with the store's own immediate area, same pattern as the Chincholi Bunder exclusion on 2026-10-28), not force-fit. All four already-open candidates (Uttan, Ghatkopar West, Waghbil, Prabhadevi) were re-checked via WebSearch; none resolved, reasoning unchanged. Site stays at **62 pages** (1 homepage + 5 store pages + 56 locality pages).

**Housekeeping:** Repo was on a detached HEAD matching `origin/main` at run start (2 commits behind local `main` branch pointer, from the 2026-10-27/28 runs). Checked out `main` and fast-forwarded cleanly, no divergence, no lost work.

**Network access note — WebFetch/Nominatim still blocked at the session network-policy level, 33rd consecutive run:** Re-tested directly at run start against `https://helmetstorenearme.in/` and `https://nominatim.openstreetmap.org/search` via WebFetch — both failed with `getaddrinfo ENOTFOUND <host>`, with the tool's own error message explicitly stating the host is outside the session's allowed network domains. Cross-checked directly via `curl` through the sandbox's configured egress proxy (`$HTTPS_PROXY/__agentproxy/status`): confirms a policy-level `403` gateway denial on arbitrary outbound hosts (the status endpoint's `recentRelayFailures` log shows the same `connect_rejected`/`403` pattern against several other non-allowlisted hosts, e.g. `mcp.asana.com`, `mcp.box.com`). This is a session network-allowlist restriction, not a transient DNS failure — it will not self-resolve without the host being added to the session's allowed domains. This run's task brief again claimed WebFetch should be unaffected since it runs on Anthropic's infrastructure rather than the sandbox VM; not borne out, 33rd run in a row. `WebSearch` continues to work fully and was used for all research this run. No live-site fetch and no direct Nominatim JSON geocoding were possible.

---

## 1. Technical GEO/SEO

| Check | Result |
|---|---|
| Sitemap vs actual pages | ✅ 62/62 match exactly, 0 missing, 0 extra |
| robots.txt bot coverage | ✅ `*`, GPTBot, ChatGPT-User, PerplexityBot, ClaudeBot, Google-Extended all `Allow: /`, sitemap referenced |
| JSON-LD parses | ✅ 0 errors across all 62 pages (re-verified after fix) |
| Broken internal links | ✅ 0 found (fresh link-checker sweep) |
| Image alt text | ✅ All 84 `<img>` tags have non-empty, descriptive alt text |
| Title tag length | ✅ All 62 ≤60 chars (post-entity-decode), all unique |
| Meta description length/uniqueness | ✅ All 62 unique, all ≤140 chars (post-entity-decode) |
| Canonical tags | ✅ Present and correct on every page |
| Open Graph `og:site_name` | ✅ Present on all 62 pages (fixed 2026-10-28), re-verified this run |
| Live-site check (helmetstorenearme.in) | ⚠️ Not performed — WebFetch failed, session-level network block (see network note above) |

**Known open issue (not re-tabled below, see Carried-over note):** `generate.py` stamps every page's sitemap `lastmod` to the run date on every invocation rather than tracking real per-page content changes (`generate.py` — `TODAY = datetime.date.today().isoformat()`). No regeneration ran this run (no A/B changes), so `lastmod` correctly stayed at 2026-10-28 (last real content change) rather than bumping to today — confirmed by inspection of `sitemap.xml`. Still needs a human call on approach (hash-based or data-driven lastmod) for the days when a regeneration *does* run with no real content change. First flagged 2026-09-18.

## 2. Schema & Structured Data

- `SportingGoodsStore` + `FAQPage` + `BreadcrumbList` present on all 61 store/locality pages, verified programmatically this run — 0 missing.
- Re-scanned all 62 pages' JSON-LD for the reviewRating-fabrication pattern (fixed 2026-09-16) — **0 found**, fix holds. No individual `Review` object anywhere on the site carries a `reviewRating`.
- `AggregateRating` programmatically re-verified against source `reviews.rating`/`reviews.count`: Malad (4.7/2445) and Thane (4.5/34) carry correct values; Santacruz, Mira Road and Navi Mumbai correctly carry no `AggregateRating` (source `reviews.rating` is `null` for all three). 0 mismatches.

## 3. AI Citability / AEO

- Entity-coverage re-check: all 6 brand-wide categories, all 3 brands (LS2, Crank1, MadDog), and both brand-wide policy sentences (EMI, 7-day return) appear verbatim (post-`html.unescape()`) somewhere on the site. 0 gaps.
- `llms.txt` re-checked programmatically against current `data/stores.json` — every store name and phone number, and all 56 locality names, found verbatim. No drift.
- No new entity-coverage or FAQ gaps surfaced this run; see Carried-over note for the standing `site_name`/`tagline` and MadDog-on-homepage non-issues (unchanged).

## 4. Content E-E-A-T / Brand Authority

- Reviews, ratings, gallery photos and `youtube_id`s untouched this run (bucket C, no changes).
- NAP consistency re-verified programmatically across all 61 store/locality pages: each store's phone number appears on every page belonging to that store, 0 mismatches.
- Authoritativeness (press/backlinks): still the human's active research track via `audits/backlink-citation-plan.md`; no change to that file this run, not touched.

## 5. Platform Optimization

- Spot-checked FAQ coverage across all 5 stores (certification, try-on, location, stock-check — 4 FAQs each, identical pattern per store). No new buying-decision gap surfaced; matches the standing conclusion that EMI/returns are covered elsewhere on each page (intro copy/policy blocks) even though not phrased as a dedicated FAQ.

## 6. Local Reach Gaps

**No new locality pages added this run.** One new lead (Liberty Garden, nominally Malad) was investigated and ruled out — not a gap, not even a candidate. All four previously-logged candidates (Waghbil, Prabhadevi, Uttan, Ghatkopar West) were re-checked via WebSearch; none resolved, reasoning unchanged.

- **Liberty Garden (nominal: Malad) — investigated, NOT a gap, not logged.** Confirmed via WebSearch as a real, named Malad West locality/park, pincode 400064 (same pincode as the store's own address). But further searches locate it as sitting immediately north of Chincholi Bunder Road, between the road and Mindspace — i.e. the same immediate neighbourhood the store itself sits in, not a separate "near me" catchment. A real-estate-directory coordinate found for it (19.21322°N, 72.79667°E) was cross-checked and rejected as unreliable: that point sits ~5.7km northwest of the store, in the direction of Mira Road/Bhayandar, which contradicts every other source placing Liberty Garden immediately beside Chincholi Bunder Road. Correctly excluded on the same reasoning as the Chincholi Bunder exclusion (2026-10-28) — too close to/overlapping with the store's own location — not logged to the candidate table since this isn't an open question.
- **Waghbil (Thane) — re-checked via WebSearch, conclusion unchanged.** Fresh search this run again surfaces two Wikipedia-sourced coordinate pairs ~1.5km apart (19.266°N/72.985°E vs. 19.253°N/72.978°E) and confirms no source gives coordinates for "Waghbil Naka" specifically (the actual bus-stop/landmark referenced in the existing Patlipada blurb) — only for the wider village area. Still not confident enough to add. Stays in the candidate table, unchanged.
- **Prabhadevi (nominal nearest: Santacruz store) — re-checked, conclusion unchanged.** This run's search (Rome2Rio, Santacruz Station ↔ Prabhadevi) returned a lower driving-distance figure (~8.5-9km) than the 10.1-10.2km computed in prior runs from the store's own lat/lng via haversine ×1.3 — but that lower figure measures from Santacruz railway station, not the store's actual coordinates, and Rome2Rio-style point-to-point estimates aren't on the same basis as every other locality on this site (straight-line × 1.3 from the store's own lat/lng). Not treated as new evidence either way; the site's own consistent methodology still puts it just over the ~10km ceiling. Stays in the candidate table, unchanged.
- **Uttan (Mira Road) — re-checked via WebSearch, conclusion unchanged.** This run's search again found only Uttan-to-Bhayandar figures (8km straight-line / 9-9.1km road), not a direct Uttan-to-Mira-Road-store distance — consistent with, not contradicting, the prior over-threshold conclusion once the Bhayandar-to-store leg is added. Stays in the candidate table, unchanged.
- **Ghatkopar West (nominal nearest: Santacruz store) — re-checked via WebSearch, conclusion unchanged.** Fresh sources this run again give a spread (7.8-9.6km foot/car figures from Rome2Rio, depending on exact endpoints used), still centred right at the ~10km ceiling once station-vs-neighbourhood ambiguity and the cross-city JVLR routing concern are factored in. Stays in the candidate table, unchanged.
- No other genuinely new, confidently-resolvable candidate surfaced this run. The extensive previously-examined-and-rejected list (Kasarvadavali, Aarey Colony, Airoli, Ulwe, Mira Road West, Koparkhairane, Ghansoli, Dahisar West, Balkum, Kanakia, Nerul East/West, Panvel, Taloja, Poonam Sagar, Hiranandani Estate, Bandra Kurla Complex, Teen Hath Naka/Khopat/Kopri, Golden Nest, Naigaon, Oshiwara cluster, Dindoshi, Powai, Rai, Kalina, Seawoods, "Upper Thane", Chincholi Bunder, Louiswadi) was not re-litigated — their reasoning stands.

Coverage remains close to saturation for genuinely distinct, in-range localities across all 5 stores. Precise geocoding (Nominatim) remains blocked at the session network-policy level, so the remaining open candidates stay stuck on the same ambiguity until either that block lifts or a human supplies tighter coordinates.

### Verification performed before closing out this run

- Full technical sweep via a fresh programmatic script covering sitemap-vs-pages, robots.txt bot coverage, JSON-LD parsing, internal links, image alt text, title/description length and uniqueness, canonical tags, and `og:site_name` presence — **0 issues found** across all 62 pages.
- Schema sweep (reviewRating fabrication pattern, AggregateRating correctness against source `reviews.rating`, FAQPage/BreadcrumbList/SportingGoodsStore completeness) — **0 issues found**.
- Entity-coverage, NAP, and `llms.txt` drift checks, all re-verified programmatically against current `data/stores.json` — **0 issues found**.
- Git state reconciled at run start — detached HEAD matching `origin/main` (2 commits behind), fast-forwarded `main` to match, nothing lost.
- WebFetch re-tested against 2 hosts, plus a direct `curl` test against Nominatim and a check of the sandbox's own `$HTTPS_PROXY/__agentproxy/status` endpoint — all confirm the block is a session-level network-policy denial (403 at the proxy gateway), not a transient DNS issue. 33rd consecutive run with this block.
- All four open candidates (Waghbil, Prabhadevi, Uttan, Ghatkopar West) re-checked via WebSearch — reasoning reconfirmed on all four, none resolved, none re-logged with duplicate reasoning.
- One new lead (Liberty Garden) investigated via WebSearch and correctly excluded (sits immediately beside the store's own address, not a distinct nearby locality) rather than force-fit or needlessly added to the candidate queue.

---

## Candidate localities awaiting human geocoding

| Locality | Assigned store | Why uncertain | First logged |
|---|---|---|---|
| Uttan | Mira Road | Only town-level coordinates available (not a pinpoint for the actual beach/lighthouse visitor area); road-distance estimate from those coordinates (~12.6km, and the lighthouse operator's own ~12km-from-Bhayandar-station figure) exceeds the ~10km threshold. Re-checked 2026-10-29 via WebSearch (only Uttan-to-Bhayandar figures found, 8-9.1km, consistent with not contradicting the over-threshold conclusion once the Bhayandar-to-store leg is added), conclusion unchanged. Needs a tighter geocode (Nominatim, once reachable) or a human call before adding. | 2026-10-22 |
| Ghatkopar West | Santacruz (nominal nearest) | Road-estimate to Santacruz sits right at the ~10km ceiling (7.8-10.3km depending on which of several sources' coordinates/endpoints are used), but the ×1.3 multiplier is unreliable for this cross-city, opposite-side-of-Mumbai hop (no direct road — via JVLR/SCLR across the hills), and Ghatkopar isn't a natural "near me" catchment for a Santacruz-area search. Needs a human call or a real-route (not straight-line) distance check before adding. Re-checked 2026-10-29, unchanged. | 2026-10-24 |
| Waghbil | Thane | Already named as a landmark in the existing Patlipada blurb, so a real place, but its own coordinates vary ~1.5km between sources and no source gives coordinates for "Waghbil Naka" specifically (only the wider village). Road-distance estimates range 6-11km depending on endpoint. Needs a tighter geocode or a human call before adding. Re-checked 2026-10-29, unchanged. | 2026-10-27 |
| Prabhadevi | Santacruz (nominal nearest) | Coordinates are consistent across sources; the site's own straight-line×1.3 methodology (from the store's actual lat/lng) puts it at 10.1-10.2km, just over the ~10km ceiling, and farther from the store than the existing Mahim entry (7.0km) which already covers the same southward corridor. A 2026-10-29 search found a lower station-to-station figure (~8.5-9km) via a travel aggregator, but that measures from Santacruz railway station, not the store's coordinates, so it isn't on a comparable basis and doesn't change the call. Needs a human call on whether to extend the ceiling for this specific locality, or leave as-is. | 2026-10-27 |

---

## Action Plan

| Finding | Category | Action Taken | Notes |
|---|---|---|---|
| Full technical/schema/AEO/E-E-A-T sweep across all 62 pages | All | Verified via a fresh programmatic sweep — **0 issues found** | Titles/descriptions, JSON-LD, links, alt text, canonicals, og:site_name, robots.txt, entity coverage, NAP, llms.txt, AggregateRating correctness, FAQ/BreadcrumbList/SportingGoodsStore coverage, reviewRating-fabrication pattern all clean. No code or data changes made this run. |
| Liberty Garden (Malad) locality lead | Local Reach | Investigated via WebSearch; found to sit immediately beside the Malad store's own address (Chincholi Bunder Road), not a separate nearby locality | Correctly excluded — not a gap, not logged as a candidate (same pattern as Chincholi Bunder, 2026-10-28) |
| Waghbil (Thane) locality lead | Local Reach | Re-investigated via WebSearch; coordinate/distance spread persists, no Waghbil-Naka-specific coordinates found | Left in candidate table, no duplicate re-log |
| Prabhadevi (Santacruz) locality lead | Local Reach | Re-investigated via WebSearch; new station-based figure found but not on a comparable basis to the site's own methodology | Left in candidate table, no duplicate re-log |
| Uttan (Mira Road) locality lead | Local Reach | Re-investigated via WebSearch; reconfirms prior over-threshold estimate | Left in candidate table, no duplicate re-log |
| Ghatkopar West (Santacruz) locality lead | Local Reach | Re-checked via WebSearch with fresh sources; estimate sits right at the ~10km ceiling either way | Left in candidate table, unchanged |
| WebFetch/Nominatim blocked, 33rd consecutive run | Technical GEO/SEO / Local Reach | Re-tested directly against 2 hosts via WebFetch, plus a direct `curl`+proxy-status check | Confirmed as a session-level network-policy denial (403 at the egress gateway), not a transient DNS fault — won't self-resolve; all research this run used WebSearch only |
| Repo was on detached HEAD at run start | Housekeeping | Checked out `main`, fast-forwarded 2 commits to match `origin/main` | No divergence, nothing lost |

**No commit this run** — no (A) fixes or (B) new localities; everything checked clean or was correctly excluded.

## Carried over from previous runs

| Finding | Category | Status | First flagged |
|---|---|---|---|
| WebFetch/Nominatim cannot reach any external host from this session (session network-policy block, confirmed via proxy status endpoint) | Technical GEO/SEO / Local Reach | Open, now 33 consecutive runs — worked around via WebSearch each time; live-site checks and precise Nominatim geocoding remain unavailable until the relevant hosts are added to the session's network allowlist | 2026-09-25 |
| Uttan (Mira Road) — candidate locality needing tighter geocode | Local Reach | Open, re-checked this run — see candidate table above | 2026-10-22 |
| Ghatkopar West — candidate locality needing a real-route distance check or human call | Local Reach | Open, re-checked this run — see candidate table above | 2026-10-24 |
| Waghbil (Thane) — candidate locality needing tighter geocode | Local Reach | Open, re-checked this run — see candidate table above | 2026-10-27 |
| Prabhadevi (Santacruz) — candidate locality, borderline over the ~10km ceiling | Local Reach | Open, re-checked this run — see candidate table above | 2026-10-27 |

*(Three items — "no press/backlinks" (first flagged 2026-09-15), "sitemap `lastmod` stamped to run date, not content-driven" (first flagged 2026-09-18), and "MadDog brand not named verbatim in homepage's brand-description copy" (first flagged 2026-09-16, not a real entity-coverage gap since MadDog is already quotable on all 5 store pages) — remain open >30 days and continue to be trimmed from this table per the 30-day rule. All three remain unresolved/unchanged; see Category 4 (reviews/backlinks), Category 1 (sitemap `lastmod`), and Category 3 (MadDog) history for current status. None needs re-litigating daily — the backlink item is the human's own active track via `audits/backlink-citation-plan.md`, the sitemap item needs a one-time human decision on approach, and the MadDog item is a non-issue under this audit's own entity-coverage criterion.)*
