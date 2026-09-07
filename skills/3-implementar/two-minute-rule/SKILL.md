---
name: two-minute-rule
description: "Two-minute rule — if a discovered fix is obvious, single-file, and needs no new proof, do it now instead of parking it. Use when a tangent is found during focused work and the choice is fix-now versus park, or when a parking list fills with trivia."
---

# Two-Minute Rule

GTD's counterweight to parking: some things cost more to write down than
to do. The rule draws the line so that parking stays for what deserves a
decision, not for typos.

## The test

Do it now only if all hold:

- one file, one obvious edit, no design choice;
- the existing proof already covers it (no new test, no new command);
- it cannot change behaviour for anyone but the case it fixes;
- it would not need its own explanation in a review.

Fail any one → park it.

## Steps

1. **Apply the test in one line.** Write the four verdicts next to the
   discovery.
   _Done when_: four yes/no answers exist.

2. **Do or park.** Four yes: make the edit, note it in the report as
   "two-minute: <what>". Any no: one line in the parking list, and back to
   the unit.
   _Done when_: the discovery is either edited-and-noted or parked, and no
   more than a minute of context was spent deciding.

## Example

Illustrative scenario; paths, commands, and results below are examples, not
artifacts or measurements from this repository.

**Request:** “While fixing the empty state, I found a misspelled test label
and a helper that mishandles nulls.”

For the label: one obvious single-file edit, yes; existing proof covers
it, yes; no other behavior changes, yes; no separate review explanation,
yes. Correct it and record “two-minute: corrected empty-state test label.”
For the null helper: a fix needs a new regression case and may change
other callers, so the proof and behavior checks are no. Park it with its
location and return to the empty state. Its small line count does not
make it a two-minute fix.
