# Critique: Vello Bookings tab ("Your bookings"), second pass

**Scope:** Bookings tab (Upcoming and Past) of the Vello prototype, reviewed against the Vello Design System (https://vello-design-system.vercel.app/docs/) and the user goals below. I reviewed this from the prototype's source code. Sizes and contrast ratios come from the design system's tokens and component CSS, and the contrast numbers were calculated against WCAG.

**Objective labels used in this document**

| Label | User goal |
|---|---|
| Status | Know the true status of every booking at a glance |
| Action | Find and take the right action (message, change, cancel, rebook) without hunting or mis-tapping |
| Price | Know exactly what they will pay or paid |
| Legibility | Read and use the screen whatever their vision or conditions |
| Trust | Build trust between neighbors |
| Repeat | Drive repeat bookings with trusted neighbors |
| Ratings | Collect reliable ratings for the trust model |
| Support | Cut support tickets and avoidable cancellations |
| DS | Keep the design system consistent |

## 1) Visual hierarchy vs the user's priority

| # | Goal-based question | Evidence | Objective at risk |
|---|---|---|---|
| H1 | Can a user tell which bookings are confirmed and which are still waiting without reading each card? | The status badge is the smallest text on the card (11px) and sits at the far right. The neighbor's name is the largest (16.5px bold). | Status, Support |
| H2 | When every upcoming card leads with an olive "Manage" button, which action does the user read as the one to take? | Two upcoming bookings means two primary buttons on one screen. The DS principle is "a single olive primary leads each surface." | Action, DS |
| H3 | Can a user who needs to reschedule or cancel find that from this screen without guessing what "Manage" contains? | Message is visible on the card. Change and cancel only appear after tapping Manage, and "Cancel booking" is a quiet text link on the next screen. | Action, Support |
| H4 | Does the Past tab push users to rebook the neighbors they had good visits with, or the one whose visit was cancelled? | The cancelled card (dimmed to 62% opacity) gets the primary "Book again." Completed cards, including Priya's 5-star visit, get a ghost button. | Repeat, Trust |
| H5 | Will users rate a visit if the rating ask carries the same weight as the other buttons in the row? | "Leave a rating" is a small secondary button next to "Book again," with nothing that sets it apart. | Ratings |
| H6 | Is the price on the card the amount the user will be charged? | The card shows "$24 / walk" and "$65." The booking screen adds a 10% service fee, so those become $26.40 per walk ($132.00 per week) and $71.50. | Price, Support |
| H7 | Can the user tell when Maya is next coming? | The recurring card shows "Weekdays at 3:00 PM." The next date (Mon, Jun 15) is in the data but isn't shown. | Status |

## 2) Consistency

| # | Goal-based question | Evidence | Objective at risk |
|---|---|---|---|
| C1 | If a neighbor's verification lapses or is pending, can this card show it? | The screen uses a custom `AvatarVerified` that draws a fixed "Background-checked" shield over the avatar. The DS says to use the `Avatar`'s own `verified`/`badge` props and "don't place a separate badge over an avatar yourself." The DS `VerifiedBadge` has four states (verified, pending, top-rated, unverified), each with its own shape. | Trust, DS |
| C2 | Do "visit happened" and "visit didn't happen" look the same on purpose? | Completed and Cancelled both use the `neutral` badge. The DS status palette also has `info` and `danger`. | Status, DS |
| C3 | Does "Book again" carry the same weight everywhere it appears? | It's `primary` on the cancelled card and `ghost` on completed ones. Same action, two emphasis levels. | DS, Repeat |
| C4 | Does the empty state lead users back into booking the way the DS empty state does? | The screen uses its own local `EmptyState`, not the DS component. The DS requires "a primary action," but the local version uses an `outline` button, which the DS reserves for tinted surfaces. | DS, Repeat |
| C5 | When the type scale or card style changes, will this screen update with the rest of the app? | The cards are custom `.bkl__card` markup, not the DS `Card`. Font sizes are hard-coded (16.5, 15, 13, 12.5px) instead of type tokens (12 / 14 / 16px). | DS |

## 3) Accessibility

| # | Goal-based question | Evidence | Objective at risk |
|---|---|---|---|
| A1 | Can someone with a tremor, or using one hand, tap Message without hitting Manage? | Small buttons are 36px tall with 9px between them. The DS minimum tap target is 44px. | Action, Legibility |
| A2 | Can someone reading at arm's length read the status and the date? | Status badge is 11px, the tab count 11px, the date chip 12px, "You rated" 12.5px and the service line 13px. The DS minimum is 14px. The two facts users need most are among the smallest text. | Legibility, Status |
| A3 | Can a low-vision user read the one status that needs their attention? | "Waiting on reply" is amber-700 on amber-100 at **2.84:1**, below the 4.5:1 minimum. | Legibility, Status |
| A4 | Can users read a cancelled booking at all? | The 62% opacity drops the service line to **2.49:1** and the badge to **2.27:1**. The primary "Book again" button inside is faded too. | Legibility, Repeat |
| A5 | Does a screen reader user know which booking "Manage" or "Book again" belongs to? | Every card repeats the same button labels with no neighbor or date in the accessible name, so a list of buttons reads "Manage, Manage." | Action, Legibility |

## 4) Missing states

| State | Goal-based question | Objective at risk |
|---|---|---|
| Loading, failed to load, offline | If the bookings don't load, does the user see an error, or an empty "Nothing booked yet" that's wrong? | Status, Support |
| Pending: how long, expiry, declined | How long has the user been "Waiting on reply," and what happens if Devon never answers or declines? | Status, Support |
| Cancelled: by whom, why, refund | Did the user or Sofia cancel, and was a fee charged? The cancel sheet warns that cancelling under 24 hours can affect your neighbor rating, but the card says nothing. | Price, Trust, Support |
| Today, in progress, on the way | On the day of a visit, does the card show anything other than "Confirmed"? | Status |
| Change requested or rescheduled | After a reschedule, how does the card show a change waiting on the neighbor's approval? | Status, Support |
| Payment: charged, pending, refunded, failed | Did the user pay $90 for Priya's clean, or $99 with the fee, and has it been charged? | Price, Support |
| Recurring: skipped or paused visit | Can the user see or skip a single walk in Maya's series without cancelling all of it? | Status, Repeat, Support |
| Rating submitted | After tapping "Leave a rating," no star value is collected. Only a thank-you toast appears, and the button stays, so it can be tapped again. What rating does the trust model receive? | Ratings |
| Neighbor unavailable | Sofia is marked unavailable in the data, yet her card's primary action is "Book again." What happens when the user taps it? | Repeat, Support |
| Upcoming empty for a returning user | A user with past neighbors but nothing upcoming sees "Nothing booked yet" and "Find help nearby." Why not offer to rebook a neighbor they rated well? | Repeat |
| Verification pending or lapsed | All five neighbors are verified in the data, and the custom shield can't show any other state. Has this card been tested with an unverified neighbor? | Trust |

## Highest risk

| Priority | Issue | Objective at risk |
|---|---|---|
| 1 | H6 plus the payment state: the price on the card doesn't match what the user is charged | Price, Support |
| 2 | The rating state: the rating button collects no rating | Ratings |
| 3 | A1 to A3: the status is small, low-contrast and next to 36px tap targets | Status, Legibility, Action |
