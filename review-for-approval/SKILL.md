---
name: review-for-approval
description: Present a completed, verified change for Marco's sign-off - per-commit measurements, what was not done, what the fix unmasked
---

# Skill: Review For Approval

**Purpose**: Hand a finished change to Marco so every decision in it can be approved or rejected
without opening a file.

**Use when**: Work is verified and the next action is Marco's — merge, push, forward-port, reject.
Not for progress reports (use `session-handoff`) and not for findings without a change (use
`explaining-to-marco`).

**CRITICAL RULES**:
1. **ALWAYS** write the packet to `<project>/investigation/REVIEW_<YYYY-MM-DD>_<slug>.md`, then
   present it condensed — the file is what survives the session
2. **ALWAYS** include all seven parts; a packet missing per-commit measurements, the not-done list,
   or the unmasked-defects section is not reviewable — send it back rather than presenting it
3. **ALWAYS** give the measurement taken **after each commit**, not one green run at the tip
4. **ALWAYS** name any defect the fix unmasked as a separate item, and say whether the change caused
   it or merely made it observable
5. **NEVER** present a change and a fix for an unmasked defect as one packet — two decisions, two
   packets
6. **NEVER** write "tests pass": give counts, units and log filenames, and mark flaky results with
   their observed frequency
7. **ALWAYS** include the wrong hypotheses corrected en route; a reviewer who sees only the final
   theory cannot tell tested from guessed

**Workflow**: gather (branch, base, pushed?, per-commit run results, remaining reds) → write the
packet → run the explainer final pass on it → present → record the decisions and their answers back
into the packet.

**Key references**:
- `/Users/marco/devel/ChickenWorld/ChickenDocs/Common/REVIEW_FOR_APPROVAL.md` - the seven parts, the
  rules with their tests, the anti-pattern table
- `/Users/marco/devel/ChickenWorld/ChickenDocs/Common/EXPLAINER_RULES.md` - presentation rules,
  applied in full to the packet

**Skills this relies on**:
- [explaining-to-marco](../explaining-to-marco/SKILL.md) - the packet is an explainer
- [deep-save](../deep-save/SKILL.md) - corrected hypotheses are edited, not appended
- [session-handoff](../session-handoff/SKILL.md) - anything still open goes to the next session
