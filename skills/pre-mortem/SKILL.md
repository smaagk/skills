---
name: pre-mortem
description: "Pre-mortem before an irreversible step — assume it already failed and write how. Use before a merge to a release branch, a production deploy or migration, a data backfill, a config or secrets change, or any action with no cheap undo."
---

# Pre-mortem

Klein's exercise: it is next week, the change shipped, and it broke
something. Write the story of how. Narrative finds failures a checklist
cannot, because a checklist only holds what already failed once.

## Steps

1. **Set the scene.** One line: what ships, where, and what "broke" would
   look like to whoever notices first.
   _Done when_: the observer and the symptom are named.

2. **Write three obituaries.** Three distinct, specific stories of how it
   failed — different mechanisms, not three phrasings of one. Each names the
   trigger, the first symptom, and how long until someone notices.
   _Done when_: three stories with three different mechanisms.

3. **Price each one.** Likelihood (seen it before / plausible / far-fetched)
   and cost to undo (minutes / hours / data loss).
   _Done when_: every story has both labels.

4. **Act on the top of the table.** For each story that is at least
   plausible AND costs more than minutes to undo: a check you run now, a
   guard you add, or a rollback you rehearse — with the command.
   _Done when_: each such story has a mitigation with a command, or an
   explicit acceptance of the risk with the reason. Then proceed.
