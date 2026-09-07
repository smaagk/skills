---
name: rolling-wave
description: "Rolling-wave planning under fog of war — detail only the next step, keep the rest as milestones with checks. Use when a plan is being written in full detail beyond what is known, when later steps depend on what earlier ones will reveal, or when a long plan keeps being rewritten."
---

# Rolling Wave

Beyond the next step is **fog of war**: detail written there is fiction
that will be rewritten, and worse, it pulls attention forward before the
current step is done. So the wave: the next step in full, the rest as
milestones each with a check, and the plan re-detailed after every step
lands.

## Steps

1. **Fix the milestones.** The end state and the few intermediate states
   between here and there, each with the check that proves it reached. No
   how, only what.
   _Done when_: every milestone has a check and none has a method.

2. **Detail one wave.** Only the work up to the next milestone: files,
   commands, order, proof. Nothing past it.
   _Done when_: the next milestone's check can be run at the end of the
   wave, and no later milestone has been detailed.

3. **Land, then re-plan.** After the wave, re-read the milestones against
   what the wave revealed: merge, split, or reorder them; then detail the
   next wave.
   _Done when_: the milestone list is updated with a note of what changed
   and why, before the next wave is written.

## Example

Illustrative scenario; paths, commands, and results below are examples, not
artifacts or measurements from this repository.

**Request:** “Plan an importer for sensor archives we have not inspected.”

Milestones: understand supported formats (sample inventory complete),
preserve readings (reconciliation passes), expose them to users (acceptance
check passes). Detail only the inventory wave: read each supplied sample's
header and rows, group formats, and check every sample against the inventory.

Suppose it reveals:

```text
samples/a.csv: timestamp,temperature_c
samples/b.csv: recorded_at,temperature_f
```

A detailed plan for “rename the timestamp field and copy temperatures” would
already be wrong. Split the reconciliation milestone by schema and require
known equivalent temperatures to converge. Now detail the conversion wave.
If a later archive introduces a third schema, reopen the inventory check
before extending conversion; the milestone's proof, not its place in the
original plan, determines whether it has been reached.
