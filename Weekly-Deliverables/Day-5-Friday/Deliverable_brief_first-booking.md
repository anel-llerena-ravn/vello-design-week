# Design Brief: Newly Verified Providers Can't Get Their First Local Booking


## Who

| Role | Who they are |
|---|---|
| **Primary: newly verified provider** | A provider a Community Admin has approved who has no completed bookings on Vello yet. They may have clients elsewhere, but no one in this neighborhood has used them |
| **Secondary: requester** | A neighborhood resident booking recurring help in their home, such as weekly cleaning or daily dog walks, and deciding which provider to choose |

The problem shows up at the requester's decision, so the core flow to prototype is theirs: a requester posts a recurring in-home job, gets replies that include a newly verified provider, and decides whom to book.

## What (the problem)

Newly verified providers have no local track record, making it difficult for requesters to decide whether to book them. Requesters often rely on recommendations from people they know when choosing someone to work in their home. A new provider has neither a personal recommendation nor a history on Vello, leaving the requester with little information beyond the Verified badge. This is a problem because providers need a first booking to build a track record, but without a track record they may struggle to get that first booking.


## Why it matters

| For | Why |
|---|---|
| **Providers** | They joined for steady local work. If approval leads to no bookings, they leave before completing a single job |
| **Requesters and Vello** | Vello's bet is that trust scales locally. If trust only goes to providers who are already known, Vello recreates the closed referral lists it promised to open up. Requesters without a local network, the group Vello most needs to serve, keep seeing the same few names |

## Evidence

### What we know

Source: six Kestrel Park discovery interviews (Day 2). Themes 1 to 4 were audited against the transcripts. Anything else is marked unaudited.

| Finding | Evidence |
|---|---|
| Requesters find providers through a named person they know | 5 of 6 (theme 1, audited). P06's rule for the trades list: "Somebody who lives here has to have used them and said they were good." This describes how people found providers before Vello, not how they choose on a platform |
| Providers can't control how fast they get new clients | P04, established with 14 clients: "If I want two new clients this month, I can't make that happen." P06 added a provider to the trades list "about four months after she should have" because P06 didn't know the person vouching for them (theme 2, audited). No newly verified provider has been interviewed |
| Ongoing in-home work needs more trust than one-off jobs | 4 of 6 (theme 4, audited). P01: "One-off thing, in and out, I don't care who it is, just be competent. Ongoing thing, someone in my house, someone with my kids, completely different question." This is why the brief is scoped to recurring work |
| Reliability is what requesters most want to know | 4 of 6 (theme 3, audited). P01, on what they want to know: "Whether he'll turn up." P03: "Just tell me a time. Not a window, a time." P05: "Turning up. That's ninety per cent of it" |
| Star ratings are only partly trusted | P01: "Stars are meaningless, everyone's four point eight." P02: "I read them but I don't believe them." But P01 has booked a sitter "based on reviews, and she was great" (unaudited) |
| Generic local labels don't build trust | P02 on "neighbour used them": "that's just a stranger who lives nearby" (unaudited) |
| One bad public record weighs heavily when it's the only one | P04, on an unfair review they couldn't answer: "That review is still there and it's the only one I've got" (theme 8, unaudited) |
| The current flow has no design for a provider with no reviews | Day 3 flow lists "Provider has no reviews yet" as an unhandled edge case. That flow was a dog-walking journey in Bay Ridge, not Kestrel Park |
| Without explicit rules, design fills the gaps itself | Prototype round 1, built from Draft 2, dropped existing messaging, moved payment off the platform, used a fixed radius, gave newcomers a different profile, and built only the happy path |


## Goal

| Type | Metric | Target |
|---|---|---|
| **Primary** | Share of newly verified providers with a first completed booking within 30 days of approval | From unknown to 70%. The 30-day window is a starting point until booking frequency is known |
| **Secondary** | Share of first bookings followed by a second booking from the same requester | From unknown to 50%. Vello's model depends on repeat work |

A "completed booking" means a booking confirmed in Vello and marked done. Payment is out of scope, so it isn't part of the definition. 

## Constraints

- [ ] Recurring in-home work only. One-off jobs, providers waiting for verification, disputes, payment and the provider's flow are out of scope.
- [ ] Admin verification stays and happens first. This work starts after approval.
- [ ] No added admin work per provider.
- [ ] No funded, discounted or assigned first jobs. Vello can make a newcomer easier to choose, not pay for or hand out work.
- [ ] Existing features stay: messaging before booking, both booking routes, booking as a request the provider accepts, and ratings and reviews. Nothing is removed unless this brief says so.
- [ ] Providers reach requesters through their service area. No fixed radius, and providers don't have to live there.
- [ ] Anything shown about a provider must come from a real person or a real event, with a clear source.
- [ ] Newly verified providers get the same information structure as established providers, not a separate or lesser format.
- [ ] A provider's reply is visible only to that requester. Vello uses only the requester's neighborhood, booking history and ratings, never phone contacts.
- [ ] Every action covers all the different states:
  - [ ] **Loading:** shows the action is in progress
  - [ ] **Success:** confirms what happened and what comes next
  - [ ] **Error:** says what went wrong and lets the requester try again without losing what they entered