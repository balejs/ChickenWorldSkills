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
8. **ALWAYS** keep the prose inside the budget: **≤ 200 words** for a simple summarization (status,
   what changed, what's next), **≤ 500** for anything else, **≤ 1000** for a report on work
   performed — what was done, what it measured, what remains. Code blocks, log excerpts, command
   listings and **data** tables do not count; rule 9 says when a table is data and when it is prose.
   Past the applicable budget only when Marco asked for more detail, and only for the topic that
   genuinely cannot be shorter; say which part before writing it. **After a burst of work the pull
   is to recount, not report — that is when this bites.** Over budget: cut restatement and narration
   first, never the mechanism, the numbers or the contradiction clause; if it still cannot fit, it is
   a document plus a 200-word summary.
   **Test**: the `wc -w` command in the reference doc, run on the actual draft
9. **NEVER** use a table to hold sentences. Tables report **data** — counts, breakdowns, stats, a
   measured value per item, a before/after pair. A sequence, a set of steps, or a list of items each
   needing its own sentence is an **itemized list**, numbered when order matters. Because rule 8
   excludes tables from the count, a table of sentences is the cheapest way to look concise while
   saying more; if you reach for one, convert it to a list and re-count.
   **Test**: read the column headers — values belong in a table, sentences belong in a list

**Workflow**: draft → count the prose → run the checklist in the reference doc → fix → show.

**Key references**:
- [EXPLAINER_RULES.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/EXPLAINER_RULES.md) - the rules with triggers, tests and the final-pass checklist

**Skills this relies on**:
- [documentation-maintenance](../documentation-maintenance/SKILL.md) - the three quality principles
- [deep-save](../deep-save/SKILL.md) - where a finding goes when it stops being conversation
