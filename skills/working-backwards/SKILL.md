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
