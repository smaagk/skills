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

**Request:** “Choose search for our 200-page internal handbook.”

Before evaluating options, set pass/fail criteria: all 12 named lookup
queries return their target page in the first five results, access remains
private, and editors can maintain the index without another service.
Suppose the static site's existing search passes all three. Stop and
record “one option examined; 12/12 lookup queries pass.” A vector-search
comparison might be interesting, but it would not change this decision.

If the agreed query set includes misspellings and existing search passes
only 8/12, it fails: evaluate the next cheapest option against the same
threshold. Do not remove four queries after seeing the result to make the
incumbent pass. A later, genuinely new requirement can reopen the choice;
that is different from never finishing the current search.
