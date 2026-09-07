---
name: opus-research
description: "Route code research to Opus 5 scouts via the Agent tool; Fable briefs, debriefs, decides. Use when answering means reading across several files — where does X live, how does Y work, what a flow touches UI→service→DB, what a plan/spec/grill must account for — or when another skill needs codebase legwork. A single-fact lookup in a known file stays in Fable."
---

# Opus Research

Fable sessions only. Fable never reads the codebase at breadth itself: it
briefs a scout, the scout reads, Fable debriefs. The scout is an Opus 5
subagent spawned with the Agent tool — same harness, read-only hands.

Rationale: file dumps are the fastest way to fill Fable's context with
material it will never use again. A scout burns its own context on the
reading and returns the map; Fable keeps the conclusion and the decisions.
Opus (not Codex) scouts because it inherits CLAUDE.md, repo skills, path
aliases and the wiki conventions — a scout that already knows what
`PropertyContextService` is needs a thinner brief and cites better.

## Route

Scout (this skill):

- locating: where X lives, every caller/consumer of Y, the files a task
  will touch
- understanding: how a feature works, one flow traced UI → service → RLS/DB
- inventories: every pattern a new piece must follow, every place a
  contract is consumed
- legwork for a plan, spec, grill, wayfinder ticket, or wiki page
- anything where raw reading ≫ the answer

Keep in Fable:

- a single-fact lookup where the file, symbol or value is already known:
  one grep, one read
- opening a scout's cited lines to verify them — that IS the debrief
- synthesis, judgment, decisions, and the answer to the user

## Brief

Agent tool, one frozen brief per scout — `model: "opus"`, no `isolation`
(scouts don't write). Two shapes:

- **sweep** — `subagent_type: "Explore"`: breadth — locate, inventory.
  State the breadth ("very thorough" when naming conventions vary).
- **trace** — `subagent_type: "general-purpose"`: depth — one flow or one
  module end-to-end; may run read-only commands (`git log -S`, `SELECT`
  against the local DB).

The brief (scouts start fresh — no conversation inheritance):

1. **Question + what it feeds** — "this feeds a spec for X" tells the
   scout what matters.
2. **Terrain** — entry points Fable already knows (paths, symbols, table
   names) and the lens.
3. **Found means** — the completion criterion, checkable and exhaustive:
   "every caller of `fn` listed", "every table the flow touches, with its
   RLS policy", "every component rendering `unit_status`". Never
   "understand X".
4. **Citations** — every claim carries `path:line`; without a citation it
   is not a claim, it is noise. Unverifiable → open question, never a guess.
5. **Read-only** — no edits, no git mutations, no `db:reset`, no touching
   running dev servers or emulators.
6. **Report shape** — executive summary (≤4 sentences) · findings by area,
   cited · numbered claims list · open questions · ≈1000-word cap. Name the
   repo skill to load when the terrain has one (`/supabase-rls`,
   `/habitalis-ui`, `/mobile-data-access-foundation`, …).

Fan out when the question spans layers: one scout per lens, in parallel;
Fable merges.

| Lens   | Terrain                                                                                                                  |
| ------ | ------------------------------------------------------------------------------------------------------------------------ |
| `ui`   | `apps/web/**`, `libs/features/**`, `apps/mobile/app/**` — components, templates, signals, routing, guards                |
| `data` | `libs/shared/data-access/**`, `libs/mobile/data-access/**`, `libs/shared/contracts/**` — services, hooks, Supabase, DTOs |
| `db`   | `supabase/migrations/**`, `supabase/functions/**` — tables, RLS, RPCs, triggers, edge functions                          |
| `flow` | one path end-to-end UI → service → DB, cross-referenced with `docs/` and `wiki/`                                         |

## Debrief (Fable, always)

- Open the cited line of every claim a decision will rest on. A scout's
  claim is advisory until Fable has seen the line.
- Gaps (missing citation, "probably", a lens not covered) go back to the
  same scout via SendMessage — context intact, cheaper than a respawn.
  After 2 rounds, close the gap yourself.
- Done when every question in the brief has a cited answer or an explicit
  open question.
- Persist only when something downstream reads it: `.claude/explorations/`
  for a plan, the **Investigación** field of a `validated-*` decision page,
  a wiki page via /wiki-ingest. Otherwise the debrief lives in the spec or
  the answer.

## Economics

Win = Fable's context stays clean and sweeps run in parallel — not token
savings; Opus is metered. Don't route one-grep questions here, and don't
ping-pong trivia through a scout.
