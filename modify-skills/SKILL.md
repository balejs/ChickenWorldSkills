---
name: modify-skills
description: Update existing skills while maintaining ChickenWorld documentation standards
---

# Skill: Modify Existing Skills

**Purpose**: Update existing skills while preserving ChickenWorld documentation standards

**Use when**: Updating an existing skill's content, references, or format

---

## CRITICAL RULES

**Preserve existing structure and format**:
1. Maintain Option B format (10-15 lines with workflow + links)
2. Keep existing ChickenDocs references intact
3. Update paths to match convention (absolute ChickenDocs, relative skill links)
4. Update cross-references when related skills change

**Documentation Gap Rule**: If modifying reveals missing documentation:
1. Create documentation in ChickenDocs first
2. Reference new documentation in the skill
3. Update skill cross-references accordingly

---

## Workflow

1. **Review current skill** - Read the existing SKILL.md to understand format
2. **Preserve structure** - Keep YAML frontmatter, headers, and organization
3. **Update content** - Modify workflow steps or ChickenDocs references as needed
4. **Maintain path conventions**:
   - ChickenDocs: Absolute paths (`/Users/marco/devel/ChickenWorld/ChickenDocs/...`)
   - Skills: Relative paths (`../skill-name/SKILL.md`)
5. **Verify completeness** - Run quality checklist from [create-skills](../create-skills/SKILL.md)

---

## Quality Checklist

**Use [create-skills](../create-skills/SKILL.md) Step 6 as reference**:
- [ ] Clear purpose statement
- [ ] Trigger conditions ("Use when...")
- [ ] Minimal workflow (3-5 steps max)
- [ ] At least 3 ChickenDocs references
- [ ] Cross-references to related skills
- [ ] File location in `~/.config/opencode/skills/` or repo

**What NOT to change**:
- [ ] Don't add detailed code examples (reference ChickenDocs instead)
- [ ] Don't add long explanations (summarize and link)
- [ ] Don't add architecture details (point to ChickenDocs)
- [ ] Don't exceed 30 lines of actual content

---

## Example: Updating a Skill

**Scenario**: Update skill to include new ChickenDocs reference

**Before**:
```markdown
**Workflow**:
1. Read [LOGGING_BEST_PRACTICES.md](...)
2. Check [ESP32_PLATFORM_DIFFERENCES.md](...)
```

**After**:
```markdown
**Workflow**:
1. Read [LOGGING_BEST_PRACTICES.md](...)
2. Check [ESP32_PLATFORM_DIFFERENCES.md](...)
3. Review [CHICKENPTR_LIFECYCLE_CHECKS_ROLLOUT_2026-03-01.md](...)  # NEW
```

---

## Skills This Relies On

- [create-skills](../create-skills/SKILL.md) - Format and quality standards
- [document-project-docs](../document-project-docs/SKILL.md) - Documentation organization

---

**Related**: [create-skills](../create-skills/SKILL.md) - For creating new skills
