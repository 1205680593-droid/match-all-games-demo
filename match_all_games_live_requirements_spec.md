# Matches Navigation & Live Experiments

## 01 All Page

### Shared Page Changes

- Rename `Explore` to `All` and remove only `You may like`; Top Competitions and All Competitions remain unchanged.
- Keep All as the default entry. Status bar, date strip, and bottom navigation keep the original dimensions when tabs change.

### Experiment B: Live Preview Area

- Top navigation contains `All / Recommended`.
- On local Today, always show `Live now / count / View all` below the date strip and above Top Competitions. Show the horizontal match preview when ongoing matches exist.
- Each card shows competition crest, clock, team crests, team names, and score. Track order is `Finished entry / Live cards / Upcoming entry`, initially aligned to the first Live card.
- A card opens Match Detail. `View all`, Finished, and Upcoming open the standalone Live page in the corresponding state. Back restores All, the selected date, and prior scroll position.
- With no ongoing match, keep `Live now 0 / View all` and hide only the horizontal cards. With exactly one ongoing match, show one wider card without duplication.
- When the final ongoing match finishes, remove that card from the preview, update the count to 0, and keep the Live entry. Loading uses fixed-height skeletons; load failure hides only the Live area. Missing scores use dashes and missing crests use fixed-size placeholders.

### Experiment A

- Top navigation contains `All / Recommended / Live`; All contains no horizontal Live preview.

## 02 Recommended Page

### Page Notes

- Recommended is an independent top tab: to the right of All in B, and between All and Live in A.

### Match List

- Include a match when either team is followed by the user, or at least one participating team belongs to one of the top three priority tiers in Eleven backend's `Popular Team Priority`. Show a double-qualified match only once.
- Scrolling into another date group updates the selected top date. Clicking a date scrolls the list to that group.
- If the selected date has no eligible match, show the online `No matches in this filter` empty state. Matches without a kickoff time appear at the end.
- Match rows open `match.html` directly. Clicking a league crest or name opens `league.html`; the right arrow only expands or collapses that league's matches.

## 03 Live Page

### Entry

- In A, open Live from the third top tab. In B, open Live through `View all` in the All-page Live entry.

### Page Content

- The Live page reached from either A or B has no visual, content, or interaction changes from the current online Live page. Reuse the online toolbar, Finished / Live / Upcoming groups, match rows, expand behavior, search, filter, following, and Match Detail navigation.

## 04 A/B Test

### Test Method

- Randomly assign new users and existing users separately 1:1:1 to Control (current online experience), A (Live tab), or B (inline Live preview).
- Run the experiment only on the current latest App version. Users still on older versions do not participate.

### Data to Validate

- Recommended daily UV = distinct users who enter Recommended at least once that day.
- Recommended daily PV = total Recommended entries that day; repeated entries by the same user on the same day continue to count.
- Recommended penetration rate = Recommended daily UV / Match module daily UV.
- Recommended visits per user-day = Recommended daily PV / Recommended daily UV.
- Recommended same-day revisit rate = distinct users who enter Recommended at least twice that day / Recommended daily UV.
- Match module daily UV = distinct users who enter Match at least once that day.
- Match module daily PV = total Match module entries that day; re-entry after leaving counts again, while switching All / Recommended / Live inside Match does not.
- Match module visits per user-day = Match module daily PV / Match module daily UV.
- Match module same-day revisit rate = distinct users who enter Match at least twice that day / Match module daily UV.
- Match Detail conversion rate = distinct Match daily users who open any Match Detail that day / Match module daily UV.
- D1 / D7 Match retention rate = distinct first-exposure cohort users who return to Match on day 1 / day 7 / distinct users in the corresponding first-exposure cohort.
