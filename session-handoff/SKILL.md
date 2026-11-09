---
name: session-handoff
description: Prepare the handoff a fresh session needs to continue work - live state, skills to load, next operations, expected results
---

# Skill: Session Handoff

**Purpose**: Write the file, plus the paste-ready prompt, that lets a session with **no
memory of this one** take the next correct action without re-deriving anything.

**Use when**: Marco asks for a handoff or for the next session's prompt; this session opened
with a continuation summary; a long unattended block is about to start whose analysis may
outlive the session; work is delegated to a fresh session; end of session with anything open.

## Workflow

1. **Deep save first** — knowledge goes to its permanent home; the handoff then *links* it
   instead of duplicating it (see skill `deep-save`).
2. Write `<project>/investigation/HANDOFF_<YYMMDD_HHMM>.md`. Never overwrite an earlier one.
3. Fill **all nine sections**: 0 load-first (skills + docs, absolute path and reason each) ·
   1 state · 2 established (ledger with status) · 3 in flight · 4 next operations ·
   5 waiting on Marco · 6 traps already paid for · 7 provenance · 8 definition of done.
4. **Verify before declaring it written**: every absolute path resolves, and live state
   (branch, commits, tree, processes) is *re-measured*, not remembered.
5. Commit on the investigation branch; name the file from the consolidated investigation doc
   so a cold session finds it.
6. Emit the prompt that **forces the load step** — it makes the next session read the file
   and restate step 1 and its expected output. It does not summarise the findings.

## Hard rules

- **Never report a context percentage.** No tool measures it; "nearly exhausted" is an
  inference. The observable 90% signal is a continuation summary at session start.
- **Name the skills explicitly.** They are not auto-discovered; unlisted means unread.
- **Every next operation carries `expected` and `contradiction`** — otherwise a surprising
  result is indistinguishable from a broken harness.
- **Record built-but-not-enabled and armed-but-inactive** mechanisms; source code alone does
  not show them.
- No root cause, no `RESOLVED`. Handoffs describe; Marco closes.

## Reference

- `ChickenDocs/Common/SESSION_HANDOFF.md` — sections, triggers, rationale, the path check
- `ChickenDocs/Common/DEEP_SAVE_PROCEDURE.md` — the knowledge half; capacity-trigger caveat
- `ChickenDocs/INVESTIGATION_PROCEDURE.md` — the loop a handoff resumes
