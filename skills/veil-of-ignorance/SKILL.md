---
name: veil-of-ignorance
description: "Veil of ignorance for authorization rules — review the policy from every role without knowing which one you'll be. Use when writing or reviewing access control, row-level security, permission checks, data projections, or any rule that decides who sees or changes what."
---

# Veil of Ignorance

Rawls: design the rule without knowing which seat you will occupy. A policy
written from the seat of the person who requested it protects that seat.
The review walks every other seat, including the one that wants to abuse it.

## Steps

1. **Enumerate the seats.** Every role the rule touches, plus two that are
   always there: the anonymous caller and the legitimate user of a
   *different* tenant, team, or account.
   _Done when_: the list is written and includes both always-there seats.

2. **Sit in each one.** For each seat, the question is "what can I read,
   write, or infer that I should not?" — including inference from counts,
   error messages, timing, and ids that leak existence.
   _Done when_: every seat has an answer with the exact query, request, or
   input tried, and its result.

3. **Fix from the weakest seat.** Repair the seat with the worst finding
   first; re-run every seat after each repair, since a fix for one often
   opens another.
   _Done when_: every seat's answer is "nothing", each backed by a captured
   result.
