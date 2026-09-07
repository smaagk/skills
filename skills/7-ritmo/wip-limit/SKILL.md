---
name: wip-limit
description: "WIP limit — a fixed maximum of open pieces (branches, worktrees, PRs, tasks); to open one, close one. Use when starting new work while other work is open, when orphaned branches or environments accumulate, or when nothing is finishing."
---

# WIP Limit

Kanban's rule: the number of pieces in flight has a ceiling, and the
ceiling is enforced by *stopping starting*. Work in progress is not
progress; it is inventory, and every open piece costs context, rebases,
and a chance to be forgotten.

## Steps

1. **Count what is open.** Every branch not merged, worktree not removed,
   PR not closed, task claimed and not done, environment or server left
   running. Each with its age.
   _Done when_: the inventory is listed with ages — including the ones you
   forgot, which is why the count is done by command, not memory.

2. **Set or read the ceiling.** The project's limit if it has one; if not,
   two pieces in flight per pair of hands, and the limit is written down
   for next time.
   _Done when_: the limit is a number.

3. **Over the limit: finish or kill before starting.** For each excess
   piece, one of: finish it, hand it off, or delete it with a note. No new
   piece opens until the count is at or under the ceiling.
   _Done when_: count ≤ limit, and each closed piece has its disposition
   recorded.
