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
- All contains 0 recommendation-rail nodes. The Live preview renders 7 neutral horizontal cards with competition, clock, crests, teams, and score; no card receives the Recommended emphasis style.
- The track starts at the first Live card. Finished is reachable at the far left and Upcoming at the far right; each opens the child list with its own status group expanded.
- Clicking a Live card opens the standalone `match.html` Match Centre page in the current tab; clicking `View all` opens the dedicated Live child list layer in the current tab.
- Dedicated Live page layer covers the status bar, top navigation, date strip, and previous content while keeping only the bottom tab bar visible. It keeps All active, renders status order Finished/Live/Upcoming, and initializes expanded states to false/true/false.
- Control variant at `?view=all&date=27&variant=control` renders three top tabs, hides the inline Live preview, and switches only the main content in place without changing the URL. Its main area uses the supplied reference toolbar, Finished / Live / Upcoming, and two reference matches while the shared App chrome remains unchanged.
- At the native 393 x 852 canvas, Control A keeps identical pre/post-switch bounds for the status bar (y=0, h=48), top navigation (y=48, h=50), date strip (y=98, h=50), and bottom navigation (y=776, h=76). The reference toolbar begins at y=148 and Upcoming begins at y=466.
- The product prototype exposes a compact A/B variant switcher outside the phone app canvas; switching variants preserves the current view, date, and Live status query parameters.
- The requirement document exposes a top-level B test / A test switcher; changing it updates the document title, context summary, Live prototype source, A/B module prototype source, and the shareable `variant=control` query parameter.
- Live child list renders 7 Live matches across 5 competition groups; status sections expand independently.
- Tue 28 renders 0 Live entries.
- Requirement document at 1440 x 900 and 1200 x 900 uses two columns with a maximum 1180 px document width.
- Requirement document at 390 x 844 uses one column, a 355 px prototype, and no rule-block overflow.
- The requirement document's Live prototype opens the dedicated Live page from `View all` and returns to the horizontal preview; the A control link exposes the three-tab variant.
- The requirement document's detail prototype opens the standalone `match.html` page; the list no longer contains or opens a bottom detail sheet.
- Requirement document module titles and navigation labels are Chinese, including the new `07 A/B 测试` module.
- Requirement document A/B switcher was verified at desktop and 390 x 844: both tabs are operable, the selected document state is reflected in the title and context, and body scroll width equals viewport width.
- League headers in Recommended, Top Competitions rows in All, and expanded league child rows expose independent links to `league.html`; the collapse control remains separate from the navigation target.
- Local league profile navigation was verified for Premier League from Recommended and English Premier League from All; both open a standalone profile page with the correct crest, match summary, date, and context-aware back link.
- Recommended, B Live preview, standalone Live rows, A reference Live rows, and redesigned All cards navigate directly to the standalone `match.html` page with the selected match and source context; `#sheet` is absent from the product DOM.
- The A/B module specifies the three-tab control A, inline-preview variant B, 50/50 sticky assignment, event schema, primary/secondary metrics, guardrails, runtime, and decision thresholds.
- Product console: 0 errors and 0 warnings.
- Direct product check includes the reference app mark, two competition marks, and four team crests added for Control A; all visible reference assets load without broken images.
- Static HTTP check: 65 of 65 files returned 200.
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
- Open the control variant and enter Live from the third top tab; confirm the URL and every shared App region remain unchanged while only the main content switches.
- Switch repeatedly between All, Recommended, and control Live; confirm the status bar, topbar, date strip, and bottom navigation keep identical bounding boxes and the search/profile controls do not appear or disappear unexpectedly.
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
