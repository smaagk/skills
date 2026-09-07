---
name: essentialism
description: "Essentialism — less, but better: of everything that could be done, do only the vital few, and say no to the rest on the record. Use when scoping a feature, a plan, a session, or a request that lists many things, or when a deliverable keeps growing."
---

# Essentialism

McKeown's discipline: almost everything is noise, a few things matter
disproportionately, and the work is *choosing* — not fitting it all in.
Two rules do the choosing. The **90% rule**: if a candidate is not a clear
yes, it is a no. **Minimalism** on what survives: the least that solves
the essential completely, not the most that fits.

## Steps

1. **Lay everything out.** Every candidate item the request, the plan, or
   your own instinct proposes — including the ones you assumed were
   obviously in.
   _Done when_: the list is written and nothing is "implied".

2. **Score against one criterion.** Write the single question that
   defines success for this work. Score each candidate 0–100 on how much
   it moves that answer. Below 90 is a no — not a maybe, not a later.
   _Done when_: every candidate has a score and the criterion is one
   sentence.

3. **Say no on the record.** Each no is listed with its score and one
   line of reason where the requester will read it. A silent cut is
   scope creep waiting to be re-requested; a recorded no is a decision.
   _Done when_: the no-list is in the report or the plan, not in your
   head.

4. **Build the least that solves the yes completely.** For each
   surviving item, the minimum implementation that fully meets the
   criterion — no options, flags, or generality the criterion did not
   ask for.
   _Done when_: each yes is met, and nothing was built for a no.

## Example

Illustrative scenario; paths, commands, and results below are examples, not
artifacts or measurements from this repository.

**Request:** “Propose the first release of a podcast editor: trimming,
transcripts, themes, and direct publishing.”

Criterion: “Can a producer remove a mistake and export a playable episode?”
Candidate scores are judgments against that criterion, not measured benefits:

| Candidate | Score | Scope decision |
|---|---:|---|
| Trim and export | 100 | Yes: remove a marked interval and verify playback |
| Transcript editing | 70 | No: useful navigation, but timestamps suffice here |
| Themes | 10 | No: does not change the audio result |
| Direct publishing | 60 | No: the producer can upload the exported file |

The tempting “smallest release” is a trim preview with no export. It fails
the criterion despite being smaller. Keep the complete trim-to-file path,
and record the three exclusions in the proposal. If the request instead
requires transcript-based editing for accessibility, reassess that item;
the original score does not justify silently dropping the requirement.
