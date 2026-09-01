# Matches Live Entry & Status List

## Scope

This specification covers the Live entry inside All and its dedicated status list page. The B variant does not add a top-level Live tab and opens an overlay-style Live page from View all. The A control variant adds a top-level Live tab that switches only the main content in place without changing the URL or shared App chrome. Neither variant changes Recommended selection logic.

## Display

- Show the Live entry only when `selected_date` is the user's local Today and the deduplicated Live count is greater than 0.
- Place the entry directly below the date strip and before Top Competitions.
- Use a two-part module: a `Live now` title row with count and `View all`, followed by a horizontally scrollable Live match preview.
- Each preview card shows a fixed-size real competition crest to the left of the competition name, normalized match clock, both team crests, both team names, and the current score.
- Reveal part of the next card in the first viewport to make horizontal scrolling discoverable.
- Place a `Finished` entry at the far left and an `Upcoming` entry at the far right. Start at the first Live card, with both status entries reachable by horizontal scrolling.
- Use the same neutral card style for every Live preview; do not add an `is_featured` background or emphasis border in this rail.
- Do not show a recommendation rail or `You may like` in Matches.
- B opens a dedicated Live page layer and keeps `All` active in the shared navigation beneath that layer.
- A switches only the area below the date strip to the reference Live content. The device status bar, `All / Recommended / Live`, date strip, and standard bottom navigation keep the same dimensions and positions as All.

## Data

- Match: `match_id`, `status`, `status_period`, `clock`, `kickoff_time`, `score`, `updated_at`.
- Competition: `competition_id`, `competition_name`, `competition_logo_url`, `competition_sort_order`.
- Teams: `home_team`, `away_team`, `home_crest_url`, `away_crest_url`.
- User: `is_following`.
- Editorial: `is_featured`.
- Preview order: `live_preview_sort_order`.

## Calculation

- Deduplication key: `match_id + status_period`; keep the newest `updated_at`.
- Group count: count unique `match_id` values in Finished, Live, and Upcoming.
- Title count and preview-card count: use the Live group count.
- Order preview cards by `live_preview_sort_order`; fall back to competition order and kickoff time.
- Track order is `Finished entry`, Live cards, `Upcoming entry`; initial scroll offset equals the Finished entry width plus one gap.
- Group order: Finished, Live, Upcoming.
- Within a group, order by `competition_sort_order`, competition name, then kickoff time.
- Display `HT` at half time; otherwise use the provider's normalized match clock.

## Interaction

- Swiping the preview browses Live cards without leaving Matches.
- Clicking a preview card opens the standalone Match Detail page in the current tab.
- Clicking `View all` opens a dedicated Live page layer in the current tab. It covers the status bar, top navigation, date strip, and previous match content; only the persistent bottom tab bar remains visible.
- Clicking a status entry navigates to the dedicated Live list page with the selected Finished or Upcoming group expanded and the other groups collapsed.
- The child list opens with Live expanded and Finished/Upcoming collapsed.
- Status groups expand independently and may remain open together.
- Back or the bottom Matches tab closes the Live page layer, returns to the directory, and restores the selected-date context.
- `By time` changes to a cross-competition chronological list.
- Search accepts team and competition names; Filter supports status, competition, and following.
- Clicking a match opens the standalone Match Detail page in the current tab. Clicking the favorite control only changes following state.
- The standalone Match Detail page owns the match URL and content; the Matches list never opens a bottom sheet or scrim for match details.
- In A, clicking the top-level Live tab keeps the URL unchanged. Clicking All or Recommended switches only the main content while all shared App regions remain mounted and fixed.

## Boundary Handling

- Hide the complete preview module on non-Today dates or when the Live count is 0.
- A legacy/direct Live URL on a non-Today date shows an empty state with a back action.
- Missing scores render as dashes; do not convert missing values to 0.
- Missing logos use fixed-size neutral placeholders without changing row height.
- Truncate long team and competition names to one line while retaining score and status.
- If push updates stop, poll every 15 seconds. Mark data delayed after 30 seconds without a successful update.
- On request failure, retain the latest successful list and expose retry state.

## Acceptance

- At 393 x 852 and 320 x 700, there is no horizontal overflow.
- Today shows the Live title and horizontal preview; Tue 28 shows neither.
- At least one preview card is fully visible and the following card remains partially visible at 393 px and 320 px widths.
- Scrolling fully left exposes Finished; scrolling fully right exposes Upcoming.
- The prototype includes a compact A/B variant switcher outside the phone app canvas. Variant B top navigation contains only All and Recommended; variant A adds Live as a third tab.
- B opening Live renders Finished, Live, Upcoming in that order on a dedicated full-screen page layer covering every App region except the persistent bottom tab bar.
- Any match row in Recommended, All, B Live preview, or either Live list navigates to `match.html` with match, status, score, crest, date, and source context in the URL.
- A opening Live renders the supplied reference only inside the main content area: toolbar, Finished / Live / Upcoming, and competition-grouped rows. The shared status bar, three match tabs, date strip, and bottom navigation are identical before and after the switch; the URL remains unchanged.
- Initial expanded states are `false`, `true`, `false`.
- The Live row count equals the entry count and no duplicate `match_id + status_period` is rendered.
- All visible team and competition assets load, and browser console errors remain at 0.

## A/B Test

- Objective: validate whether the horizontal Live preview improves Live discovery and match-detail entry without harming overall match browsing.
- Control A: three top-level tabs, All, Recommended, and Live; Live opens the dedicated Live list directly, and All has no inline Live preview.
- Variant B: `Live now` title row with `View all`, horizontal Live cards, and Finished/Upcoming entries at the two ends of the rail. All cards use the same neutral style.
- Control demo URL: `?view=all&date=27&variant=control`. Clicking the top-level Live tab switches only the main content in place without changing the URL.
- All, Recommended, and control Live share one fixed status-bar, top-navigation, date-strip, and bottom-navigation geometry. Active state must not alter any shared component's bounding box.
- Eligibility: Matches + Today users with a successfully rendered Live module and at least one Live match. Exclude bots, internal accounts, request failures, and duplicate devices.
- Assignment: 50/50 random assignment by `user_id` or stable device ID, sticky for the experiment period; keep `experiment_id`, `variant`, and `assignment_time` on every event.
- Primary metric: unique exposed users who click any Live entry, Live card, or open Match Detail divided by unique exposed users.
- Secondary metrics: card click-through, View all click-through, Finished/Upcoming usage, P50 time to first Match Detail, and Match Detail opens per session.
- Guardrails: overall Match Detail opens, page exit rate, first-screen load time, and client error rate. Pause if any guardrail worsens by more than 3% or errors rise by more than 0.2 percentage points.
- Runtime: collect a 7-day baseline for sample sizing, then run at least 14 days including two complete weekends. Recommend B only when the primary metric improves by at least 5% relative and its 95% confidence interval excludes 0; otherwise extend one week or mark the result inconclusive.
