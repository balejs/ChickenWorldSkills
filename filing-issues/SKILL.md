---
name: filing-issues
description: File or manage a GitHub issue safely - per-action per-repo approval, a reproduction in that repo first, and explainer rules applied to the title, body and every comment
---

# Skill: Filing Issues

**Purpose**: Keep the tracker honest — no remote side effect without authorisation, no public claim
without a reproduction, no issue a cold reader cannot act on.

**Use when**: About to open, close, re-open, comment on, label, relabel or assign an issue in any
ChickenWorld repository; or when a finding points at a dependency's code.

**CRITICAL RULES**:
1. **ALWAYS** pass the quote test before any remote write: *can I quote the sentence that authorised
   this action, naming this repository?* Full rule:
   [GIT_COMMIT_GUIDELINES.md § Remote Side Effects Require Explicit Approval](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/GIT_COMMIT_GUIDELINES.md)
2. **NEVER** treat anticipation as authorisation. *"we may need to file"*, *"possibly"*, *"if it confirms"*
   authorise nothing — write a ledger row and ask
3. **NEVER** file against a repository you have not reproduced in. Reading another repo's source and
   finding a plausible mechanism makes it a **finding**, not a defect report. Filed
   `ChickenParsersLib#1` on exactly that and it closed `not planned`
4. **ALWAYS** apply [EXPLAINER_RULES.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/EXPLAINER_RULES.md)
   to the title, the body and every later comment — quote the code, name the function, `File.cpp:648`
   with the repo stated once, numbers with units and a source, lists over tables. Run the final-pass
   checklist as a step
5. **ALWAYS** give frequency as *n* of *m* runs, and say when *m* is too small to mean anything
6. **ALWAYS** link the ledger row that owns it — the ledger is the authority, the issue is the surface
7. **NEVER** quietly delete a wrong claim: comment the disproof, close as *not a defect*, mark the ledger
   row `REFUTED` with its reopen condition

**Workflow**: ledger row first → reproduce in the target repository → check approval per action per repo →
draft to the seven-part structure → run the explainer final pass → **show Marco the draft** → file →
set the Status label → link back from the ledger.

**Key references**:
- [ISSUE_FILING.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/ISSUE_FILING.md) - the rules with
  their triggers and tests, the seven-part body structure, the Status label set, and how to correct an
  issue that was wrong

**Skills this relies on**:
- [explaining-to-marco](../explaining-to-marco/SKILL.md) - the writing rules an issue is judged by
- [review-for-approval](../review-for-approval/SKILL.md) - the acceptance gate before presenting a fix
- [investigation-workflow](../investigation-workflow/SKILL.md) - where a finding lives before it is filed
- [git-commit-conventions](../git-commit-conventions/SKILL.md) - remote side effects and commit hygiene
