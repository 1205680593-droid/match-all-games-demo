# Design QA

## Sources

- Product Demo: `index.html`
- Visual requirement document: `requirements.html`
- Implementation specification: `match_all_games_live_requirements_spec.md`
- Reference image supplied by the user: `/Users/wangfanhan/Downloads/IMG_1715.PNG`

## Review Scope

- Matches navigation and Today date state.
- Top-positioned Live title and horizontal match preview.
- Live child list with Finished, Live, Upcoming groups.
- Top competition and All Competitions continuity after removing the recommendation rail.
- Requirement document prototype and Live specification blocks.

## Required Viewports

- Product: 393 x 852 and 320 x 700.
- Requirement document: 1440 x 900, 1200 x 900, and 390 x 844.

## Verified Results

- Product at 393 x 852: Live preview begins at the date strip bottom, remains 150 px high, and has 0 px horizontal overflow. The first 196 px card is fully visible and 175 px of the next card is exposed.
- Product at 320 x 700: Live preview remains 150 px high with 0 px horizontal overflow. The first card is fully visible and 101 px of the next card is exposed.
- Matches contains 0 recommendation-rail nodes. The Live preview renders 7 neutral horizontal cards with competition, clock, crests, teams, and score; no card receives the Top Matches emphasis style.
- The track starts at the first Live card. Finished is reachable at the far left and Upcoming at the far right; each opens the child list with its own status group expanded.
- Clicking a Live card opens Match Detail; clicking `View all` opens the existing Live child list.
- Dedicated Live page keeps Matches active, renders status order Finished/Live/Upcoming, and initializes expanded states to false/true/false.
- Live child list renders 7 Live matches across 5 competition groups; status sections expand independently.
- Tue 28 renders 0 Live entries.
- Requirement document at 1440 x 900 and 1200 x 900 uses two columns with a maximum 1180 px document width.
- Requirement document at 390 x 844 uses one column, a 355 px prototype, and no rule-block overflow.
- The requirement document's Live prototype opens the Live child list from `View all` and returns to the horizontal preview.
- Requirement document module titles and navigation labels are Chinese, including the new `07 A/B 测试` module.
- The A/B module specifies control A, variant B, 50/50 sticky assignment, event schema, primary/secondary metrics, guardrails, runtime, and decision thresholds.
- Product console: 0 errors and 0 warnings.
- Direct product check loaded all 25 referenced images with 0 broken assets.
- Static HTTP check: 58 of 58 files returned 200.
- Inline product script compiled successfully as one script block.
- The in-app browser annotation layer emitted two source-less `MutationObserver` errors when reloading the multi-iframe requirement page. The project contains no `MutationObserver` call; direct product-page console checks remained clean.

## Public Deployment

- Repository: `https://github.com/1205680593-droid/match-all-games-demo`
- Demo: `https://1205680593-droid.github.io/match-all-games-demo/?view=all&date=27`
- Visual requirements: `https://1205680593-droid.github.io/match-all-games-demo/requirements.html#live`
- Hosting: GitHub Pages from `main` and `/(root)`, with HTTPS enforced.
- Pages workflow `pages-build-deployment #1` completed successfully in 46 seconds.
- Public Demo and requirements URLs returned HTTP 200.
- Public Demo rendered the Matches entry and dedicated Live page with 7 matches, 5 competition groups, 0 broken visible images after load, and 0 console errors/warnings.

## Required Interactions

- Open Live from Matches.
- Swipe the Live preview and open a match card.
- Expand and collapse each status group.
- Return from Live to Matches.
- Switch from Today to Tue 28 and confirm the Live entry is absent.
- Open the requirements document and operate the embedded Live prototype.

## Evidence Boundaries

- Match, score, clock, following, and importance values are static Demo data.
- Push updates, 15-second fallback polling, delayed-data state, search, filter, and backend retry are specified production behavior; toolbar controls currently demonstrate entry feedback only.
- Real crest and competition-logo files are local static assets, not a production CDN integration.
- Permanent public hosting requires an authenticated deployment account; localhost is not a shareable production URL.
