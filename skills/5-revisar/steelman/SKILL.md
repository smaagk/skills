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

## Example

Illustrative scenario; paths, commands, and results below are examples, not
artifacts or measurements from this repository.

**Request:** “The reviewer says this cache is unsafe, but it clears on logout.”

Strong version: “A user can switch tenants without logging out. A cache
key containing only the invoice ID could then reuse the previous tenant's
result.” Exercise that scenario with two tenants sharing a local invoice
ID: fetch in A, switch to B, then fetch again. If A's data appears, the
finding holds despite the logout behavior. Scope the key by tenant and
verify the transition again. Reply with the scenario, captured failing
result, and passing regression. If isolation already holds, rebut with
that same scenario's evidence rather than only citing logout cleanup.
