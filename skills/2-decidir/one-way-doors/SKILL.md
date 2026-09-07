---
name: one-way-doors
description: "One-way vs two-way doors — decide alone and fast when the action is reversible, stop and confirm when it is not. Use when about to act and unsure whether to ask, when a spec is silent, or when defining which actions in a project require confirmation."
---

# One-Way Doors

Bezos's cut: a **two-way door** is a decision you can walk back cheaply —
take it now, alone, and record it. A **one-way door** cannot be walked
back — stop, state the options, and confirm before opening it. The whole
skill is telling them apart quickly.

## The test

An action is a one-way door if any of these hold:

- it destroys or overwrites data or history that nothing else holds;
- it is visible to people outside the work (published, sent, deployed,
  merged to a shared branch);
- undoing it costs more than an hour or needs someone else's help;
- it changes a secret, a credential, or a production configuration.

Everything else is a two-way door.

## Steps

1. **Classify before acting.** Apply the test; write the verdict in one
   word next to the action.
   _Done when_: the verdict and the clause that decided it are written.

2. **Two-way: act, record.** Take the decision, note it where the work is
   reported, move on. No confirmation requested.

3. **One-way: stop, lay out, confirm.** State the action, what cannot be
   undone, the options with your pick first, and wait. Never open a one-way
   door on an inferred approval — approval for one door does not carry to
   the next.
   _Done when_: an explicit confirmation for this action exists, or the
   action is not taken.

## Project list

A project keeps its own list of one-way doors (branches, environments,
commands) beside this skill, so the test is never re-derived under
pressure. Absent a list, the test above is the list.

## Example

Illustrative scenario; paths, commands, and results below are examples, not
artifacts or measurements from this repository.

**Request:** “Prepare the migration; I have not authorized production execution.”

Classify creating a local migration file as two-way: the edit can be
reverted cheaply. Write and validate it, then record that choice.
Classify dropping the production column as one-way: it destroys values
unless another copy holds them and changes production state. Present the
concrete migration, the affected data, and the options: retain the column
for now, or approve its removal after verifying the backup and recovery
path. Stop before production execution. Preparing the file is complete;
permission to prepare it is not permission to run the destructive step.
