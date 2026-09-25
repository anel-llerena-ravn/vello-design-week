# Stress test: Request phase user flow

**Flow:** Sam posts a request for a weekday dog walker for Loki and waits for the first replies. It runs from tapping + to seeing the replies, where the Compare phase starts.

**Stress-tested flow:** [Walk Request Flow v2](https://claude.ai/artifact/4KVN9G4hgBzyWwrfd8vcPF) · local file `User-flow_request-phase_v2.html`

## Where I corrected Claude

| Claude's first draft | Correction | Why it mattered |
|---|---|---|
| Assumptions like "Posting can't fail" and "Loads instantly, never fails" | We can't assume that. The flow has to plan for specific scenarios, like the internet connection dropping mid request creation. | A flow that assumes nothing fails has no states for when it does. |

## Gaps, from most to least critical

| # | What if… | What the flow did | Missing state | What Sam should see |
|---|---|---|---|---|
| 1 | Sam's address is inside the neighborhood, but no verified dog walker covers that street? | Sam gets "Request posted to your block" and "Neighbors usually answer within a couple of hours" anyway. | Empty: no walkers nearby | S5 says no walkers cover the street yet, keeps the request open for new walkers, and offers Browse neighbors. |
| 2 | Sam loses connection right as they tap Post? | One note says posting waits for a connection and another says it fails, so Sam can't tell if Loki's request went out. | Error: not sure it posted | A clear message saying whether the request is live or still waiting to post, and trying again never posts it twice. |
| 3 | Elena replies and is then removed by a Community Admin before Sam opens the replies? | Only a walker who withdraws is covered, so Elena's reply would still show as verified and bookable. | Error: reply no longer available | Elena's reply shows "No longer available on Vello", Book is off, and the reply count drops. |
| 4 | Sam posts a second dog-walking request by mistake? | S2 lets Sam post another without saying what happens to the first, and the prototype replaces it along with its replies. | Conflict: two open requests | S2 says the first request and its replies stay, and Sam can see both requests and delete the extra one. |
| 5 | No walker ever replies? | S5 keeps saying "usually within a couple of hours" for days, and the 24-hour nudge has no screen. | Empty: still no replies after a day | After 24 hours S5 explains that nobody has replied yet and offers to widen the time or budget, or browse neighbors. |

## Missing states caught

| State type | Where | What it covers |
|---|---|---|
| Empty | S5 | No walkers cover the street |
| Empty | S5 · Nudge | No replies after 24 hours |
| Error | Posting | Connection lost, not sure the request went out |
| Error | S8 | A reply from a walker who was removed |
| Conflict | S2 | Two open requests for the same need |

Every screen in the flow now lists its Loading, Empty, Error and Success states.

## Assumptions to verify

Each one is a gap between the flow and Vello's current screens.

**The screen exists, but behaves differently**

- **#1** The empty-category button on Home opens the request form.
- **#2** A second request keeps both open, instead of replacing the first.
- **#3** Leaving a filled-in form asks before discarding.
- **#4** Addresses outside Vello's area are blocked, with a waitlist.
- **#6** Only walkers who cover the street get the request, and Sam is told when there are none.
- **#7** Sam can edit or close a request, and walkers who replied are told.
- **#10** Each reply sends a push. With notifications off, only the Home card updates.

**Nothing exists yet**

- **#5** A lost connection keeps the draft and never posts twice.
- **#8** After 24 hours with no replies, Sam gets a nudge.
- **#9** Requests with no replies expire after 7 days.
- **#11** A walker removed by an admin shows as no longer available.

## One gap between the flow and Vello's current screens

**Assumption #6: who gets the request.** The prototype always shows "Request posted to your block", whether or not a walker covers Sam's street. The flow adds a check (D6), and if no walker covers the street, S5 tells Sam and keeps the request open.

## One place the journey reveals a need a screen alone wouldn't

**The Wait stage.** Looking at S5 alone, the problem looks like an empty state. The journey shows that Sam isn't looking at S5: Sam is at work, hopeful but uncertain, thinking "Will anyone be free every single weekday?"

- **The problem:** between posting and the first reply, Sam has no way to know whether anything is happening, and Vello says nothing unless Sam opens the app.
- **Why a screen misses it:** the problem only appears over time, and a single screen doesn't show time passing.
- **Ideas to explore:** telling Sam when a walker replies, checking in when a day goes by with no replies, or showing how many walkers have seen the request.
