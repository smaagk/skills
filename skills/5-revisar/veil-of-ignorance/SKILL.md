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

**Request:** “The owner can download a document. Review everyone else's access.”

Policy: document 17 is private to its owner and the workspace administrator.
Probe `GET /documents/17` and nonexistent ID 999 with each identity:

| Seat | ID 17, observed | ID 999, observed | Verdict |
|---|---|---|---|
| Owner | 200 + file | 404 | Intended access |
| Administrator, same workspace | 200 + file | 404 | Intended access |
| Other member, same workspace | 404 | 404 | No difference in these responses |
| Member, different workspace | 403 “private document” | 404 | Leaks existence |
| Anonymous | 401 | 401 | Authentication required |

“No unauthorized download succeeded” misses the fourth row. Make forbidden
and missing IDs indistinguishable for that caller, then rerun every seat
so the owner still succeeds. Compare bodies, counts, and timing as separate
probes before claiming wider isolation. Equal status codes alone establish
only the status-code result, not absence of every inference channel.
