---
name: lindy
description: "Lindy effect for dependency and pattern choice — what has survived long is likelier to keep surviving. Use when choosing a library, framework feature, pattern, or tool, when a review proposes replacing an existing one, or when 'the newer way' is on the table."
---

# Lindy

For non-perishables, expected remaining life grows with age. A pattern
that has lived in the repo for years, or a library that has survived
several major versions of its ecosystem, carries evidence the new option
cannot have yet. Novelty is a cost to be justified, not a feature.

## Steps

1. **Age both options.** For the incumbent and the candidate: years in
   existence, years in this repo, number of ecosystem major versions
   survived, and whether it is still maintained.
   _Done when_: the four figures are written for both.

2. **Name the concrete gap.** What the incumbent cannot do that the task
   needs — a feature, a fixed bug, a dropped platform — with a locator.
   "Cleaner", "modern", "recommended" are not gaps.
   _Done when_: a gap with a locator exists, or the candidate is dropped.

3. **Price the switch.** Files touched, tests re-verified, migration path,
   and rollback.
   _Done when_: the decision cites the gap from step 2 against the price
   from step 3, and the reason is recorded where the next chooser will
   find it.
