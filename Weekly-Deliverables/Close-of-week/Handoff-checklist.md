# Handoff Checklist

A gate for the moment work changes hands between product and design. Every box is checked before the work moves on. If a box can't be checked, it's either fixed or written down as an open question with an owner and a default answer.

## Brief to design

The PM's handoff. The test: could a designer with no extra context build a coherent flow from this brief alone?

### Problem

- [ ] The problem names who has it, what the pain is and why it matters, with no feature, screen or UI element in it
- [ ] Every solution-shaped request behind the work has been rewritten as a problem ("add a badge" becomes "residents don't know what makes a stranger trustworthy")

- [ ] The solution is explicitly left to design

### Evidence

- [ ] Each finding links back to a source: a verbatim quote, a data point or a product audit
- [ ] AI-generated synthesis was manually checked against the transcripts
- [ ] Unaudited findings and single-participant claims are marked as such
- [ ] Missing evidence is named, including which user group hasn't been heard from yet


### Goal

- [ ] One primary metric with a baseline and a target
- [ ] Any term the metric depends on is defined ("completed booking" means confirmed and marked done)
- [ ] The metric can actually be measured in the current product

### Scope and constraints

- [ ] What's in and out of scope is explicit, including separate systems the flow must not touch
- [ ] Existing features the flow must keep are listed by name, so a new feature can't quietly replace one
- [ ] Constraints describe what must be true, not how the screen should look
- [ ] Technical and business limits are flagged now, not discovered during build (for example, no payment step exists)
- [ ] Every trust or safety rule the product depends on is stated

### Flow and states

- [ ] Required states are listed for every action: empty, loading, success, error, partial and, where the flow needs access, permission denied
- [ ] Known edge cases are written down before design starts (no replies, the other side declines, a cancellation)
