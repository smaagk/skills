---
name: frictionless-focus
description: "Frictionless focus for hands-on implementation — one unit, one proof, tangents parked, no question the repo can answer. Use when implementing from a frozen spec, issue, or work order, or when another skill hands a spec to a worker."
---

# Frictionless Focus

Design is frozen before this skill fires; what remains is the hands. *Friction*
is every stop that is not the work: a question the repo could answer, a tangent,
a reopened decision. *Focus* is one **unit** with one **proof**. Where the
design phase's rule is "if uncertain, ask", the hands' rule is **precedent**,
then record.

## Steps

1. **Frame the unit.** One line: what changes, the exact **proof** command
   (test, build, SQL script, screenshot) and the non-goals. A spec without a
   proof gets one from the nearest precedent — the spec or test beside the file
   you will touch — never from a question.
   _Done when_: the proof command is written down and has run once (red or
   green) before any edit.

2. **Read to the edit, not around it.** Open the files the unit touches and
   one **precedent**: the closest existing piece that already does what you are
   about to do. Copy its shape — naming, layer, error handling, test pattern.
   _Done when_: every edit has a `path:line` it lands on and a precedent it
   copies.

3. **Tracer bullet, then fill.** Land the thinnest end-to-end slice that moves
   the proof from red toward green, then widen: happy path, error, empty.
   Edits are surgical (/karpathy-guidelines §3): adjacent code stays as found.
   _Done when_: the proof is green from a fresh run and the output is captured.

4. **Park, don't chase.** Anything found outside the unit — dead code, a smell,
   a second bug, a better design — goes to the **parking lot** (`bd create`,
   or the report's Parked section when you cannot), one line each, and you
   return to the unit. The single exception is the anti-ossification valve: if
   the unit cannot be done without working around a wrong existing design,
   stop at that piece, report why, and hand back — no workaround.
   _Done when_: nothing outside the unit was edited; every discovery is parked
   or reported.

5. **Report, don't narrate.** Files changed · proof command and captured
   output · decisions taken by precedent (which precedent) · Parked ·
   Stopped-at (if any, in /sbar form). No progress story, no restated spec.
   _Done when_: a reviewer can re-run the proof from the report alone.

## Deciding without asking

When the spec is silent: repo precedent → the unit's non-goals (leave it out)
→ the smallest reversible choice. Record the choice in the report. Ask only
when all three hold — not inferable from the repo, materially different
behaviours, expensive to undo — and ask once, with the options laid out.

## Example

Illustrative scenario; paths, commands, and results below are examples, not
artifacts or measurements from this repository.

**Request:** “Implement the frozen attachment-list empty state. Keep the
agreed copy and do not redesign uploads.”

`npm test -- attachment-list` starts red: expected the empty message,
received a blank panel. The spec omits markup, but
`src/comment-list.ts:35` already uses the shared `EmptyState` component.
Reuse that precedent and record it instead of asking which component to use.

Two discoveries lead to different decisions:

| Evidence | Action |
|---|---|
| `src/upload-progress.ts:70` duplicates percentage formatting | Park it; the empty state does not depend on it |
| The list exposes both “loading” and “loaded with zero items” as `[]` | Stop at the missing state distinction if no canonical loading state exists |

In the second case, a timer that guesses when loading finished would hide
a design problem. Report that blocker with the red proof. If an existing
loading signal resolves it, use that signal and finish with a fresh green
run; no new design decision is needed.
