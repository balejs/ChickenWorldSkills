# Skill: Create New Skills

**Purpose**: Create new skills following ChickenWorld documentation organization rules

**Use when**: You need to create a new skill for a specific task or workflow

---

## CRITICAL RULES

**All actual documentation/instructions must go in ChickenDocs first**. Skills should contain ONLY:
1. Moderate workflow instructions (10-15 lines, Option B)
2. References to relevant ChickenDocs sections
3. Trigger conditions (when to use the skill)
4. ChickenTools integration when applicable

**Before creating any skill, methodically parse ChickenDocs for ALL relevant documentation**:
- ChickenDocs/Common/ - Generic patterns and guidelines
- ChickenDocs/[ProjectName]/ - Project-specific details
- ChickenDocs/ChickenFundamentalsLib/ - Reference implementations

**Documentation Gap Rule**: If you discover missing documentation while creating a skill:
1. Create the documentation in ChickenDocs first (follows DOCUMENTATION_ORGANIZATION_RULES.md)
2. Reference the new documentation in the skill
3. Include practical examples and ChickenTools integration
4. Update ChickenDocs/ChickenSoftwareUpdateLib/README.md with new references

---

## Skill Creation Workflow

### Step 1: Identify Task Scope

**Define what the skill should accomplish:**
- What is the primary task?
- What ChickenWorld libraries/components are involved?
- Is this generic or project-specific?

### Step 2: Search ChickenDocs Methodically

**Search for existing documentation:**

**Generic patterns**:
```bash
cd /Users/marco/devel/ChickenWorld/ChickenDocs/Common
grep -r "task keyword" . --include="*.md"
ls -la *.md
```

**Project-specific details**:
```bash
cd /Users/marco/devel/ChickenWorld/ChickenDocs
find . -name "*.md" -exec grep -l "relevant keyword" {} \;
```

**Reference patterns**:
- [ChickenFundamentalsLib/](ChickenFundamentalsLib/) - Complex project documentation example
- [ChickenNetworkingLib/](ChickenNetworkingLib/) - Project structure template

### Step 3: Determine Skill Category

**Generic Skill** (applicable to all projects):
- Location: `~/.opencode/skills/`
- References: ChickenDocs/Common/*

**Project-Specific Skill**:
- Location: `~/.opencode/skills/`
- References: ChickenDocs/ChickenSoftwareUpdateLib/* and project-specific docs

### Step 4: Gather ALL Relevant References

**For each skill, collect ALL relevant ChickenDocs sections**:

**Example**: For a skill about creating TLS connections:
- [TLS_SNI_REQUIREMENT_2025-11-25.md](../../ChickenDocs/Common/TLS_SNI_REQUIREMENT_2025-11-25.md)
- [LOGGING_BEST_PRACTICES.md](../../ChickenDocs/Common/LOGGING_BEST_PRACTICES.md)
- [LOOPED_LISTENER_CIRCULAR_REFERENCE_2025-12-06.md](../../ChickenDocs/Common/LOOPED_LISTENER_CIRCULAR_REFERENCE_2025-12-06.md)
- [ChickenHttpLib/include/HttpExchange.h](../../ChickenHttpLib/include/HttpExchange.h) - API reference
- [ChickenHttpLib/test/HttpExchangeTester.cpp](../../ChickenHttpLib/test/HttpExchangeTester.cpp) - Usage examples

### Step 5: Create Skill File

**Location**: `~/.opencode/skills/[skill-name].md`

**Format**:
```markdown
# Skill: [Skill Name]

**Purpose**: [Brief description]

**Use when**: [When to trigger this skill]

**CRITICAL RULES**: [1-3 bullet points of essential rules]

**Workflow**:
1. Read [ChickenDocs/Common/DOC1.md](path)
2. Follow [ChickenDocs/[Project]/DOC2.md](path)
3. Verify with [Test pattern](path)

**Key references**:
- [Document 1](path) - Main guidelines
- [Document 2](path) - Examples
- [Document 3](path) - Common pitfalls

**Skills this relies on**:
- [Skill Name 1](skill-name-1.md)
- [Skill Name 2](skill-name-2.md)
```

### Step 6: Verify Completeness

**Checklist before completing skill creation:**
- [ ] Searched ChickenDocs/Common/ for relevant docs
- [ ] Searched ChickenDocs/[ProjectName]/ for project details
- [ ] Found ALL existing documentation on the topic
- [ ] Skill contains minimal instructions (≤20 lines workflow)
- [ ] All detailed info points to ChickenDocs references
- [ ] Added references to relevant ChickenDocs files
- [ ] Included cross-references to related skills

---

## Existing Skills (Reference)

**Organizational Skills**:
- [document-project-docs.md](document-project-docs.md) - Document project-specific details
- [organize-agents.md](organize-agents.md) - Organize AGENTS.md content

**Common Patterns Documented in ChickenDocs**:
- Logging: [LOGGING_BEST_PRACTICES.md](../../ChickenDocs/Common/LOGGING_BEST_PRACTICES.md)
- Circular References: [LOOPED_LISTENER_CIRCULAR_REFERENCE_2025-12-06.md](../../ChickenDocs/Common/LOOPED_LISTENER_CIRCULAR_REFERENCE_2025-12-06.md)
- TLS/SNI: [TLS_SNI_REQUIREMENT_2025-11-25.md](../../ChickenDocs/Common/TLS_SNI_REQUIREMENT_2025-11-25.md)
- Tokenizer: [development_guidelines.md](../../ChickenDocs/development_guidelines.md#tokenizer-usage-optimization)
- Lifecycle: [ChickenDocs/Common/CHICKENPTR_LIFECYCLE_CHECKS_ROLLOUT_2026-03-01.md](../../ChickenDocs/Common/CHICKENPTR_LIFECYCLE_CHECKS_ROLLOUT_2026-03-01.md)

**ChickenDocs Structure**:
- Generic guidelines: [ChickenDocs/Common/](../../ChickenDocs/Common/)
- Project docs: [ChickenDocs/ChickenSoftwareUpdateLib/](../../ChickenDocs/ChickenSoftwareUpdateLib/)
- Development practices: [ChickenDocs/development_guidelines.md](../../ChickenDocs/development_guidelines.md)

---

## Examples

### Example 1: Creating a "Create TLS Connection" Skill

**Search results**:
- TLS_SNI_REQUIREMENT_2025-11-25.md (SNI requirements)
- LOGGING_BEST_PRACTICES.md (logging setup)
- HttpExchange.h (API reference)

**Skill content**:
```markdown
# Skill: Create TLS Connection

**Use when**: Creating HTTPS/TLS connections in ChickenWorld

**CRITICAL**: Always provide domain name as SNI when using IP addresses

**Workflow**:
1. Read [TLS_SNI_REQUIREMENT_2025-11-25.md](../../ChickenDocs/Common/TLS_SNI_REQUIREMENT_2025-11-25.md)
2. Use MakeHttpExchange with SNI parameter
3. Add NetworkExchangeStateListener for error handling

**Reference**: [ChickenHttpLib/include/HttpExchange.h](../../ChickenHttpLib/include/HttpExchange.h)
```

### Example 2: Creating a "Debug Circular Reference" Skill

**Search results**:
- LOOPED_LISTENER_CIRCULAR_REFERENCE_2025-12-06.md
- development_guidelines.md (debugging rules)

**Skill content**:
```markdown
# Skill: Debug Circular Reference

**Use when**: Tests hang, sockets not destroyed, 10-second timeouts

**CRITICAL**: Pass `true` for weakListenerRef in LoopedSocketListener

**Workflow**:
1. Check test duration (>10s = circular reference likely)
2. Find LoopedSocketListener creation
3. Verify `true` parameter passed

**Reference**: [LOOPED_LISTENER_CIRCULAR_REFERENCE_2025-12-06.md](../../ChickenDocs/Common/LOOPED_LISTENER_CIRCULAR_REFERENCE_2025-12-06.md)
```

---

## Quality Checklist

**Every skill must have**:
- [x] Clear purpose statement
- [x] Trigger conditions ("Use when...")
- [x] Minimal workflow (3-5 steps max)
- [x] At least 3 ChickenDocs references
- [x] Cross-references to related skills
- [x] File location in .opencode/skills/

**Every skill must NOT have**:
- [ ] Detailed code examples (reference them instead)
- [ ] Long explanations (summarize and link)
- [ ] Architecture details (point to ChickenDocs)
- [ ] More than 30 lines of actual content

---

**Created**: 2026-05-21  
**Purpose**: Framework for creating skills that follow ChickenWorld documentation standards
