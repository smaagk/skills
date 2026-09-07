---
name: pareto
description: "Pareto triage — attend the few findings that carry most of the damage first, and state explicitly what is left unattended. Use when a review, audit, scan, or bug list returns more items than the budget allows, or when nits are being fixed while a blocker waits."
---

# Pareto

A minority of findings carries the majority of the damage. The failure
mode is a full list worked top to bottom — ten nits fixed, the blocker
still open — because the list's order was the finder's, not the damage's.

## Steps

1. **Score by damage, not by position.** For each item: what breaks if
   unfixed (nothing / a case / a user / everyone / data), and how cheap
   the fix is.
   _Done when_: every item has both scores.

2. **Cut the line.** Order by damage descending; the line falls where the
   cumulative damage above it is most of the total, or where the budget
   ends — whichever comes first. Cheap fixes below the line may be
   pulled up only if they cost less than deciding.
   _Done when_: the line is drawn and the items above it are named.

3. **Fix above, declare below.** Work the items above the line to done.
   The items below are listed in the report as unattended, with their
   scores — never silently dropped.
   _Done when_: above-the-line items are done and the below-the-line list
   is in the report.
