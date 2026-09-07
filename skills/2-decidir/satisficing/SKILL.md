---
name: satisficing
description: "Satisficing — set the good-enough threshold before searching, and take the first option that crosses it. Use when comparing designs, libraries, approaches, or wordings, when a search for alternatives has no end condition, or when the third option was already fine."
---

# Satisficing

Simon's word: optimising searches for the best; **satisficing** searches
for the first that is good enough — and knows what good enough is before
looking, or the search never ends.

## Steps

1. **Write the threshold first.** The criteria an option must meet, each
   checkable, before any option is examined. No ranking criteria, only
   pass/fail ones.
   _Done when_: the threshold is written and contains no "best" or
   "most".

2. **Examine in order of cheapness.** Cheapest to evaluate first
   (already in the repo, already known, already installed). Stop at the
   first that passes every criterion.
   _Done when_: an option passed, or all cheap options are exhausted.

3. **Take it and record why it was enough.** The passing option, the
   criteria it met, and how many options were examined. Options not
   examined are not listed as rejected — they were not looked at.
   _Done when_: the decision cites the threshold, not a comparison.

## Example

Illustrative scenario; paths, commands, and results below are examples, not
artifacts or measurements from this repository.

**Request:** “Choose a date formatter for these receipts.”

Before looking, write the threshold: Spanish month names, an explicit
Mexico City timezone, correct day around UTC midnight, and no additional
runtime dependency. Evaluate the platform formatter already used by the
repo first. Suppose its output passes the locale and boundary fixtures;
choose it and stop. Record “1 option examined; all four criteria pass.”
Do not claim other libraries were rejected or build a comparison matrix
for options never inspected. If the boundary fixture fails, continue to
the next cheapest option using the same threshold.
