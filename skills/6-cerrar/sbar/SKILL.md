---
name: sbar
description: "SBAR handoff — Situation, Background, Assessment, Recommendation — for passing work between agents or sessions. Use when handing off, escalating or asking for help, reporting a stop, or persisting state before a session may die."
---

# SBAR

The nursing shift-change protocol, applied to agents: the receiver acts
without opening your transcript. Four headings, this order, literal.

**Situation** — one sentence, present tense, observable: issue/branch, state
of the proof (red/green, which command), what is blocked. No history.

**Background** — only what the receiver lacks and needs to act: the spec or
issue locator, what was tried and its outcome (command → result), the
constraints in force (frozen surfaces, shared resources, non-goals). Every
fact carries a locator: `path:line`, commit, command, URL.

**Assessment** — your judgement, separated from the facts: the likely cause
or state, your confidence, and what you do not know. A guess labelled as a
guess is useful; a guess dressed as a fact is the failure this section
prevents.

**Recommendation** — the one next action you propose. If a decision is
needed from the receiver, frame it as options with your pick first. One ask,
not a list.

## Where it goes

`gt handoff -m`, `gt mail send … -s "HELP: …"`, `bd update <id> --notes`
before a session may die, a SendMessage to a teammate, and the Stopped-at
section of an implementation report.

_Done when_: read it as the receiver — can they act from these four blocks
alone, and does every fact in Background open to something? A block that
fails either test is rewritten, not padded.
