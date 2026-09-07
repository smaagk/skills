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
