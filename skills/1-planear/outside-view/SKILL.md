---
name: outside-view
description: "Outside view for estimates — size the work from the reference class of similar past work, not from the plan in front of you. Use when estimating duration, effort, or risk, when a plan looks quick, or when a previous estimate for similar work was missed."
---

# Outside View

Kahneman's planning fallacy: the inside view sees this plan and its
reasons to go well; the **outside view** asks how long things *like this*
took. The reference class beats the plan on average, and the plan does not
know it is average.

## Steps

1. **Name the reference class.** Three or more past pieces of work that a
   stranger would call similar in kind and size — with their locators
   (commits, PRs, issues) and what they actually took: elapsed time, rounds
   of rework, incidents after shipping.
   _Done when_: three members with actual figures, not remembered ones.

2. **Take the base rate.** The median of the class, and the worst member.
   That is the estimate until evidence moves it.
   _Done when_: median and worst are written next to the inside-view
   estimate.

3. **Adjust only with a named difference.** Move off the base rate only
   for a concrete way this work differs from the class — and by how much
   that difference moved a past member.
   _Done when_: each adjustment cites the difference and a past member, or
   the base rate stands. Report the final figure with the class beside it.

## Example

Illustrative scenario; paths, commands, and results below are examples, not
artifacts or measurements from this repository.

**Request:** “This migration looks like two days. Estimate it.”

Use three comparable migrations with recorded elapsed times: PR #101,
4 days and 1 rework round; #108, 6 days and 2 rounds; #119, 11 days and
3 rounds. Each had zero recorded incidents in the same 30-day follow-up
window. The median is 6 days and the worst is 11, beside the inside-view
estimate of 2. “We understand this one better” has no measured adjustment
behind it, so report 6 days as the baseline and 11 as the observed worst,
not a guaranteed upper bound. If those records are unavailable, report the
missing evidence rather than inventing a reference class.
