---
name: eat-the-frog
description: "Eat the frog — the task with the most unknowns opens the session, while context is clean. Use when ordering a session, a batch, or a day's list, or when the hardest item keeps sliding to the end."
---

# Eat the Frog

The **frog** is the item you least want to start: most unknowns, most
likely to need judgement, most likely to change the rest. It goes first,
because the resources it needs — clean context, full attention, room to
change course — are highest at the start and only fall.

## Steps

1. **Find the frog.** For each item: unknowns (things you would have to
   find out), and blast radius (how many other items change if this one
   surprises you). The frog maximises both.
   _Done when_: every item has both scores and one is named the frog.

2. **Start it first, fully.** No warm-up items, no "quick ones" before it.
   Work it until its first real surprise is resolved or it is done.
   _Done when_: the frog is done, or its surprise is written down and the
   rest of the list has been re-ordered in its light.

3. **Then the rest, easiest last.** The remaining items in descending
   unknowns, so the tail of the session holds only what needs little
   context.
   _Done when_: the order is written and the frog is not below position one.

## Example

Illustrative scenario; paths, commands, and results below are examples, not
artifacts or measurements from this repository.

**Request:** “Order today's work: tenant isolation, a loading label, and docs.”

On a 0–3 scale, tenant isolation has unknowns 3 / blast radius 3; docs
have 1 / 1; the loading label has 0 / 0. Tenant isolation is the frog.
Start with its cross-tenant request check, not the label as a warm-up.
Suppose that check reveals the cache key lacks a tenant component.
Resolve the key ownership question and record how it changes the plan;
then finish isolation before documentation and the label. The order is
based on uncertainty and downstream consequences, not simply which item
has the largest estimated line count.
