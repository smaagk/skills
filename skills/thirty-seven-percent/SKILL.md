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
