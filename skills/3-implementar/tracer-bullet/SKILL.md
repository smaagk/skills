---
name: tracer-bullet
description: "Tracer bullet — the thinnest end-to-end slice that stays, to prove the path before filling it in. Use when starting a feature that crosses layers, integrating a new system, or when a plan builds one layer completely before touching the next."
---

# Tracer Bullet

The Pragmatic Programmer's alternative to the spike: a **tracer** goes all
the way through — UI to storage, caller to callee, input to output — with
the minimum in every layer, and it *stays*. It is not a prototype; it is
the first real version, thin enough to see where it lands.

## Steps

1. **Pick the path.** One concrete input and the output it must produce at
   the far end, naming every layer it crosses.
   _Done when_: the input, the output, and the layers are listed.

2. **Land the thinnest slice.** The minimum in each layer for that one
   input: hard-coded where allowed, no branches, no error paths, but real
   code in real places, with one test that drives the input to the output.
   _Done when_: the test passes end to end on the shipping branch.

3. **Widen from the tracer.** Add inputs, branches, errors, empty states,
   each as its own change, each extending the tracer's test.
   _Done when_: every case in the plan is reached by extending the tracer,
   and no layer was rebuilt from scratch.

## Example

Illustrative scenario; paths, commands, and results below are examples, not
artifacts or measurements from this repository.

**Request:** “Build a note form that saves and reloads its contents.”

Tracer: enter “Buy milk” → form → client → endpoint → storage → returned
ID → reload that ID and display “Buy milk”. Use real storage in the test
environment and retain the required access checks. One acceptance test
submits, reloads, and compares the text.

A form that displays “Saved” after a mocked response can pass a UI test
while this tracer fails. Suppose the reload returns “not found”: resolve
the ID or persistence boundary before adding tags, attachments, or rich
text. Those features would only widen an unproven path.

Once reload passes, this implementation stays; extend it with validation,
network errors, and planned fields. If the only question is whether a
storage SDK works at all and the code will be discarded, use a spike
instead. Keeping the code and proving the full path distinguish the tracer.
