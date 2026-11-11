---
name: explaining-to-marco
description: Write an explanation, finding or answer that Marco can read without the agent's context - readable, concise, non-prosaic, with openable code references
---

# Skill: Explaining to Marco

**Purpose**: Explain something so it stands on its own, without the session's working context

**Use when**: Answering a question, reporting a finding, or describing a change in conversation

**Priority order**: readable → concise → non-prosaic. They conflict; cut words before cutting
explanation.

**CRITICAL RULES**:
1. **NEVER** use a name the reader does not already have — internal IDs (`T1`, `N4`), bare line
   numbers (`:648`), hashes, log filenames. Expand it inline or recap it in one context block
2. **ALWAYS** quote the 3–8 lines you are describing. A line number is a pointer, not an explanation
3. **ALWAYS** name the function and write `File.cpp:648` — never a bare `:648` — and state once per
   explainer which directory those files live in. Escalate to `code -g <abs path>:<line>` only when
   the short form is ambiguous
4. **ALWAYS** put context in exactly one block at one end, or embed it per paragraph — never neither
5. **ALWAYS** give numbers units and a source, and mark measured vs inferred
6. **NEVER** write sentences that only announce or connect other sentences; the first sentence
   carries content
7. **ALWAYS** run the final-pass checklist on the draft before showing it — the pass is a step, not
   an intention

**Workflow**: draft → run the checklist in the reference doc → fix → show.

**Key references**:
- [EXPLAINER_RULES.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/EXPLAINER_RULES.md) - the rules with triggers, tests and the final-pass checklist

**Skills this relies on**:
- [documentation-maintenance](../documentation-maintenance/SKILL.md) - the three quality principles
- [deep-save](../deep-save/SKILL.md) - where a finding goes when it stops being conversation
