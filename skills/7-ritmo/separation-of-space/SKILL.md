---
name: separation-of-space
description: "Separation of space — one space, one kind of work: experiments, shipping code, notes, and design each live in their own place, and nothing crosses without a deliberate move. Use when starting work that mixes kinds (a spike beside a feature, a design question mid-implementation), when a tree has both throwaway and shipping changes, or when setting up a session."
---

# Separation of Space

The brain learns what a place is for; so does a repository. A spike in
the shipping tree becomes shipping code; a design argument in an
implementation session reopens the design. Give each kind of work its
own **space** — branch, worktree, directory, session — and let artifacts
cross only by a deliberate, named move.

## The spaces

- **Shipping** — the branch that will merge: real code, real tests, no
  experiments.
- **Scratch** — throwaway code, spikes, measurements: outside the
  shipping tree, deletable without loss.
- **Notes** — the lab notebook, findings, decisions: outside both, kept
  or filed at the end.
- **Design** — where questions of what and why are settled: a plan, a
  spec, a separate conversation — never the implementation session.

## Steps

1. **Name the kinds in play.** Which of the four does this session
   involve, and where each one lives, by path or branch.
   _Done when_: every kind has an address.

2. **Work each kind in its space only.** A design question that arises in
   shipping space is written to notes and settled in design space, not
   answered inline. Experiment code is written in scratch, never
   "temporarily" in shipping.
   _Done when_: at any moment, the current file's space matches the kind
   of work being done.

3. **Cross by a named move.** Scratch → shipping is a rewrite with tests,
   as its own change. Notes → report is a citation. Design → shipping is
   a frozen spec. Never a copy, a merge, or a "clean up later".
   _Done when_: each crossing is recorded as which move it was.

4. **Leave each space as its kind.** At close: scratch deleted or
   deliberately kept and labelled, notes filed, shipping tree containing
   only shipping changes.
   _Done when_: `git status` on shipping shows only shipping work, and
   scratch and notes each have a disposition.
