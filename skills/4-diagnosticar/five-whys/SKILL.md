---
name: five-whys
description: "Five whys before recording a lesson — chase a recurring failure to a cause you can change, not a symptom you can describe. Use when a failure, hang, flaky test, or incident has happened more than once, or before writing a memory, runbook, or postmortem entry."
---

# Five Whys

Ohno's discipline: ask *why* until the answer is something you can change
tomorrow. A lesson that records the symptom ("tool X hangs on long runs")
teaches the next reader to expect it; a lesson that records the cause
teaches them to prevent it.

## Steps

1. **Write the symptom as observed.** One line, with count and context:
   what happened, how many times, under what conditions.
   _Done when_: the line has a number in it.

2. **Chain the whys.** Each answer must be a fact with a locator (a log
   line, a config value, a commit, a measured number), and each next *why*
   asks about that answer. Stop when the answer is a decision or default
   you control. Five is the usual depth, not a rule.
   _Done when_: the last link is something you can change, and every link
   above it has a locator. A link without one is a guess — test it or mark
   the chain as unfinished.

3. **Record the cause, keep the symptom.** The lesson states the
   changeable cause first, the symptom as the way to recognise it, and the
   change made or proposed.
   _Done when_: the recorded lesson leads with the cause.

## Example

Illustrative scenario; paths, commands, and results below are examples, not
artifacts or measurements from this repository.

**Request:** “Three integration jobs timed out waiting for their fixture
server. Should we double the timeout?”

Follow the evidence instead of the proposed fix:

| Why? | Observed answer and locator |
|---|---|
| Why did the jobs time out? | Server readiness never arrived; `logs/job-3.txt:80` |
| Why was the server not ready? | Bind failed with `EADDRINUSE`; `logs/job-3.txt:12` |
| Why was the port occupied? | A prior fixture process still owned it; `logs/ports.txt:2` |
| Why did it survive? | Cleanup is after an assertion that threw; `tests/server-fixture.ts:44` |

Stop at the cleanup placement, a default we control. Verify that a failing
test leaves the process alive, then move cleanup into a finally block and
verify process exit and port release. Increasing the timeout would only
wait longer for the same occupied port. If the process-owner evidence is
missing, the third link is a hypothesis: collect it before recording
“cleanup caused the hang” as a lesson.
