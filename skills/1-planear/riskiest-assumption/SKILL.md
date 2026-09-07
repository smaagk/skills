---
name: riskiest-assumption
description: "Riskiest assumption first — find the belief that, if false, kills the plan, and test it before building anything else. Use when a plan rests on unverified beliefs about a system, an API, a user, or a performance figure, or when choosing which spike to run first."
---

# Riskiest Assumption

Lean's test: every plan stands on beliefs, and one of them is the
**riskiest** — most likely to be false and most fatal if it is. Testing it
first is the cheapest possible failure; testing it last is the most
expensive.

## Steps

1. **List the assumptions.** Everything the plan treats as true without
   evidence: "the API returns X", "this query is fast enough", "the
   library supports Y", "users will do Z".
   _Done when_: each is written as a claim that could be false.

2. **Rank by likelihood × damage.** For each: how likely it is false
   (seen counter-evidence / unknown / well-established) and what happens
   to the plan if it is (dead / reworked / unchanged).
   _Done when_: the list is ordered and the top item is named.

3. **Kill or confirm the top one.** The cheapest test that could prove it
   false — a call, a query, a measurement, a spike — run before any
   building.
   _Done when_: the top assumption has evidence and a verdict, and the plan
   is updated or abandoned accordingly. Then take the next one.
