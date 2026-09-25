# Deliverable: Bookings Critique Log

**Screens:** S1 Your bookings, Upcoming · S2 Your bookings, Past · S3 Your booking (confirmed), including the cancel sheet
**User:** the requester

## Objectives

| Code | Owner | Objective |
|---|---|---|
| U1 | Requester | Know the true status of every booking at a glance |
| U2 | Requester | Find and take the right action without hunting or mis-tapping |
| U3 | Requester | Know exactly what they will pay or paid |
| U4 | Requester | Read and use the screen whatever their vision or conditions |
| B1 | Vello | Build trust between neighbors |
| B2 | Vello | Drive repeat bookings with trusted neighbors |
| B3 | Vello | Collect reliable ratings for the trust model |
| B4 | Vello | Cut support tickets and avoidable cancellations |
| B5 | Vello | Keep the design system consistent |

## Critique log

| # | Finding | Goal-based question | Obj. | Category | Found by |
|---|---|---|---|---|---|
| 1 | Devon's "Waiting on reply" booking shows as "Confirmed" | Can the requester trust that a confirmed booking is really happening? | U1, B1 | States | Me |
| 2 | "Leave a rating" and "Message Maya" say thanks without doing anything | When the app says something worked, can the requester believe it? Is Vello getting the ratings it needs? | B1, B3 | States | Both |
| 3 | The status is the hardest thing to read on the card | Can the requester see which bookings are on without reading every card? | U1, U4 | Hierarchy, accessibility | Both |
| 4 | The price changes between the card and the booking screen | Does the requester know what they'll actually pay? | U3, B4 | Consistency | Both |
| 5 | There's no way to change one walk, and cancel doesn't say one or all | Can the requester change a recurring booking without cancelling all of it? | U2, B4 | States | Claude |
| 6 | The loudest "Book again" is on the cancelled card | Does the Past tab lead the requester back to the neighbors they liked? | B2, B5 | Hierarchy, consistency | Both |
| 7 | Buttons are too small to tap reliably | Can the requester tap the right button on the first try, even on the move? | U2, U4 | Accessibility | Both |

Coverage of the four categories: hierarchy (#3, #6), consistency (#4, #6), accessibility (#3, #7), states (#1, #2, #5).

**Marked-up screens:** every comment pinned to the Vello screens, with the evidence for each one: [Bookings Critique Markup](https://claude.ai/artifact/Xf4siQ5S7rgFg3HT4ufqQn)

## Taste slips

Each comment from the manual pass was checked with two questions: without the objective, is it just a preference? Is there evidence, or only an opinion?

| # | Comment | Why it's taste | Action |
|---|---|---|---|
| T1 | Empty space on the right of each card doesn't look standardized | Layout preference. No evidence it slows anyone down | Dropped |
| T2 | Manage and Message look too similar | Visual impression. The screen shows a filled button next to an outlined one | Re-anchored: both buttons lead to Message (U2) |
| T3 | Book again looks like plain text | Perception, not tested | Kept only the checkable part: Book again has a different style on each card (#6) |
| T4 | Good hierarchy between name, task and date. The date format on Past helps scanning | Praise based on a read of the screen, with no evidence | Left out of the log |

Not every first impression was taste. The grey filter on cancelled cards looked hard to read, and measuring the contrast (2.28 to 2.52:1) confirmed it.

**Comments without an objective:** T1 and T4 had no objective when written. T2 and T3 had a related goal, but the comment itself was about looks. Every point in Claude's second pass named an objective.