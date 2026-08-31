# All Games Live Entry & Status List

## Scope

This specification covers the Live entry inside All Games and its child status list. It does not add a top-level Live tab and does not change Featured selection logic.

## Display

- Show the Live entry only when `selected_date` is the user's local Today and the deduplicated Live count is greater than 0.
- Place the entry directly below the date strip and before Top Competitions.
- Keep the entry to one 42 px row: live dot, `Live matches`, count, chevron.
- Do not show team names, scores, a recommendation rail, or `You may like` in All Games.
- Keep `All Games` active while the Live child list is open.

## Data

- Match: `match_id`, `status`, `status_period`, `clock`, `kickoff_time`, `score`, `updated_at`.
- Competition: `competition_id`, `competition_name`, `competition_logo_url`, `competition_sort_order`.
- Teams: `home_team`, `away_team`, `home_crest_url`, `away_crest_url`.
- User: `is_following`.
- Editorial: `is_featured`.

## Calculation

- Deduplication key: `match_id + status_period`; keep the newest `updated_at`.
- Group count: count unique `match_id` values in Finished, Live, and Upcoming.
- Entry count: use the Live group count.
- Group order: Finished, Live, Upcoming.
- Within a group, order by `competition_sort_order`, competition name, then kickoff time.
- Display `HT` at half time; otherwise use the provider's normalized match clock.

## Interaction

- Clicking the entry opens the Live child list without creating another top navigation tab.
- The child list opens with Live expanded and Finished/Upcoming collapsed.
- Status groups expand independently and may remain open together.
- Back or the All Games tab returns to the directory and restores its scroll position.
- `By time` changes to a cross-competition chronological list.
- Search accepts team and competition names; Filter supports status, competition, and following.
- Clicking a match opens Match Detail. Clicking the favorite control only changes following state.

## Boundary Handling

- Hide the entry on non-Today dates or when the Live count is 0.
- A legacy/direct Live URL on a non-Today date shows an empty state with a back action.
- Missing scores render as dashes; do not convert missing values to 0.
- Missing logos use fixed-size neutral placeholders without changing row height.
- Truncate long team and competition names to one line while retaining score and status.
- If push updates stop, poll every 15 seconds. Mark data delayed after 30 seconds without a successful update.
- On request failure, retain the latest successful list and expose retry state.

## Acceptance

- At 393 x 852 and 320 x 700, there is no horizontal overflow.
- Today shows one 42 px Live entry; Tue 28 shows none.
- The top navigation contains only All Games and Featured.
- Opening Live keeps All Games active and renders Finished, Live, Upcoming in that order.
- Initial expanded states are `false`, `true`, `false`.
- The Live row count equals the entry count and no duplicate `match_id + status_period` is rendered.
- All visible team and competition assets load, and browser console errors remain at 0.

