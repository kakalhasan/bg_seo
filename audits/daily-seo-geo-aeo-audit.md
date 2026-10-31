# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-10-31
**Status:** 🟢 Clean sweep, no changes needed. Full programmatic re-sweep of all 62 pages (technical, schema, entity-coverage, NAP, llms.txt, AggregateRating correctness) found 0 issues. No new locality pages added this run — the four already-open candidates (Uttan, Ghatkopar West, Waghbil, Prabhadevi) were re-checked via WebSearch; none resolved, reasoning unchanged. Site stays at **62 pages** (1 homepage + 5 store pages + 56 locality pages).

**Housekeeping:** Repo was clean and already on `main`, up to date with `origin/main` at run start (no detached HEAD, no divergence). Nothing to reconcile.

**Network access note — WebFetch/Nominatim still blocked at the session network-policy level, 34th consecutive run:** Re-tested directly at run start against `https://helmetstorenearme.in/` and `https://nominatim.openstreetmap.org/search` via WebFetch — both failed with `getaddrinfo ENOTFOUND <host>`, with the tool's own error message stating the host is outside the session's allowed network domains. Cross-checked via the sandbox's `$HTTPS_PROXY/__agentproxy/status` endpoint: `recentRelayFailures` shows the same `connect_rejected`/403 pattern against many other non-allowlisted hosts (e.g. `mcp.box.com`, `mcp.asana.com`, `mcp.notion.com`). This is a session network-allowlist restriction, not a transient DNS failure. `WebSearch` continues to work fully and was used for all research this run. No live-site fetch and no direct Nominatim JSON geocoding were possible.

---

## 1. Technical GEO/SEO

| Check | Result |
|---|---|
| Sitemap vs actual pages | ✅ 62/62 match exactly, 0 missing, 0 extra |
| robots.txt bot coverage | ✅ `*`, GPTBot, ChatGPT-User, PerplexityBot, ClaudeBot, Google-Extended all `Allow: /`, sitemap referenced |
| JSON-LD parses | ✅ 0 errors across all 62 pages |
| Broken internal links | ✅ 0 found (fresh link-checker sweep) |
| Image alt text | ✅ All 84 `<img>` tags have non-empty, descriptive alt text |
| Title tag length | ✅ All 62 ≤60 chars (post-entity-decode), all unique |
| Meta description length/uniqueness | ✅ All 62 unique, all ≤140 chars (post-entity-decode) |
| Canonical tags | ✅ Present and correct on every page |
| Open Graph `og:site_name` | ✅ Present on all 62 pages |
| Live-site check (helmetstorenearme.in) | ⚠️ Not performed — WebFetch failed, session-level network block (see network note above) |

**Known open issue (not re-tabled below, see Carried-over note):** `generate.py` stamps every page's sitemap `lastmod` to the run date on every invocation rather than tracking real per-page content changes (`generate.py` — `TODAY = datetime.date.today().isoformat()`). No regeneration ran this run (no A/B changes), so `lastmod` correctly stayed at 2026-10-28 (last real content change) rather than bumping to today. Still needs a human call on approach (hash-based or data-driven lastmod) for the days when a regeneration *does* run with no real content change. First flagged 2026-09-18.

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

**No new locality pages added this run.** All four previously-logged candidates (Waghbil, Prabhadevi, Uttan, Ghatkopar West) were re-checked via WebSearch; none resolved, reasoning unchanged. No genuinely new, confidently-resolvable candidate surfaced.

- **Waghbil (Thane) — re-checked via WebSearch, conclusion unchanged.** Fresh search again surfaces the same two disagreeing coordinate pairs for the wider Waghbil area (Wikipedia: ~19.266°N/72.985°E; a wiki-mirror: ~19.253°N/72.978°E, ~1.5km apart) and confirms no source gives coordinates for "Waghbil Naka" specifically — only for the broader village. Still not confident enough to add. Stays in the candidate table, unchanged.
- **Prabhadevi (nominal nearest: Santacruz store) — re-checked, conclusion unchanged.** This run's search again returned Rome2Rio aggregator figures (~8.5-9km) measured from Santacruz railway station, not the store's actual coordinates — not on the same basis as the site's own straight-line×1.3-from-store-lat/lng methodology, which still puts Prabhadevi at 10.1-10.2km, just over the ~10km ceiling. Not treated as new evidence; stays in the candidate table, unchanged.
- **Uttan (Mira Road) — re-checked via WebSearch, conclusion unchanged.** This run's search again found no direct Uttan-to-Mira-Road-store figure; only a vague "5-10km from Mira Road station" general estimate with no reliable source, consistent with (not improving on) the prior over-threshold conclusion. Stays in the candidate table, unchanged.
- **Ghatkopar West (nominal nearest: Santacruz store) — re-checked via WebSearch, conclusion unchanged.** Fresh sources this run give a wider spread than before (9.6-12km depending on exact Ghatkopar/Ghatkopar West/Ghatkopar East endpoint used), still straddling the ~10km ceiling with the same cross-city routing ambiguity. Stays in the candidate table, unchanged.
- No other genuinely new, confidently-resolvable candidate surfaced this run. The extensive previously-examined-and-rejected list (Kasarvadavali, Aarey Colony, Airoli, Ulwe, Mira Road West, Koparkhairane, Ghansoli, Dahisar West, Balkum, Kanakia, Nerul East/West, Panvel, Taloja, Poonam Sagar, Hiranandani Estate, Bandra Kurla Complex, Teen Hath Naka/Khopat/Kopri, Golden Nest, Naigaon, Oshiwara cluster, Dindoshi, Powai, Rai, Kalina, Seawoods, "Upper Thane", Chincholi Bunder, Louiswadi, Liberty Garden) was not re-litigated — their reasoning stands.

Coverage remains close to saturation for genuinely distinct, in-range localities across all 5 stores. Precise geocoding (Nominatim) remains blocked at the session network-policy level, so the remaining open candidates stay stuck on the same ambiguity until either that block lifts or a human supplies tighter coordinates.

### Verification performed before closing out this run

- Full technical sweep via a fresh programmatic script covering sitemap-vs-pages, robots.txt bot coverage, JSON-LD parsing, internal links, image alt text, title/description length and uniqueness, canonical tags, and `og:site_name` presence — **0 issues found** across all 62 pages.
- Schema sweep (reviewRating fabrication pattern, AggregateRating correctness against source `reviews.rating`, FAQPage/BreadcrumbList/SportingGoodsStore completeness) — **0 issues found**.
- Entity-coverage, NAP, and `llms.txt` drift checks, all re-verified programmatically against current `data/stores.json` — **0 issues found**.
- Git state checked at run start — already clean, on `main`, matching `origin/main`, nothing to reconcile.
- WebFetch re-tested against 2 hosts (live site + Nominatim), plus the sandbox's own `$HTTPS_PROXY/__agentproxy/status` endpoint — confirms the block is a session-level network-policy denial (403 at the proxy gateway), not a transient DNS issue. 34th consecutive run with this block.
- All four open candidates (Waghbil, Prabhadevi, Uttan, Ghatkopar West) re-checked via WebSearch — reasoning reconfirmed on all four, none resolved, none re-logged with duplicate reasoning.

---

## Candidate localities awaiting human geocoding

| Locality | Assigned store | Why uncertain | First logged |
|---|---|---|---|
| Uttan | Mira Road | Only town-level coordinates available (not a pinpoint for the actual beach/lighthouse visitor area); road-distance estimate from those coordinates (~12.6km, and the lighthouse operator's own ~12km-from-Bhayandar-station figure) exceeds the ~10km threshold. Re-checked 2026-10-31 via WebSearch (no direct Uttan-to-store figure found, only a vague unsourced "5-10km from Mira Road station" estimate), conclusion unchanged. Needs a tighter geocode (Nominatim, once reachable) or a human call before adding. | 2026-10-22 |
| Ghatkopar West | Santacruz (nominal nearest) | Road-estimate to Santacruz sits right at the ~10km ceiling (7.8-12km depending on which of several sources' coordinates/endpoints are used), but the ×1.3 multiplier is unreliable for this cross-city, opposite-side-of-Mumbai hop (no direct road — via JVLR/SCLR across the hills), and Ghatkopar isn't a natural "near me" catchment for a Santacruz-area search. Needs a human call or a real-route (not straight-line) distance check before adding. Re-checked 2026-10-31, unchanged. | 2026-10-24 |
| Waghbil | Thane | Already named as a landmark in the existing Patlipada blurb, so a real place, but its own coordinates vary ~1.5km between sources and no source gives coordinates for "Waghbil Naka" specifically (only the wider village). Road-distance estimates range 6-11km depending on endpoint. Needs a tighter geocode or a human call before adding. Re-checked 2026-10-31, unchanged. | 2026-10-27 |
| Prabhadevi | Santacruz (nominal nearest) | Coordinates are consistent across sources; the site's own straight-line×1.3 methodology (from the store's actual lat/lng) puts it at 10.1-10.2km, just over the ~10km ceiling, and farther from the store than the existing Mahim entry (7.0km) which already covers the same southward corridor. Station-based aggregator figures (~8.5-9km) found again this run aren't on a comparable basis and don't change the call. Needs a human call on whether to extend the ceiling for this specific locality, or leave as-is. | 2026-10-27 |

---

## Action Plan

| Finding | Category | Action Taken | Notes |
|---|---|---|---|
| Full technical/schema/AEO/E-E-A-T sweep across all 62 pages | All | Verified via a fresh programmatic sweep — **0 issues found** | Titles/descriptions, JSON-LD, links, alt text, canonicals, og:site_name, robots.txt, entity coverage, NAP, llms.txt, AggregateRating correctness, FAQ/BreadcrumbList/SportingGoodsStore coverage, reviewRating-fabrication pattern all clean. No code or data changes made this run. |
| Waghbil (Thane) locality lead | Local Reach | Re-investigated via WebSearch; coordinate/distance spread persists, no Waghbil-Naka-specific coordinates found | Left in candidate table, no duplicate re-log |
| Prabhadevi (Santacruz) locality lead | Local Reach | Re-investigated via WebSearch; station-based figure again not on a comparable basis to the site's own methodology | Left in candidate table, no duplicate re-log |
| Uttan (Mira Road) locality lead | Local Reach | Re-investigated via WebSearch; no new direct figure found, reconfirms prior over-threshold estimate | Left in candidate table, no duplicate re-log |
| Ghatkopar West (Santacruz) locality lead | Local Reach | Re-checked via WebSearch with fresh sources; estimate spread widened slightly (9.6-12km) but still straddles the ~10km ceiling | Left in candidate table, unchanged |
| WebFetch/Nominatim blocked, 34th consecutive run | Technical GEO/SEO / Local Reach | Re-tested directly against 2 hosts via WebFetch, plus a proxy-status check | Confirmed as a session-level network-policy denial (403 at the egress gateway), not a transient DNS fault — won't self-resolve; all research this run used WebSearch only |
| Git state at run start | Housekeeping | Checked — already clean and up to date with `origin/main` | No action needed |

**No commit this run** — no (A) fixes or (B) new localities; everything checked clean or stayed in the candidate queue unchanged.

## Carried over from previous runs

| Finding | Category | Status | First flagged |
|---|---|---|---|
| WebFetch/Nominatim cannot reach any external host from this session (session network-policy block, confirmed via proxy status endpoint) | Technical GEO/SEO / Local Reach | Open, now 34 consecutive runs — worked around via WebSearch each time; live-site checks and precise Nominatim geocoding remain unavailable until the relevant hosts are added to the session's network allowlist | 2026-09-25 |
| Uttan (Mira Road) — candidate locality needing tighter geocode | Local Reach | Open, re-checked this run — see candidate table above | 2026-10-22 |
| Ghatkopar West — candidate locality needing a real-route distance check or human call | Local Reach | Open, re-checked this run — see candidate table above | 2026-10-24 |
| Waghbil (Thane) — candidate locality needing tighter geocode | Local Reach | Open, re-checked this run — see candidate table above | 2026-10-27 |
| Prabhadevi (Santacruz) — candidate locality, borderline over the ~10km ceiling | Local Reach | Open, re-checked this run — see candidate table above | 2026-10-27 |

*(Three items — "no press/backlinks" (first flagged 2026-09-15), "sitemap `lastmod` stamped to run date, not content-driven" (first flagged 2026-09-18), and "MadDog brand not named verbatim in homepage's brand-description copy" (first flagged 2026-09-16, not a real entity-coverage gap since MadDog is already quotable on all 5 store pages) — remain open >30 days and continue to be trimmed from this table per the 30-day rule. All three remain unresolved/unchanged; see Category 4 (reviews/backlinks), Category 1 (sitemap `lastmod`), and Category 3 (MadDog) history for current status. None needs re-litigating daily — the backlink item is the human's own active track via `audits/backlink-citation-plan.md`, the sitemap item needs a one-time human decision on approach, and the MadDog item is a non-issue under this audit's own entity-coverage criterion.)*
