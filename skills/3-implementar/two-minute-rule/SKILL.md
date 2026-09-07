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

**Request:** “While fixing a download button, I found two one-line changes.”

The first is “Dowload” → “Download” in the component already under test.
The current failing accessible-name assertion expects “Download”. The second
is adding `?? 0` to a shared size calculation to suppress a null error.

| Check | Button label | Shared calculation |
|---|---|---|
| One file, obvious edit, no design choice | Yes | No: does null mean zero or unknown? |
| Existing proof covers the change | Yes | No: needs a null-size case |
| Other cases keep their behavior | Yes | No: other callers share the helper |
| No separate review explanation needed | Yes | No: changes missing-data semantics |

Fix the label and record it as a two-minute edit. Park the calculation
with its location. Both edits occupy one line; only the first costs no
new behavioral decision.
