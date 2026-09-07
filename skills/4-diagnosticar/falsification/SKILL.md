---
name: falsification
description: "Falsification before a fix — write the prediction the diagnosis forbids and run it before touching code. Use when diagnosing a bug, a flaky test, a performance regression, or any 'it works now' whose cause is unproven."
---

# Falsification

A diagnosis is worth what it **forbids** (Popper). "It's the cache" earns
nothing until it predicts something that must NOT happen if it is true — and
that prediction has been tested. A fix applied before that step is a
coincidence with a commit message.

## Steps

1. **State the hypothesis as a prohibition.** "If the cause is X, then Y
   cannot happen." Y must be observable with one command or one input.
   _Done when_: the forbidden observation and the command that would produce
   it are written down.

2. **Try to produce Y.** Run the command that should fail to produce Y. If
   Y appears, the hypothesis is dead — write the next one; do not patch
   around a dead hypothesis.
   _Done when_: the output is captured and the hypothesis is marked alive or
   dead.

3. **Occam before the second hypothesis.** When two hypotheses survive,
   test first the one that assumes fewer broken parts.
   _Done when_: the surviving hypotheses are ordered by parts assumed broken.

4. **Fix one thing.** Change only what the live hypothesis names, then re-run
   the original failure and the prohibition from step 1.
   _Done when_: the original failure is green and Y still does not appear.
   A fix that needed a second change was a second hypothesis — go back to 1.

## Example

Illustrative scenario; paths, commands, and results below are examples, not
artifacts or measurements from this repository.

**Request:** “The API returns an old invoice amount. Is it the response cache?”

Hypothesis: “If only the response cache is stale, a direct database query
cannot return the old amount.” Query the same invoice ID in a test
environment, bypassing that cache. If it still returns the old amount,
mark the cache-only hypothesis dead and investigate the write path.
If storage contains the new amount while the cached response is old,
the hypothesis survives, but is not yet proved. Check the invalidation
path, fix the identified omission alone, then rerun the original update
and request sequence plus the direct query. Both must show the new amount.
