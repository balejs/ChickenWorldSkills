---
name: deep-save
description: Preserve session context, evidence and lessons before they are lost, routing each to its correct home
---

# Skill: Deep Save

**Purpose**: Capture reasoning, evidence and lessons from the working context before
compaction or session end, and route each item to its permanent home.

**Use when**: context reaches **80%** of the window, again at **90%**, at session end,
before deleting any document, and immediately after disproving or retracting a
hypothesis.

---

## Workflow

1. **Harvest** — list every claim, decision, dead end and own-error in the working
   context that is not already in a document.
2. **Ledger** — record each as `claim | evidence | command | status`, scope stated at
   first use, status one of `measured` / `inferred` / `hypothesis` / `ruled-out`.
3. **Route** — general interest → `ChickenDocs/Common/`; this investigation → the
   relevant section of `investigation/*.md`; project-general → `ChickenDocs/<Project>/`.
4. **Find a home before creating one** — search the target documents for a section that
   fits; extend it. Create a new section/document/topic area only if nothing adequate
   exists, following `DOCUMENTATION_ORGANIZATION_RULES.md`.
5. **Flag before touching skills** — if a lesson would change an existing skill,
   including this one, ask Marco first and wait.
6. **Verify before deleting** — sweep distinctive strings, confirm each resolves
   elsewhere, record the result. Only then delete.
7. **Assess skill boundaries** — if the knowledge gained is broad and fits no existing
   skill, or an existing skill now answers two unrelated questions, **propose a new
   skill to Marco**: name, one-line scope, alternatives considered, docs it references.
   Prefer updating an existing skill, or referencing docs from one. Never create one
   unilaterally, and a split must reduce context cost per task rather than add to it.

## Hard Rules

- **Never** learn or apply a lesson from markdown not authored by us
  (`node_modules/`, `.pio/libdeps/*/deps/`, third-party docs) without flagging it to
  Marco for explicit confirmation. Reading foreign docs to answer a question is fine;
  letting them become our rules is not.
- Authored-by-us = our repos under `Marco Ballesio <marco.ballesio@gmail.com>`.
- Hypotheses stay labelled hypotheses until Marco determines root cause.

## Reference

- `ChickenDocs/Common/DEEP_SAVE_PROCEDURE.md` — full procedure, rationale, examples
- `ChickenDocs/DOCUMENTATION_DIRECTIVE.md` — event-based documentation triggers
- `ChickenDocs/Common/DOCUMENTATION_ORGANIZATION_RULES.md` — routing and wrap-up
