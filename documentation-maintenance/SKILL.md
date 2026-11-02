---
name: documentation-maintenance
description: Write and revise ChickenWorld documentation under the three quality principles - consistency, conciseness, clarity
---

# Skill: Documentation Generation & Maintenance

**Purpose**: Produce and revise documentation that stays true — one fact in one place,
stated once, checkable by a stated test.

**Use when**: creating any new document, revising an existing one, merging content
between documents, or reviewing a documentation diff.

---

## Leading principles — apply to every write and every revision

1. **Consistency — one truth, one place.** Every fact, rule and procedure is stated in
   exactly one authoritative location; everywhere else is a pointer. When new information
   contradicts documented information, **edit the existing claim** — never append a
   correction and leave the wrong statement standing. Audit for *primary*, *main*,
   *canonical*: if the section bearing that label is not the current one, the label is a
   defect.
   **Test:** *can two passages in this corpus disagree?* If yes, one must go.

2. **Conciseness — say it once, where it is owned.** Redundancy is allowed only when it
   strengthens: a thin skill plus the detailed doc it points to earns its space because
   they are loaded in different contexts; near-verbatim blocks 200 lines apart do not.
   **Test:** *if these two passages drifted, would anyone notice?* If they could disagree
   silently, one is a future contradiction, not reinforcement.

3. **Clarity — every rule is checkable.** Each rule states its **action**, its
   **trigger**, and its **test**. A rule with no test is a preference. State scope at
   first use, name the platform or version, and label claims
   `measured` / `inferred` / `hypothesis` / `ruled-out`.
   **Test:** *could two competent readers act differently on this text?* If yes, it is
   not yet a rule.

**Fix in that order** — consistency, then conciseness, then clarity. Collapsing two
passages that disagree forces a decision about which is true, and that decision must
precede the choice of which to keep; polishing the prose of a contradiction only makes it
more persuasive.

## Workflow

1. **Locate the owner** — search the corpus for the section that owns the subject. If it
   exists you are revising, not creating.
2. **Write or revise** under the three principles; give each rule its trigger and test.
3. **Supersede properly** — delete or edit what your change replaces; leave a pointer so
   the absence reads as intentional.
4. **Review the diff against the three tests** in order before committing.
5. **Wire it in** — link new documents from the relevant index (`AGENTS.md`,
   `ChickenDocs/README.md`) so they are discoverable.

## Reference

- `ChickenDocs/Common/DOCUMENTATION_QUALITY_PRINCIPLES.md` — the principles in detail,
  with the failures that produced them
- `ChickenDocs/DOCUMENTATION_DIRECTIVE.md` — when and what to document
- `ChickenDocs/Common/DOCUMENTATION_ORGANIZATION_RULES.md` — where content goes
- `ChickenWorldSkills/deep-save/SKILL.md` — preserving session context into docs
