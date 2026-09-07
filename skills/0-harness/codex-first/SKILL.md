---
name: codex-first
description: "Route implementation work to Codex CLI; Claude specs, reviews, verifies."
---

# Codex First

Claude Code sessions only. Codex/other harnesses: skip; never self-delegate.

Rationale: Claude (Fable/Opus) tokens metered + expensive; Codex flat-rate. GPT-6 Astra (`gpt-6-astra`, house model since 2026-09-07) is usually the better and faster model at writing/implementing code; Claude wins at ergonomics — judgment, design, spec-writing, review, orchestration. So Codex types, Claude thinks and verifies.

## Route

Delegate to Codex (default for hands-on work):

- implementation from a frozen spec; refactors; mechanical migrations
- bug fixes with known repro; test writing; coverage fills
- CI fixes, dependency bumps, scripts/tooling
- bulk codebase exploration where raw reading ≫ the answer

Keep in Claude:

- design, API design, architecture, naming, UX judgment
- tasks where writing the spec IS the work (ambiguity = design)
- tiny edits (~<20 lines, single obvious change) — delegation overhead loses
- anything needing session tools: MCP (browser/computer-use/chronicle), 1Password, secrets
- destructive/irreversible ops, releases, pushes, GitHub mutations — Claude-side per git rules
- review of Codex output — never delegated, never skipped

Mixed task: Claude designs first, freezes spec, delegates build-out.
Heuristic: prompt reads as a work order → delegate; writing it forces decisions → design, Claude.
Portfolio/multi-repo work: `$maintainer-orchestrator` instead.

## Invoke

Prompt via temp file, never inline quoting:

```bash
P=$(mktemp); cat >"$P" <<'EOF'
<goal, repo + key paths, constraints ("don't touch X"), non-goals, proof expected, output shape>
EOF
codex exec --yolo -C <repo> \
  -m gpt-6-astra \
  -c model_reasoning_effort="high" \
  -o /tmp/codex-<slug>.md - <"$P" 2>/tmp/codex-<slug>.err.log
```

- `-m gpt-6-astra` and `-c model_reasoning_effort=...` are BOTH explicit on purpose: `~/.codex/config.toml` is the user's interactive profile (as of 2026-09-07: `gpt-6-astra` at `model_reasoning_effort = "max"`) and can change without notice. Omitting the effort flag inherits that profile — today that means every delegated run at `max`, the slowest and most expensive level. Astra accepts `low` | `medium` | `high` | `xhigh` | `max` | `ultra`; `high` is the default here, `xhigh` for hard problems.
- Lower efforts for bounded work (explorer/worker `low`/`medium`) are an untested hypothesis in this repo: the only measured doctrine is spec-frozen → `xhigh` (lote licitaciones, 10/10). Don't lower by default; if trying it, record the effort per run so /batch-conductor's economy table can compare.
- `--yolo` is the house default; Codex may run commands/tests freely. Keep prompts scoped to the target repo.
- plain `codex`, no `command` prefix — permission allow rules match on the `codex` prefix; run the prompt-file write and the `codex exec` call as separate shell invocations for the same reason. If not on PATH: `fnm exec --using default -- codex`
- stderr goes to a per-run log, never `/dev/null`: it carries the live progress (agent narration + `exec` blocks with command, output, exit code), while stdout carries only the final message. Costs zero context until read. Don't read it by default; `tail -n 40 /tmp/codex-<slug>.err.log` only to report progress on a long run or to debug a failure. The user can follow it from their terminal with `! tail -f /tmp/codex-<slug>.err.log`.
- read `-o` file for the result; don't parse the JSONL stream
- long runs: Bash run_in_background, read `-o` file on exit; don't kill quiet runs <30 min
- parallel independent tasks OK: separate repos/dirs, separate `<slug>` (so separate `-o` and `.err.log` files)
- outside a git repo add `--skip-git-repo-check`

Follow-up fixes — cheaper than fresh runs, keeps context. `resume` has no `-C`/`--yolo`: run from the repo dir, spell the long flag:

```bash
(cd <repo> && codex exec resume --last \
  --dangerously-bypass-approvals-and-sandbox \
  -m gpt-6-astra \
  -o /tmp/codex-<slug>.md - <"$P2" 2>>/tmp/codex-<slug>.err.log)
```

## Prompt contract

Codex starts with zero session context. First line of every prompt: `Read
.claude/skills/frictionless-focus/SKILL.md and follow its Steps.` Then: goal, exact repo/paths, constraints, non-goals, proof expected (exact test command), output shape ("report files changed + test output"). Spec quality decides success.

## Verify (Claude, always)

- `git status -sb` + read the full diff; judge like a contributor PR
- run focused tests yourself or demand proof output; Codex claims are advisory
- iterate via resume; after 2 failed rounds, take over and do it directly
- normal closeout still applies: `$autoreview` before ship

## Economics

Win = generation + exploration tokens moved to Codex; Claude spends only on spec + diff review. Don't ping-pong trivia through delegation; don't re-read what Codex already summarized.
