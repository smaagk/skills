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

## Example

Illustrative scenario; paths, commands, and results below are examples, not
artifacts or measurements from this repository.

**Request:** “Triage these review findings within a two-hour fix budget.”

Score a tenant-data leak as data / 60 minutes, a crash on empty results
as a case / 30 minutes, and eight naming nits as nothing / 10 minutes
each. Put the leak and crash above the line, reserve the remaining
30 minutes for their regression checks, and leave the nits below it.
After the authorization and empty-result checks pass, report those two
fixed. List all eight nits as unattended with their scores and locations.
If the leak takes the full budget, explicitly leave the crash open; do
not call it fixed because it was above the original line.
