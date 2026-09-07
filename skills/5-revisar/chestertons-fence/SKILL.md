---
name: chestertons-fence
description: "Chesterton's fence before removing or simplifying existing code — find who built it and why before the fence comes down. Use when a change deletes, bypasses, or collapses an existing guard, branch, flag, policy, migration, config key, or helper, or when a review proposes a judo move that removes one."
---

# Chesterton's Fence

A **fence** is any existing piece a change would remove or route around.
The rule: a fence comes down only after its **builder**'s reason is known —
and a reason that has **expired** is the only good reason to remove it.
"I can't see why it's there" is the starting condition, not a verdict.

## Steps

1. **Name the fence.** `path:line` range and, in one sentence, the behaviour
   that disappears if it goes (what input now takes a different path).
   _Done when_: both are written; a fence you cannot describe behaviourally
   you do not yet understand.

2. **Find the builder.** In this order, stopping at the first hit:
   the inline citation at the site (`#695`, `ADR-0051`, `audit PR #917` — the
   repo's convention) → `git log -S'<distinctive snippet>' --oneline -- <path>`
   and `git blame -L<a>,<b> <path>`, then the commit's PR/issue
   (`gh pr view <n>` / `gh issue view <n>`) → `docs/adr/`, `CONTEXT.md`, the
   wiki, `bd memories <keyword>`.
   _Done when_: the reason is quoted with its locator, or every source above
   is listed as checked with no hit.

3. **Verdict.** Exactly one:
   - **Holds** — the condition it guards still exists. Keep it; if the change
     needs it gone, the change is wrong, not the fence.
   - **Expired** — the condition no longer exists, and you can point at what
     removed it (a migration, a dropped feature, a later commit). Remove it.
   - **Unknown** — builder not found. Not a licence: remove only if the proof
     covers the fence's own scenario (the input from step 1 exercised, red →
     green unchanged) and the risk is reversible.
   _Done when_: the verdict names its evidence.

4. **Leave the marker.** At the site or in the commit: `removed <fence>; reason
   expired with <locator>` or `origin unknown; checked <sources>; proof
   <command>`. The next agent finds the why in place, not in a dead
   conversation.
   _Done when_: the marker cites a locator a stranger can open.
