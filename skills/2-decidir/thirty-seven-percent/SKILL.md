---
name: thirty-seven-percent
description: "37% rule — explore without committing for the first third of a budget, then take the first option better than everything seen. Use when choosing among options that arrive one at a time under a fixed budget of attempts, candidates, or time, and you cannot go back."
---

# 37% Rule

The optimal-stopping answer to the secretary problem: with n candidates
seen one at a time and no going back, look at the first n/e (≈37%)
without choosing, then take the first that beats all of them. It applies
whenever options are sequential, the budget is fixed, and the rejected
cannot be recalled.

## Steps

1. **Fix n.** The budget: number of candidates you will see, attempts you
   will make, or minutes you will spend. Confirm the rejected cannot be
   recalled; if they can, use /satisficing instead.
   _Done when_: n is a number and recall is confirmed impossible.

2. **Look, don't leap, for the first 37%.** Evaluate each candidate fully,
   record the best so far, choose none.
   _Done when_: ⌈0.37·n⌉ candidates are logged with a running best.

3. **Take the first that beats the best.** From then on, the first
   candidate better than the running best is the choice. If none appears,
   the last candidate is taken — that is the known cost of the rule.
   _Done when_: a choice is made and the log shows the threshold it beat.

## Example

Illustrative scenario; paths, commands, and results below are examples, not
artifacts or measurements from this repository.

**Request:** “Choose one of ten sequential, one-time offers in a simulation;
an offer expires as soon as we pass.”

Fix n = 10 and use the simulation's score as the ranking criterion.
Observe the first ⌈0.37 × 10⌉ = 4 without choosing: 42, 70, 55, 63.
The benchmark is 70. Offer 5 scores 68, so pass; offer 6 scores 74,
so take it and stop. If offers 5–9 never beat 70, take offer 10 as the
stated fallback even if worse. If earlier offers remain available, this
example's no-recall condition fails; use satisficing instead.
