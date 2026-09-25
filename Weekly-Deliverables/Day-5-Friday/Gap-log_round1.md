# Gap Log: Prototype Round 1

**Brief tested:** `brief_first-booking_draft2.md` (Draft 2)
**Prototype:** `Vello First Booking.html` (Claude Design, round 1), 11 screens plus sheets: R1 to R8 for the requester, P1 to P3 for the provider
**Sources:** the decision list Claude Design returned, and a manual pass through the prototype

## How decisions were sorted

Claude Design reported about 40 decisions. Not every one of them is a hole in the brief. The brief deliberately leaves the solution to design, so a decision only counts as a gap if a designer shouldn't have made it alone: scope, business rules, or what the flow must cover.

| Bucket | Count | Meaning |
|---|---|---|
| Gap in the brief | 8 | The brief should have answered it. Patched in Draft 3 |
| Design choice | 10 | The solution itself. The brief was right to leave it open |

**Round 1 incompleteness score: 8 gaps.**

## Gaps in the brief

| # | Screen | Decision forced | Type | What the prototype assumed | Brief section that should cover it | How it's closed (proposed) |
|---|---|---|---|---|---|---|
| 1 | All screens | Which states must the flow cover beyond the happy path? | Empty / error / loading | Mostly the happy path. The only other states are a waiting screen, a pending booking and one form error. No empty states, no failed actions, no declined or cancelled bookings | Constraints | Constraint: the flow must cover empty, loading, error and cancelled states for both roles. List the required states in the brief (see the table below) |
| 2 | R5, nav bar | Does one-to-one messaging before booking exist, and does it stay? | Other (scope) | Not included. The Messages tab is in the nav but goes nowhere, and group questions are the only way to contact providers. The brief never said the current app already has messaging | Constraints | Constraint: list the existing features the flow must keep. One-to-one messaging before booking stays alongside any new flow |
| 3 | Booking sheet, R6 | How is payment handled? | Other (business) | "You pay Ama directly. Vello doesn't handle payment." | Goal (definition of completed booking) | Constraint: payment is out of scope. Show price per visit with its unit. Don't state how payment happens |
| 4 | R8 | Can a provider respond to a "late" or "didn't come" record? | Error | No. Records show exactly as the requester reported them, with no way to respond. Disputes are out of scope | Constraints (scope row) | Constraint: a provider can add one short public reply to a late or missed record. No admin involvement. Full disputes stay out of scope |
| 5 | R2 | Who receives a posted request? | Other (scope) | Verified cleaners within 2 miles, a fixed radius | Constraints (neighborhood row) | Constraint: requests go to verified providers whose service area includes the neighborhood. No fixed radius |
| 6 | R3 | Who can see a provider's answers to the requester's questions? | Other (visibility) | Only the requester, implied by the Compare tab but never stated | Constraints | Constraint: answers are visible only to the requester who asked |
| 7 | R2 | Can requesters ask their own questions, or only pick from a list? | Other (scope) | Only preset questions: pick up to 3 from a list of 4 (getting in, running late, supplies, the cat). A requester with a different concern has no way to ask it. Found in the manual pass | What (the problem) and Constraints | What: requesters need to learn different things before choosing (P01 reliability, P03 an exact arrival time, P02 checks for childcare), so a fixed list can't cover them. Constraint: requesters can add at least one question in their own words. Suggested questions are allowed, and design decides how custom answers are compared |
| 8 | R3, R5 | Do newcomers and established providers share one card and profile structure, and what does a requester see first? | Other (information priority) | Two different profiles. Established providers get About plus reviews. The newcomer gets answers, references, verification, "In her words" and an empty Vello record card, in a different order and with more explanatory copy. Reply cards carry up to seven facts each (availability, answers, references, reply time, distance, price, badges) with no clear priority. Found in the manual pass | What (the problem) and Constraints | Constraint: every provider card and profile uses the same structure and order, with or without reviews. References from clients outside Vello sit in the same place as reviews, labeled as outside Vello. A section with no data gets one short line, not a large empty card. Priority order, from the Day 2 evidence: 1. can they come when I need, 2. answers to my questions, 3. what people who've used them say (reviews or references), 4. arrival record, 5. price, 6. verification and self-description. Cards show only the first three plus price and trust status; everything else lives on the profile |

### States required for gap 1

| Role | State | Type |
|---|---|---|
| Requester | No replies, then still none after two days | Empty |
| Requester | Only newly verified providers reply | Empty |
| Requester | Replies or profile still loading | Loading |
| Requester | Provider declines the booking request, or it expires | Error |
| Requester | Newcomer cancels the first visit | Error |
| Requester | Posting the job or sending the booking request fails | Error |
| Provider | Approved, but no matching jobs nearby | Empty |
| Provider | Replies to a job that has just been filled | Error |
| Provider | Requester books someone else | Other |

## Design choices (not gaps)

These are the solution. The brief left them open on purpose, and each fits its constraints.

| Screen | Choice |
|---|---|
| R3 | Compare tab grouping answers by question, with an honest "No Vello reviews yet" row |
| R4 | Newcomer mixed into the main list with an optional "New to Vello" filter |
| R5 | "No Vello reviews yet" stated at the top of the profile; answers shown first |
| R5 | Admin not named, and a line saying admins don't vouch for work quality |
| Booking sheet | "Start with one visit" as the default, to lower commitment without a discount |
| Booking sheet | Booking is a request the provider confirms, so there's a pending state |
| R6 | "What happens next" list setting expectations on lateness and confirmation |
| R7, P3 | Two-sided arrival record: provider taps "I'm here", requester confirms on time, late or didn't come |
| P1 | Provider sets their own arrival window (15 or 30 minutes) |
| P2 | Provider sees a preview of their card as the requester sees it |

**One finding worth noting:** the brief no longer mentions vouching, yet the prototype arrived at named references from a newcomer's real clients on its own. Starting from the problem led back to a form of vouching, which supports the original hypothesis without the brief prescribing it.
