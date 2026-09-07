---
name: hansei
description: "Hansei at the close of a piece of work — what went wrong by our own doing, not by luck, and what changes next time. Use when closing an issue, a batch, a sprint, or a session that produced metrics, incidents, or surprises."
---

# Hansei

Toyota's reflection: before celebrating, name what went wrong *because of
us*. Not blame — the point is that a problem attributed to luck cannot be
fixed, and one attributed to us can. Three lines, honest, filed where the
next run will read them.

## Steps

1. **Separate luck from cause.** For each surprise, delay, or failure in
   the work: was it outside our control, or a decision, omission, or habit
   of ours? Bad luck that recurs is a cause with a disguise.
   _Done when_: every item is labelled luck or ours, and any "luck" that has
   happened before is relabelled ours.

2. **One change per cause.** For each "ours": the single concrete change —
   a check, a default, a wording, a skill line — that would have prevented
   it. Not "be more careful".
   _Done when_: each cause has a change that a stranger could apply.

3. **File it where it fires.** Put each change in the place the next run
   reads before making the same decision — the skill, the checklist, the
   template, the project memory. A reflection kept in the closing summary
   is a reflection lost.
   _Done when_: each change has a locator in that place.

## Example

Illustrative scenario; paths, commands, and results below are examples, not
artifacts or measurements from this repository.

**Request:** “Reflect on why this small change needed three review rounds.”

Separate the surprises: a one-off provider outage was outside our control;
missing the tenant-switch scenario was our omission; repeating a rejected
API shape was our failure to read the recorded decision. For the first
controllable cause, add the tenant-switch case to
`tests/cache-isolation.spec.ts`. For the second, link the accepted contract
from the implementation template at `docs/templates/change.md:12`.
Record each change with its locator. “Review more carefully” would not
prevent either recurrence, and a lesson left only in the closing message
would not reach the next implementation.
