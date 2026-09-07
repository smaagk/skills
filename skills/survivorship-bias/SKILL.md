---
name: survivorship-bias
description: "Survivorship bias check for tests, seed data, and samples — the cases you see are the ones that came back. Use when designing test fixtures or seed data, judging coverage, reading metrics or logs, or deciding a feature is safe because nothing has failed."
---

# Survivorship Bias

Wald's bombers: the bullet holes you can see are on the planes that
returned; armour goes where the holes are **not**. Every fixture set, log
sample and "no one has complained" is a set of survivors.

## Steps

1. **Name the selection.** In one sentence: how did these cases get in front
   of you? (They passed CI; a user reported them; they exist in production;
   they were easy to write.)
   _Done when_: the filter is written as a sentence, not assumed.

2. **List what the filter drops.** For each mechanism in step 1, the class
   of case it cannot show you: silent failures, users who left, inputs that
   never reach the log line, states that crash before telemetry.
   _Done when_: at least one dropped class per mechanism, or an explicit
   "this filter drops nothing" with the reason.

3. **Put a case in each hole.** For every dropped class, one concrete
   fixture, test, or query that would surface it.
   _Done when_: each class from step 2 has a case with a locator, or is
   marked out of scope with the reason.
