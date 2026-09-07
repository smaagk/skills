---
name: maker-manager-schedule
description: "Maker vs manager schedule — separate blocks for deep work (design, review) and for supervision (monitors, CI, queues); never interleave them. Use when orchestrating while also designing or reviewing, when a monitor is polled mid-thought, or when review quality is dropping."
---

# Maker / Manager Schedule

Paul Graham's split: makers need unbroken blocks, managers run on
intervals. An orchestrator is both, and the failure is doing them at
once — reviewing a diff with half the attention on a check that will
finish in a minute anyway.

## Steps

1. **Sort the pending work by kind.** Maker: design, spec, review,
   debugging. Manager: watching CI, queues, monitors, answering status.
   _Done when_: every pending item is labelled maker or manager.

2. **Run maker work in a closed block.** Start it only when nothing
   requires a reaction in the next block's length; background monitors
   notify — they are not polled. The block ends at the item's completion
   criterion, not at the first notification.
   _Done when_: the maker item is done and no monitor was read during it.

3. **Run manager work as a sweep.** Between blocks, read every
   notification and status at once, dispatch what each needs, then return
   to the next maker block.
   _Done when_: the sweep leaves no notification unread and the next maker
   block has started.

## Example

Illustrative scenario; paths, commands, and results below are examples, not
artifacts or measurements from this repository.

**Request:** “Review the authorization diff while CI is running.”

Label reading the policy and tracing tenant isolation as maker work;
checking CI, the review queue, and status notifications as manager work.
If nothing requires an immediate reaction, start a closed maker block
whose endpoint is a completed role-by-role review. Let CI produce a
notification without polling it between policy branches. At the block's
end, read CI and the queue in one sweep, record or dispatch each required
follow-up, then start the next review block. If a release requires an
immediate decision, handle that before beginning a block that cannot stay
uninterrupted.
