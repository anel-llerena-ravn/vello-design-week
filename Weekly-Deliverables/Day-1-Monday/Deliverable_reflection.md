# Monday reflection: Design process mapping


## What design owns

Design is a decision-making discipline, not a layer of polish applied at the end. The visual craft is real, but it sits on top of harder decisions: who the user is, what problem is actually being solved, and which of many possible solutions is the right one. Design owns that full stack, from strategy through craft to the final user-experience call, across the whole lifecycle from Discover to Validate & hand off.

## What product contributes across the lifecycle

| Phase | Product's contribution |
|---|---|
| Discover | Flag which role is least understood, on Vello that is Admin, and which business assumptions are unproven, such as whether neighborhood trust generalizes past one pilot area |
| Define | Write the problem statement as a problem and a constraint, not a feature list, and name the sequencing question: who goes live first, requesters, providers, or admins |
| Architect | Surface states design might not think to ask about, such as what a brand new neighborhood with zero verified providers looks like on day one |
| Design | Hand over real edge-case content, a provider with no reviews, a disputed booking, instead of finished opinions about layout |
| Validate & hand off | Decide what is worth testing before launch, such as whether an admin verification call is more likely to fail as a false positive or a false negative, and what each one costs |

## Two things I pushed back on

**1. The Design phase was too generic.**
Initial map: requester, provider, and admin treated as one single flow. What the pushback surfaced: the admin is really an internal tool for the team, not a customer-facing screen. Providers need more than a star rating, the brief itself says they want to be known for their skill, not just their speed. A generic map would have missed both points.

**2. The bootstrap problem was hidden instead of named.**
Vello has a loop between the three roles: requesters need providers to exist, providers need admin approval to show up, admins need providers to review in the first place. The first map buried this loop inside the Architect phase. It should be its own decision, made on purpose by product: who is live on day one of the pilot. It should not be something engineering or design discovers later, when they open the app to an empty neighborhood.

## One decision I'd reframe

| | |
|---|---|
| Solution as proposed | Add a verified badge or trust level to the ProviderCard |
| Problem underneath | We don't know what makes a Kestrel Park resident trust a stranger enough to let them into their home. A badge is one guess at an answer, not a proven one |

This matters because it is not a small UI detail, it is the core idea the whole product depends on. The brief's central claim is that trust scales locally. A badge system is the kind of solution the program warns PMs about: it looks finished, but nobody tested it. It skips the research that would tell us if a badge is even the right signal. Trust here might come from something else instead, repeat bookings, a neighbor's name on a review, or an admin the residents already know in person. If we approve the badge as a UI spec before we answer that question, we build the whole product on an assumption nobody tested.
