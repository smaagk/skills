---
name: interruption-marker
description: "Interruption marker — before attending an interruption, write where you are and the exact next step, so you return without redoing. Use when a message, question, or notification arrives mid-task, or when switching tasks under pressure."
---

# Interruption Marker

The surgeon's practice: before looking up, mark the place. The cost of an
interruption is not the interruption; it is the re-orientation after it,
and a one-line marker removes most of it.

## Steps

1. **Mark before you look.** One line: current unit, the step you are in,
   the exact next action (command or edit), and what you were about to
   verify.
   _Done when_: the line is written before the interruption is read.

2. **Attend, bounded.** Handle the interruption to the point where it can
   wait or is done; anything it spawns is parked, not started.
   _Done when_: the interruption has a disposition: done, parked, or
   handed off.

3. **Return by the marker.** Re-read the line, run the "next action" from
   it — not from memory of what you think you were doing.
   _Done when_: the next action from the marker has been executed.

## Example

Illustrative scenario; paths, commands, and results below are examples, not
artifacts or measurements from this repository.

**Request:** “Answer a status question halfway through a failing parser test.”

“Resume parser work” is too vague: the edit is already made, but its effect
has not been checked. Write the boundary precisely before switching:

```text
CSV quoting; src/parser.ts:61 escape handling edited, not verified; next: npm test -- quoted-field; check a quoted comma stays in one field.
```

After answering status, run that command. The next action is verification,
not making the same edit again or starting the next parser case. If the
status question uncovers an unrelated build warning, park its log locator
before returning.

If someone changes the parser while you are away, the marker identifies
the intended boundary but is now stale: inspect that diff, then run the
proof against the current file. A marker saves reorientation; it does not
make an old workspace snapshot authoritative.
