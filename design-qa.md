# Design QA

## Sources

- Product Demo: `index.html`
- Visual requirement document: `requirements.html`
- Implementation specification: `match_all_games_live_requirements_spec.md`
- Reference image supplied by the user: `/Users/wangfanhan/Downloads/IMG_1715.PNG`
- Two annotated A/B scheme reference images supplied in the 2026-09-02 browser comment.

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
- B's 0-Live state keeps a 58 px `Live now 0 / View all` entry, renders no horizontal track, opens the standalone `Live matches 0` empty page, and restores the 0 count after returning to All.
- The track starts at the first Live card. Finished is reachable at the far left and Upcoming at the far right; each opens the child list with its own status group expanded.
- Clicking a Live card opens the standalone `match.html` Match Centre page in the current tab; clicking `View all` opens the dedicated Live child list layer in the current tab.
- Dedicated Live page layer covers the status bar, top navigation, date strip, and previous content while keeping only the bottom tab bar visible. It keeps All active, renders status order Finished/Live/Upcoming, and initializes expanded states to false/true/false.
- The A experimental variant at `?view=all&date=27&variant=control` renders three top tabs, hides the inline Live preview, and switches only the main content in place without changing the URL. Its main area uses the supplied reference toolbar, Finished / Live / Upcoming, and two reference matches while the shared App chrome remains unchanged.
- At the native 393 x 852 canvas, Control A keeps identical pre/post-switch bounds for the status bar (y=0, h=48), top navigation (y=48, h=50), date strip (y=98, h=50), and bottom navigation (y=776, h=76). The reference toolbar begins at y=148 and Upcoming begins at y=466.
- The product prototype exposes a compact A/B variant switcher outside the phone app canvas; switching variants preserves the current view, date, and Live status query parameters.
- The requirement document exposes a top-level B test / A test switcher outside every phone canvas; changing it updates the document title, variant-specific rules, embedded prototype sources, and the shareable `variant=control` query parameter.
- The 2026-09-02 reference-copy update was verified at 1200 x 900 and 390 x 844: B shows `All / Recommended` plus the inline Live preview and standalone-page entry; A shows `All / Recommended / Live` and explicitly reuses the online Live list. Both states show the shared Explore / You may like / Recommended changes.
- Page modules render only the active variant's rules: B exposes no visible A copy and A exposes no visible B copy. Module 04 intentionally keeps the shared Control / A / B test definition.
- Module 01 is titled `All 页面`; it records the comparison with the original Explore page and, for B only, the Live horizontal preview area.
- The Recommended module removes the technical `取数` and `计算` blocks. Both A and B explicitly state that a match enters the list when it satisfies either eligibility condition: it involves a team followed by the user, or a team in the top three tiers of Eleven backend's `Popular Team Priority`. Matches satisfying both conditions are shown once.
- The corrected Recommended module was rechecked in both variants at 1280 px and 390 x 844: no `取数` or `计算` heading remains, the eligibility hint is visible, annotation targets remain selectable, and `scrollWidth === clientWidth`.
- The 2026-09-02 eligibility clarification was verified in A and B at 1280 x 720 and 390 x 844: Recommended includes user-followed teams or teams in Eleven backend's top three `Popular Team Priority` tiers, double-qualified matches are shown once, all generic popular-team wording is removed, prototype-label overflow is 0, duplicate IDs are 0, and blocked annotation targets are 0.
- Recommended date synchronization was verified by scrolling the list from the Today anchor to its end: the top date selection changed from `Today 27` to `Thu 30`. Clicking `Tue 28` selected that date and aligned its day section to the top of the list.
- Top Competitions and All Competitions remain visible in the All prototype but do not become standalone document modules.
- B's module 01 prototype exposes `多场 / 1 场 / 0 场`; its Live preview requirements contain placement, content, interaction, and five product-facing boundary cases. The 0-Live state retains the title entry and hides only match cards. A hides the state switcher and all B-only Live preview rules.
- Module 02 is `Recommended 页面` in both documents. `页面说明` contains only the variant difference; scroll/date synchronization, match and league opening, eligibility, and boundaries stay under `比赛列表`.
- Module 03 is `Live 页面` in both documents. B shows the page reached through All's `View all`; A shows the page reached through the Live tab. Both explicitly state that the page has no differences from the current online Live page.
- At 390 x 844, both document variants have `scrollWidth === clientWidth`; every visible rule retains a unique annotatable ID, accessible label, and keyboard focus target.
- Embedded prototypes hide their internal A/B switcher so the document-level switcher is the only experiment control visible in the requirement document. B loads the two-tab All / Recommended demo and standalone Live page; A loads the three-tab All / Recommended / Live demo.
- The requirements document and prototype override the Codex annotation layer's global selection reset with `:root body * { user-select: text !important; }`. Stable annotation targets carry `data-annotatable`, unique IDs, accessible labels, and focusability; dynamic prototype rows are marked after each render.
- The 2026-09-02 annotation repair also marks document controls, headings, body copy, formulas, inline emphasis, and prototype content with `data-openai-annotatable`. All four visible prototypes expose independently marked content; the current outer-document checks found no blocked selection, duplicate IDs, or horizontal overflow.
- Interactive prototype iframes now mount only after the Codex comment layer has initialized. On the exact local URL `http://localhost:4181/requirements.html?v=page-modules-1`, the comment root mounted successfully, text hover produced the blue target outline and comment cursor, and the A/B switcher label was recognized as an independent target.
- After leaving comment selection mode, A/B switching was rechecked: both A and B load four visible prototypes including Live; the comment root remains mounted in both states.
- The requirement document records the shared changes from the online baseline: Explore becomes All, All no longer contains You may like, and Recommended becomes an independent kickoff-time-ordered tab.
- A is documented as `All / Recommended / Live` with the current online Live page reused inside the Live tab. B is documented as `All / Recommended` with an inline Live preview whose `View all` opens the same unchanged Live page.
- Live child list renders 7 Live matches across 5 competition groups; status sections expand independently.
- Tue 28 renders 0 Live entries.
- Requirement document at 1440 x 900 and 1200 x 900 uses two columns with a maximum 1180 px document width.
- Requirement document at 390 x 844 uses one column, a 355 px prototype, and no rule-block overflow.
- The requirement document displays the Live page below Recommended in both variants: B shows the dedicated page reached from `View all`, while A shows the existing Live-tab page.
- The standalone `match.html` page remains shared by both variants and is outside the A/B requirement modules; the list no longer contains or opens a bottom detail sheet.
- Requirement document module titles and navigation labels are Chinese, including the `04 A/B 测试` module.
- Requirement document A/B switcher was verified at desktop and 390 x 844: both tabs are operable, the selected document state is reflected in the title and module rules, and body scroll width equals viewport width.
- Requirement document A/B switcher was verified after a live toggle: A and B expose different module summaries, prototype labels, embedded URLs, and navigation chrome while preserving the same outer document layout.
- League headers in Recommended, Top Competitions rows in All, and expanded league child rows expose independent links to `league.html`; the collapse control remains separate from the navigation target. The Recommended UEFA Champions League arrow was verified to set `competition collapsed` without navigation, while its crest/name opened the correct League Profile and returned to the list.
- Local league profile navigation was verified for Premier League from Recommended and English Premier League from All; both open a standalone profile page with the correct crest, match summary, date, and context-aware back link.
- Recommended, B Live preview, standalone Live rows, A reference Live rows, and redesigned All cards navigate directly to the standalone `match.html` page with the selected match and source context; `#sheet` is absent from the product DOM.
- The final A/B module contains only `测试方法` and `需要验证的数据`; both document tabs show the same copy.
- New users and existing users are randomized separately 1:1:1 across the current online Control, standalone-Live-tab A, and inline-Live-preview B. Only users on the current latest App version participate.
- Recommended shows the inline `No matches in this filter` example directly under its empty-state boundary. Its interaction rules distinguish league-title navigation from the right-arrow expand/collapse action. At 390 x 844, the empty-state example is 96 px high, both variants have zero horizontal overflow and duplicate IDs, all annotation targets remain selectable, and `#codex-browser-sidebar-comments-root` is mounted.
- Validation now measures whether Recommended and the Match module become more popular, rather than whether users enter Live. It includes explicit formulas for Recommended and Match daily UV, daily PV, visits per user-day, same-day revisit rate, Recommended penetration, Match Detail conversion, and D1 / D7 Match retention.
- The revised validation block was checked in both A and B documents. No Live-entry metric remains; at 390 x 844 the longer UV/PV formulas wrap without block or page overflow, duplicate IDs remain 0, and the Codex comment root mounts successfully.
- Requirement modules map one-to-one to product pages. Both documents use module 01 `All 页面`, module 02 `Recommended 页面`, module 03 `Live 页面`, and module 04 for the shared A/B test definition.
- The B All module separates `页面调整` and `Live 横滑预览` with prominent in-module headings. The A All module shows only `页面调整`. Recommended separates `页面说明` and `比赛列表`; `页面说明` contains only the A/B difference and neither variant shows a `展示位置` block. The shared Live module separates the variant-specific `页面入口` from the unchanged `页面内容`.
- The Explore-to-All rename, removal of `You may like`, and preservation of Top Competitions / All Competitions are shown as one shared All-page rule in both A and B. Only the top-tab composition remains variant-specific.
- Product scripts: 0 errors and 0 warnings when checked independently of the injected annotation layer.
- Direct product check includes the reference app mark, two competition marks, and four team crests added for Control A; all visible reference assets load without broken images.
- Static HTTP check: 65 of 65 files returned 200.
- Inline product script compiled successfully as one script block.
- The in-app browser still records a source-less `MutationObserver` error while scanning nested prototype documents. It does not prevent the repaired comment root, selectable targets, or page interactions from working.

## Public Deployment

- The latest local requirements revision is not deployed: local `main` is 30 commits ahead of public `main` (`6824be4`). HTTPS push has no GitHub credential and SSH has no accepted key, so the public requirements page still contains the previous requirement copy.
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
- Enter Recommended from another tab, verify its Live / most-recent-Finished anchor, scroll across date groups, and confirm the selected top date follows the visible group.
- On the local requirements URL, audit the outer document and embedded prototype DOM independently: `html`, `body`, and descendants report selectable text, blocked descendants count is zero, target IDs are unique, and the A/B buttons remain clickable.
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
