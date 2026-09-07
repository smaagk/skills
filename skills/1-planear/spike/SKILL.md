---
name: spike
description: "Spike — a timeboxed, throwaway investigation that answers one question with evidence. Use when a plan is blocked on 'can this work', 'how does this behave', or 'which option', when an estimate cannot be made without trying, or when code is being written to learn rather than to ship."
---

# Spike

Extreme Programming's tool for the unknown: a **spike** answers one
question, inside a **timebox**, with code that is **thrown away**. The
deliverable is the answer; keeping the code is the most common way to
ruin a spike, because code written to learn was not written to live.

## Steps

1. **Write the question.** One sentence with a yes/no or a pick-one shape,
   and what evidence would settle it (an output, a measurement, a working
   call). "Explore X" is not a question.
   _Done when_: the question and its settling evidence are written.

2. **Set the timebox.** A fixed budget — hours, or attempts — and the
   fallback decision if the box runs out unanswered (assume no; pick the
   incumbent; escalate).
   _Done when_: the budget and the fallback are written before starting.

3. **Go straight at the evidence.** Skip tests, structure, naming, error
   handling: the shortest path to the settling evidence, in a scratch
   location, never on the shipping branch.
   _Done when_: the evidence is captured, or the timebox is out.

4. **Answer and discard.** Record the answer, the evidence, and what was
   learned that the plan did not know; delete the code. Anything worth
   keeping is rewritten on the shipping branch with tests, as its own
   piece of work.
   _Done when_: the answer is filed where the plan reads it, and the spike
   code is gone.
