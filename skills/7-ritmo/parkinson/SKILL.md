---
name: parkinson
description: "Parkinson's law — every unit of work carries a budget, and at the budget's end what exists is delivered with its state, not extended. Use when a task keeps growing, when 'almost done' has been said twice, or when setting up any piece of work that could expand."
---

# Parkinson

Work expands to fill the time available. The defence is a **budget** set
before starting — time, attempts, or rounds — and a rule for the end of
it that is not "a bit more".

## Steps

1. **Set the budget before the first edit.** A number: minutes, attempts,
   or rounds of fix-and-retry; and the deliverable at budget end if the
   work is not finished (a report of state, a partial with its gaps
   marked, a handoff).
   _Done when_: the number and the fallback deliverable are written.

2. **Check at the halfway mark.** Is the remaining work ≤ the remaining
   budget? If not, cut scope now, not at the end: what is dropped is
   named.
   _Done when_: a halfway note exists: on track, or scope cut with the
   list.

3. **Deliver at the budget, whatever exists.** The fallback from step 1,
   with the state exact: what works, what does not, what was cut. Asking
   for more budget is a new decision for the receiver, made on that
   report — not a default.
   _Done when_: the deliverable is handed over at or before the budget.

## Example

Illustrative scenario; paths, commands, and results below are examples, not
artifacts or measurements from this repository.

**Request:** “Spend 30 minutes investigating the flaky export test.”

Set the deliverable before starting: either a reproduced cause with
command output or an investigation report with the remaining uncertainty.
At minute 15, suppose two timezone cases reproduce consistently but the
CI-only failure does not. Drop the optional formatter comparison and
record the cut; spend the remaining time comparing CI inputs with the
local reproducer. At minute 30, hand over the evidence and state that the
CI cause is still unproved if it is. Do not silently extend the budget
or describe the investigation as a completed fix.
