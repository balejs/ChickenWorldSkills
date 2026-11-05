---
name: skill-maintenance
description: Create and revise ChickenWorld skills - location, format, path conventions and quality bar
---

# Skill: Skill Maintenance

**Purpose**: Create new skills and revise existing ones without letting the set rot

**Use when**: Adding a skill, editing one, or reorganising the skill collection

**Last Updated**: 2026-11-05

Merges `create-skills` and `modify-skills` - they shared one checklist split by verb.

---

## Location and format

Canonical home is the **only** clone: `~/devel/ChickenWorld/ChickenWorldSkills/`.
`~/.claude/skills` and `~/.config/opencode/skills` are **symlinks into it** - never write
there directly, and never clone this repo elsewhere.

```
ChickenWorldSkills/<skill-name>/SKILL.md      ← correct
~/.opencode/skills/<skill-name>.md            ← WRONG dir, WRONG format
```

Every skill is a **directory containing `SKILL.md`** with YAML frontmatter:

```markdown
---
name: <skill-name>
description: <one line, states what it does and when>
---

# Skill: <Title>

**Purpose**: ...
**Use when**: <trigger conditions>

**CRITICAL RULES**: ...
**Workflow**: ...
**Key references**: ...
**Skills this relies on**: ...
```

## CRITICAL RULES

1. **ALWAYS** write the substance into ChickenDocs first; the skill is a thin router of
   10-15 lines plus links
2. **ALWAYS** search `ChickenDocs/Common/` and `ChickenDocs/<Project>/` before creating -
   if the documentation does not exist, create it there, then reference it
3. **ALWAYS** use absolute paths for ChickenDocs and relative paths for skill-to-skill
   links (`../other-skill/SKILL.md`)
4. **NEVER** inline code examples, architecture detail or long explanations - link instead
5. **ALWAYS** update the README catalog when adding, removing or renaming a skill
6. When a change to one skill invalidates another, fix both in the same commit
7. When **revising**, preserve the existing structure - frontmatter, heading order and
   organisation stay as they are; change content, not shape, unless the shape is the defect

**Documentation Gap Rule**: when creating or editing reveals documentation that should exist
but does not - write the documentation in ChickenDocs first, then reference it from the
skill. Never let the skill become the only place a fact is written down.

## Workflow

1. **Search** - `grep -r "<topic>" ChickenDocs/Common ChickenDocs/<Project>` and read
   `README.md` to find whether a skill already owns this subject. Extending an owner beats
   creating a neighbour.
2. **Write the doc** - substance goes to ChickenDocs per
   [DOCUMENTATION_ORGANIZATION_RULES.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/DOCUMENTATION_ORGANIZATION_RULES.md)
3. **Write or revise the skill** - thin, linked, each rule carrying its trigger and test
4. **Verify paths resolve** - every link must point at a file that exists
5. **Review the diff** against the three principles in
   [documentation-maintenance](../documentation-maintenance/SKILL.md)
6. **Update README** catalog and totals

## Splitting a skill that has outgrown itself

Split when it covers subjects that are loaded in different contexts - e.g. SSH setup,
commit format and branch policy are three skills, not one 470-line file. Split when:

- it exceeds ~150 lines, or
- you routinely load it for reason A while only rules for reason B apply, or
- two sections have begun to drift from each other.

Keep a pointer in the old name if anything still references it.

## Propose a new skill rather than bloating an existing one

Flag to Marco before creating a skill when a topic is broad enough not to fit an existing
owner, or when an existing skill has grown across competence areas and two smaller skills
would load and maintain better. Do not create silently.

---

**Key references**:
- [DOCUMENTATION_QUALITY_PRINCIPLES.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/DOCUMENTATION_QUALITY_PRINCIPLES.md) - Consistency, conciseness, clarity
- [DOCUMENTATION_ORGANIZATION_RULES.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/DOCUMENTATION_ORGANIZATION_RULES.md) - Where content goes
- [DOCUMENTATION_DIRECTIVE.md](/Users/marco/devel/ChickenWorld/ChickenDocs/DOCUMENTATION_DIRECTIVE.md) - When and what to document

**Skills this relies on**:
- [documentation-maintenance](../documentation-maintenance/SKILL.md) - The three principles
- [deep-save](../deep-save/SKILL.md) - Routing session findings to their home
- [organize-agents](../organize-agents/SKILL.md) - AGENTS.md structure
