---
name: batching
description: "Batching — group actions of the same kind and issue them together: all reads, then all edits, then all checks. Use when alternating between reading, editing, and running, when several independent lookups are needed, or when a tool is being called one item at a time."
---

# Batching

Switching kinds of action costs more than the actions. Reads that could
have been one sweep become ten round-trips; checks run one at a time
serialise what was independent. The discipline is to see the batch
before issuing the first item.

## Steps

1. **Group before acting.** List what the step needs by kind: things to
   read, things to change, things to run. Mark the dependencies — which
   items need another's result first.
   _Done when_: the lists exist and the dependent items are flagged.

2. **Issue each independent group at once.** All reads without
   dependencies in one round; all edits in one round; all checks in one
   round. Only dependent items wait.
   _Done when_: no independent item was issued alone after another of its
   kind.

3. **Read results as a set.** Consume the batch's results together before
   deciding the next batch; do not react to the first result while the
   rest are pending.
   _Done when_: the next batch is planned from the full set of results.
