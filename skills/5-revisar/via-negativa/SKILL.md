---
name: via-negativa
description: "Via negativa for refactors and design — the first proposal is what to remove, and only then what to add. Use when refactoring, simplifying, reviewing for structure, or when a design adds a layer, a flag, a mode, or an abstraction."
---

# Via Negativa

Improvement by subtraction (Taleb). Adding is easy to justify and hard to
undo; removing is the reverse. So the order of proposals is fixed: what
disappears, then what changes, and only then what is added.

## Steps

1. **List what could disappear.** Branches, flags, modes, wrappers, layers,
   parameters, config keys, dead paths that the change makes unnecessary or
   that were never necessary.
   _Done when_: every candidate has a `path:line` and the behaviour that
   would remain identical without it.

2. **Remove and prove.** Take out each candidate the proof allows (the
   existing tests plus the candidate's own scenario), one at a time.
   _Done when_: each removal is green, or the candidate is marked "kept:
   <reason>".

3. **Only now, add.** Whatever the change still needs after subtraction.
   Each addition must name the concept it introduces and why no removal
   covered it.
   _Done when_: the diff's additions are each justified against step 1, and
   the net line count is reported.

## Example

Illustrative scenario; paths, commands, and results below are examples, not
artifacts or measurements from this repository.

**Request:** “Simplify the export service without changing its API.”

Candidates: `src/export.ts:18`, a wrapper that only forwards to the
serializer; `src/export.ts:42`, two identical branches; and
`src/export.ts:70`, a retry guard. Remove the wrapper and collapse the
branches one at a time, rerunning the export fixtures after each. Keep
the retry guard because the transient-failure case still needs it. Only
then consider additions: none are required if the direct serializer call
preserves the API. Report the retained guard and the net change, for
example −24 lines, alongside the passing checks. A smaller diff alone
would not justify removing retry behavior.
