---
name: critical-path
description: "Critical path and the constraint — order a plan by what everything else waits on, and protect that step. Use when sequencing tasks, parallelising work across people or agents, or when a plan is late and it is unclear which step to rescue."
---

# Critical Path

Goldratt's rule: a system moves at the pace of its **constraint**, and time
saved anywhere else is not saved. In a plan the constraint is the longest
chain of dependent steps — the critical path — and the plan is only as
good as the care taken along it.

## Steps

1. **Draw the dependencies.** For each step, what it needs finished first —
   by surface (the file, the schema, the contract), not by narrative order.
   _Done when_: every step lists its prerequisites, and the list has been
   checked for a hidden shared surface (two steps touching the same file
   are dependent even if the plan says otherwise).

2. **Find the path.** The longest chain from now to the end state. Steps
   off it have slack; steps on it have none.
   _Done when_: the path is written as a chain and the slack of every other
   step is stated.

3. **Protect the path.** Start its first step first; put the best hands on
   it; give it no shared resources to wait on; keep off-path work from
   touching its surfaces. Parallelise only what is off the path and
   disjoint by surface.
   _Done when_: the plan's order starts the path immediately, and every
   parallel pair is disjoint by surface. When late, look only at the path.

## Example

Illustrative scenario; paths, commands, and results below are examples, not
artifacts or measurements from this repository.

**Request:** “Sequence an invoice export and its help page.”

The export contract takes 1 day; the service needs that contract and takes
2 days; the UI needs the service and takes 1 day. The help page takes
1 day independently, and release waits for both paths. The critical path is
contract → service → UI → release (4 days); the help page has 3 days of
slack. Start the contract first. The help page can run alongside it only
if it touches separate files and needs no time from the contract owner.
Finishing the help page early does not bring release forward.
