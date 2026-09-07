---
name: working-backwards
description: "Working backwards from the finished state — write what 'done' looks like to its user before planning a step. Use when starting a plan, a feature, a migration, or a refactor, or when a plan's first step is being written before its last."
---

# Working Backwards

Amazon's discipline: write the announcement before the product. For a
plan, the **end state** comes first — observable, from the seat of whoever
uses the result — and every step is derived by asking what must be true
just before it. A plan written forwards accumulates steps; a plan written
backwards accumulates only the necessary ones.

## Steps

1. **Write the end state.** In the user's words, present tense: what they
   can do, see, or stop doing when the work is finished; and the one check
   that proves it (a command, a screen, a query).
   _Done when_: a stranger could run the check and say yes or no.

2. **Derive backwards.** Ask "what must already be true for that?" and
   write that as the previous step, until you reach the current state.
   Each step carries its own check.
   _Done when_: the chain reaches something true today, and every step has
   a check.

3. **Cut what the chain never touched.** Anything you planned to do that
   no step of the chain requires is out of scope — record it as such.
   _Done when_: the plan holds only chain steps, and the cut items are
   listed with the reason "not on the chain".

## Example

Illustrative scenario; paths, commands, and results below are examples, not
artifacts or measurements from this repository.

**Request:** “Let administrators export the invoices visible on screen.”

End state: “I download a CSV containing exactly the invoices selected by
my current filters.” Proof: an acceptance test filters to March and
compares downloaded IDs with the March fixture. Derive backwards:
download preserves filters ← export endpoint applies those filters ←
query returns the selected invoices ← invoice records already exist.
Give the endpoint a response assertion and the query a fixture check.
A chart dashboard and a new reporting framework are not prerequisites;
record them as outside this chain rather than adding them to the plan.
