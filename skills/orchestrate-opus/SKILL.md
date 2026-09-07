---
name: orchestrate-opus
description: "Operating mode: Fable orchestrates and architects; Opus 5 implements via /opus-first; Codex serves as decorrelated code-review lens and mechanical worker; Fable reviews, ships, and supervises PR babysitting."
---

# Operating mode: Fable orchestrates, Opus implements

Fable is the orchestrator and architect. Opus 5 subagents (via /opus-first)
are the primary hands; Codex (via /codex-first) stays in the fleet as the
mechanical worker and — critically — as the decorrelated review lens.
Fable never types implementation code while a spec can be frozen; workers
never make a design decision or touch git/GitHub.

## Cycle

1. **Plan (Fable).** Decompose the task, make the design/architecture calls,
   freeze a spec per unit of work. Codebase legwork for the plan goes
   through /opus-research (Fable briefs, Opus scouts, Fable debriefs).
   Ambiguity is design work — resolve it here, never delegate it.

2. **Placement (Fable).** Before touching code, decide worktree vs. stay and
   state it in one line: worktree when parallel/dirty/risky, stay when serial
   and small.

3. **Route (Fable).** Per unit, pick the hand using /opus-first's route
   table: judgment-heavy / session-tools / parallel fan-out → Opus;
   mechanical bulk → Codex. State the route in one line.

4. **Implement (worker).** One frozen spec per run, following the invoked
   skill's prompt contract. Standard spec lines carry over from
   batch-conductor: the anti-ossification valve ("if the existing design is
   wrong, don't work around it — report and stop") and the megafile flag
   ("mark files >~800 lines, don't decompose them yourself").

5. **Review & correct (Fable — never skipped, never delegated).** The lens
   assignment is fixed regardless of route (see /batch-conductor Fase 3):
   - **Judge A / code lens** = GPT-6 Astra via `codex exec` read-only
     (resulting tree, no diff, no transcript; flat rate, effort `high`).
   - **Judge B / structure lens** = Fable or an Opus subagent (thermo-nuclear
     rubric, independent cross-model review).
   - **Spec lens** = Sonnet subagent (issue+spec+diff only).
   - **Security lens** = Fable personally.
   Decorrelation holds because the two judges are of different families, so
   at least one never shares a family with the hand that wrote the code.
   Run the gates yourself (focused tests, lint with the project's real
   config, build); worker reports are advertising, not proof. Iterate via
   SendMessage (Opus) or `codex exec resume` (Codex); after 2 failed rounds,
   take over and finish directly.

6. **Ship (Fable).** Commit, push, open the PR. All git/GitHub mutations are
   Fable-side, always.

7. **Babysit the PR (Fable supervises, workers fix).** Monitor CI and
   CodeRabbit; each actionable finding becomes a mini-spec routed back
   through step 3 (same route table — a mechanical CI fix goes to Codex even
   if Opus built the feature). Fable reviews and pushes every fix. Loop
   until merged.

## Batch mode

/batch-conductor composes with this mode unchanged: its lot machinery
(dependency map, hot-surface freezing, megafile detection, bitácora, rebase
discipline, economy table) is engine-agnostic. In Fase 2 replace /codex-first
with the route step above; in Fase 3 apply the flipped lens assignment. The
economy table gains one column: route chosen per issue (opus/codex) — it
feeds the next lot's routing.
