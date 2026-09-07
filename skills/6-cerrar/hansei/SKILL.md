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

**Request:** “The thumbnail service failed again. Was this just provider bad luck?”

`logs/thumbnails.txt:18` records a provider 503; the previous incident at
`docs/incidents/thumbnail-1.md:9` records the same trigger. We did not cause
the outage. But our worker has no bounded retry or failed-job state, so
users again see an endless spinner. Calling the entire incident “luck”
hides the behavior we control.

Record the reflection where the next implementation reads it:

```text
Cause we own: transient provider errors leave thumbnail jobs permanently pending.
Change: bounded retries, then an explicit failed state; preserve successful jobs.
Locator: worker contract in docs/thumbnail-jobs.md:24 and regression in tests/thumbnail-retry.spec.ts.
```

Verify repeated 503s exhaust the budget and surface failure. If the provider
returns a permanent “unsupported format” error instead, retries are the
wrong correction; expose that failure immediately. The lesson changes an
observed failure path, not every interaction with a provider.
