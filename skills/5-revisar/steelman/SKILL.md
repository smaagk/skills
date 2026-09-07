---
name: steelman
description: "Steelman a finding before rebutting it — state the strongest version of a review comment, objection, or bug report before deciding it is wrong. Use when triaging reviewer or automated feedback, answering a bug report you believe is invalid, or disagreeing with a spec."
---

# Steelman

Before "this is invalid", write the version of the objection its author
would nod at — stronger than they wrote it. A rebuttal that only beats the
weak wording wins nothing; the valid point underneath ships in the next
round anyway, with interest.

## Steps

1. **Rewrite the objection at full strength.** Two sentences, in your
   words, with the concrete case that would make it right. If you cannot
   find that case, you do not understand the objection yet — read the cited
   line again.
   _Done when_: the strong version names a concrete input or scenario.

2. **Test the strong version, not the weak one.** Run the scenario, read
   the line, check the spec.
   _Done when_: the result is captured.

3. **Answer the strong version.** Either: it holds — fix it and say what
   changed; or: it fails — say why, citing the result from step 2 and the
   strong version you tested, so the author sees you argued their best case.
   _Done when_: the reply quotes the strong version and the evidence.
