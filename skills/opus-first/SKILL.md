---
name: opus-first
description: "Route implementation work to Opus 5 subagents via the Agent tool; Fable specs, reviews, verifies. Use when implementation needs session tools/MCP, judgment-heavy code (contracts, RLS, UX), or parallel worktree fan-out — or when Codex is down/rate-limited. Mechanical bulk still routes to /codex-first."
---

# Opus First

Fable sessions only. The implementer is an Opus 5 subagent spawned with the
Agent tool — same harness, different hands.

Rationale: unlike Codex, an Opus subagent inherits the harness — CLAUDE.md,
repo skills (habitalis-ui, supabase-rls, data-access-service…), path aliases,
and session MCP (browser, angular-cli). Specs get thinner because the
environment carries context Codex had to be told. Orchestration is native:
worktree isolation, background runs with completion notifications, and
follow-up iteration via SendMessage with the agent's context intact. The
trade: Opus tokens are metered — this is a quality/integration play, not a
cost play. Route accordingly.

## Route

Delegate to Opus (this skill):

- judgment-heavy implementation: shared contracts, RLS/multi-tenant surfaces,
  UX flows, API shape decisions baked into code
- cross-cutting refactors where writing an exhaustive spec would cost as much
  as implementing
- work needing session tools mid-implementation: MCP browser evidence,
  angular-cli MCP, reading its own screenshots
- parallel fan-out across worktrees (2+ independent issues at once)
- fallback when Codex is down, rate-limited, or looping

Delegate to Codex (via /codex-first — still the economic default):

- mechanical implementation from a frozen spec; repetitive migrations
- coverage fills, dependency bumps, CI fixes, scripts/tooling
- never code research — that is /opus-research (Opus scouts, Fable
  debriefs)

Keep in Fable:

- design, architecture, naming, scope — ambiguity is design work
- tiny edits (~<20 lines, single obvious change) — delegation overhead loses
- destructive/irreversible ops, releases, pushes, ALL git/GitHub mutations
- review of any worker's output — never delegated, never skipped

## Invoke

Agent tool, one frozen spec per agent:

- `model: "opus"`, `subagent_type: "general-purpose"`
- `isolation: "worktree"` when tasks run in parallel, the checkout is dirty,
  or the change is risky; omit for small serial work on the current branch
- background by default; the completion notification arrives on its own —
  never poll, never fabricate a pending result
- worktrees need a REAL `npm ci` (symlinked node_modules breaks jest/TestBed
  and poisons running dev servers — NG0203)

Prompt contract (subagents start fresh — no conversation inheritance): goal,
exact repo paths, constraints ("don't touch X"), non-goals, proof expected
(exact test command), output shape ("report files changed + test output").
Thinner than a Codex spec — skip what CLAUDE.md and repo skills already say;
DO name which repo skills to load (e.g. "load /data-access-service before
writing the service").

Shared resources stay Fable's: if the environment has global state (one DB
container, one emulator), forbid the agent from touching it ("do NOT run
db:reset") and run those steps serially yourself.

## Follow-ups

Iterate via SendMessage to the same agent — its context is intact, cheaper
and better than a fresh spawn. After 2 failed rounds, take over and finish
directly.

## Verify (Fable, always)

- `git status -sb` + read the full diff; judge like a contributor PR
- run focused tests yourself or demand proof output; agent claims are advisory
- decorrelation: hand and orchestrator are both Anthropic here, so the code
  lens goes to Codex read-only (flat rate, GPT error family) — see
  /orchestrate-opus for the full lens assignment
- normal closeout still applies: /code-review before ship

## Economics

Win = parallel throughput, thinner specs, same-harness fidelity, session-tool
access — not token savings. Don't route mechanical bulk here; that's what
/codex-first is for. Don't ping-pong trivia through delegation.
