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

## Example

Illustrative scenario; paths, commands, and results below are examples, not
artifacts or measurements from this repository.

**Request:** “Review GET /invoices/17 for cross-tenant access.”

Use invoice 17 belonging to resident A in tenant A. Try the same request
as its owner, another resident in A, an administrator in A, a user in B,
and an anonymous caller. Expected policy: owner and A's administrator can
read it; other authenticated callers receive the same not-found response
as for a nonexistent ID; anonymous callers receive an authentication
error. Suppose B receives an amount: fix that isolation failure first,
then rerun every seat. Also compare counts and error bodies for existing
and nonexistent IDs. Record exact requests and results; a hidden UI link
does not establish that the endpoint enforces the policy.
