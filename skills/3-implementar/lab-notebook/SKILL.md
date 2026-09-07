---
name: lab-notebook
description: "Lab notebook — record command, result, and moment as they happen, before knowing whether they matter. Use during debugging, experiments, spikes, migrations, or any session whose report will be written after the fact."
---

# Lab Notebook

A report written at the end is reconstructed, and reconstruction
attributes the second attempt's result to the first. The notebook is
written *during*: each entry the exact command, the exact result, the
time — dull, complete, and unedited.

## Steps

1. **Open the notebook before the first command.** A scratch file for the
   session, outside the shipping tree.
   _Done when_: the file exists with a header: goal, start time.

2. **One entry per action, as it happens.** Command or edit → captured
   result (not a summary) → timestamp → one line of what you concluded,
   if anything. Failures and dead ends included; they are the entries the
   report will most need.
   _Done when_: no command was run without an entry.

3. **Write the report from the notebook, not from memory.** Every claim
   in the report cites an entry. Discrepancies between memory and
   notebook are resolved in the notebook's favour.
   _Done when_: each result in the report traces to an entry, and the
   notebook is kept alongside the report or discarded deliberately.

## Example

Illustrative scenario; paths, commands, and results below are examples, not
artifacts or measurements from this repository.

**Request:** “Investigate why the export test fails only in one timezone.”

Create a notebook outside the delivery tree with the goal and start time.
Record entries as they happen, including the failed run:

```text
Goal: reproduce export date boundary. Started 2026-01-12T10:00:00Z.
10:01:00Z | TZ=UTC npm test -- export-date
Captured stdout: PASS export-date; Tests: 1 passed, 1 total
Conclusion: UTC does not reproduce.
10:02:00Z | TZ=America/Mexico_City npm test -- export-date
Captured stdout: FAIL export-date; Expected: 2026-01-01; Received: 2025-12-31
Conclusion: the configured timezone changes the observed day.
```

These are short illustrative outputs; retain the full actual output in a
real run. Cite the 10:02 entry in the report and file the notebook with it.
