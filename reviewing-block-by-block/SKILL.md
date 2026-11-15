---
name: reviewing-block-by-block
description: Conduct the live code review with Marco - one commit per block, context before the diff, risks after it, and stop for feedback before continuing
---

# Skill: Reviewing Block By Block

**Purpose**: Walk Marco through a verified change one decision at a time, so each block can be
approved or rejected on its own and an objection is settled before it compounds into the next block.

**Use when**: Marco says he is starting the review, asks to go through changes block by block, or a
change is large enough that one message cannot carry it. Not for writing the packet (that is
`review-for-approval`) and not for findings with no change attached (`explaining-to-marco`).

**CRITICAL RULES**:
1. **ALWAYS** give the context **before** the diff: what the block does, where it sits, **who consumes
   its output**, **when it runs**, **how** it achieves it. Full list and why:
   /Users/marco/devel/ChickenWorld/ChickenDocs/Common/REVIEW_FOR_APPROVAL.md § *The interactive walkthrough*
2. **ALWAYS** close every block with potential negative issues and side effects — **even when there are
   none**; say what was checked. An absent risk section is indistinguishable from an unconsidered risk
3. **ALWAYS** stop after each block and wait. Never preview the next one, never batch two
4. **ALWAYS** apply `explaining-to-marco` in full to each block, ≤500 words of prose, diffs excluded
5. **NEVER** carry an unanswered objection forward, and **NEVER** fix code mid-walkthrough without
   re-taking the measurements of every later block
6. **ALWAYS** write the decisions and answers back into the packet file at the end, and restate which
   blocks were approved, rejected, or never reached

**Workflow**: packet file exists first → per block: context → diff with the reason per hunk → risks →
stop → record the answer → next block → closing summary.

**Key references**:
- /Users/marco/devel/ChickenWorld/ChickenDocs/Common/REVIEW_FOR_APPROVAL.md - the seven parts, the
  acceptance gate, and § *The interactive walkthrough*
- /Users/marco/devel/ChickenWorld/ChickenDocs/Common/EXPLAINER_RULES.md - rules applied per block

**Skills this relies on**:
- [review-for-approval](../review-for-approval/SKILL.md) - what the packet must contain before the walk
- [explaining-to-marco](../explaining-to-marco/SKILL.md) - how each block is written
- [git-investigation-branches](../git-investigation-branches/SKILL.md) - never re-split history mid-review
