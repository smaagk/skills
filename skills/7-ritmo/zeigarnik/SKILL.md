---
name: zeigarnik
description: "Zeigarnik close — no turn or session ends with an unwritten intention; every open loop is written to the report or the parking list first. Use at the end of any turn, before a handoff, when context is filling, or when 'I'll do that later' has just been thought."
---

# Zeigarnik

Open loops occupy memory whether or not you work them, and an agent's
memory does not survive the session. So every intention is closed the
moment it forms: done, or written where it will be read. "Later" without
a locator is "never".

## Steps

1. **Sweep for open loops.** Before ending a turn: things you said you
   would do, questions you raised and did not answer, files touched and
   not verified, commands started and not read.
   _Done when_: the sweep is a list, even if empty.

2. **Close each loop one of three ways.** Do it now (if trivial), write
   it to the report's next-steps with what and where, or park it with a
   locator. Nothing stays in your head.
   _Done when_: every item from step 1 has one of the three dispositions.

3. **End on a state, not a promise.** The last lines of the turn describe
   what is true now; any "I will" has been converted into a written item.
   _Done when_: the closing text contains no future-tense commitment
   without a locator.

## Example

Illustrative scenario; paths, commands, and results below are examples, not
artifacts or measurements from this repository.

**Request:** “Close the session after updating the handbook search.”

“I'll check the build and fix the accent issue later” leaves two intentions
without state. Sweep the actual artifacts:

| Open loop | Disposition |
|---|---|
| Build job 812 started; result unread | Read its result and record the job link |
| Changed search index not verified | Run the agreed lookup-query check |
| Accent handling defect outside this change | File issue #73 with query, expected page, and reproducer |

If the first two checks pass, close with “build 812 and lookup check pass;
accent defect remains in #73.” If build 812 is still running, report the
change as awaiting that result and put the job locator and next action in
the handoff. Recording pending work closes the memory loop; it does not
make an unfinished build green or the delivery complete.
