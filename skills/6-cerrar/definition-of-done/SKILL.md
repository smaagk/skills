---
name: definition-of-done
description: "Definition of done — one checklist, kept in one file, that says what finished means in this project; every closing skill points at it. Use when closing any unit of work, when 'done' is disputed, or when a project has no written definition."
---

# Definition of Done

Scrum's single source of truth for "finished". Its value is that it lives
in **one place** — a project file — so that every skill, template and
review that would otherwise restate it points there instead, and changing
what done means is a one-line edit.

## The file

`DEFINITION_OF_DONE.md` at the project root (or wherever the project keeps
its agent docs). Flat checklist, each line checkable by command or by
looking, grouped: code (lint, format, tests, build), evidence (screens,
logs), tracking (issue state, notes), hygiene (branches, environments,
temp files). No prose.

## Steps

1. **Read or create.** Open the file. If absent, write it from what the
   project already demands in scattered places (contributing docs, CI
   config, review templates), and delete the scattered copies or replace
   them with a pointer.
   _Done when_: the file exists and no other file restates its lines.

2. **Run every line.** Each line executed or inspected, with its result
   captured. A line that cannot be checked is rewritten until it can, or
   removed.
   _Done when_: every line has a pass, or a fail with what remains.

3. **Close only on all-pass.** A unit with a failing line is not done;
   it is "done except <line>", reported that way.
   _Done when_: the report states all-pass, or names the failing lines.

## Example

Illustrative scenario; paths, commands, and results below are examples, not
artifacts or measurements from this repository.

**Request:** “CI is green. Can we close the keyboard-navigation change?”

The repo disagrees with itself:

| Source | Requirement | Evidence of authority |
|---|---|---|
| PR template | Unit tests pass | Old copy, last updated before accessibility policy |
| CONTRIBUTING.md | Unit tests and keyboard walkthrough pass | Current policy, added by PR #64 |
| CI | Unit tests pass | Keyboard walkthrough is explicitly manual in PR #64 |

Green CI satisfies only part of the current policy. Consolidate both
checks in `DEFINITION_OF_DONE.md`: `npm test -- navigation`, plus open the
menu by keyboard, reach each item, press Escape, and verify focus returns
to the trigger. Replace duplicated criteria in the template and contributing
docs with a pointer; keep CI executing its automated check.

Suppose Escape loses focus: report the failed walkthrough and leave the
change open. If the policies' authority were unresolved, surface that
specific conflict rather than choosing the shortest checklist. One source
of truth cannot be created by quietly discarding a live requirement.
