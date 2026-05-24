---
name: document-project-docs
description: Document project-specific details in ChickenDocs
---

# Skill: Document Project-Specific Details

**Purpose**: Organize and document ChickenWorld project-specific architecture, patterns, and investigations

**Use when**:
- Documenting a new ChickenWorld project
- Creating project structure documentation
- Recording investigation findings
- Organizing project-specific guidelines

**CRITICAL RULES**:
1. **All actual documentation** must exist in appropriate ChickenDocs locations (not in skill itself)
2. **Skill provides workflow** that points to ChickenDocs references
3. **Always search ChickenDocs first** for existing guidelines before creating new docs

---

## Workflow

### 1. Determine Documentation Scope

**Check if project is simple or complex:**
- Simple (2-4 headers, straightforward): Use inline API docs + README
- Complex (many headers, intricate design): Use Architecture docs + Guidelines

**Reference**: 
- [PROJECT_DOCUMENTATION_BLUEPRINT.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/Documentation/Process/PROJECT_DOCUMENTATION_BLUEPRINT.md) - Complete documentation process
- [ChickenDocs/ChickenFundamentalsLib/](/Users/marco/devel/ChickenWorld/ChickenDocs/ChickenFundamentalsLib/) - Complex project example
- [ChickenDocs/ChickenLoggerLib/](/Users/marco/devel/ChickenWorld/ChickenDocs/ChickenLoggerLib/) - Simple project example

### 2. Document Project Structure

**Create project structure document** if it doesn't exist:
- Location: `ChickenDocs/[ProjectName]/[ProjectName]_PROJECT_STRUCTURE.md`
- Content: Directory layout, dependencies, build system, platform-specific notes

**Reference**:
- [ChickenNetworkingLib_PROJECT_STRUCTURE.md](/Users/marco/devel/ChickenWorld/ChickenDocs/ChickenNetworkingLib/ChickenNetworkingLib_PROJECT_STRUCTURE.md) - Template with multi-repo structure details
- [ChickenSpaceTimeLib_PROJECT_STRUCTURE.md](/Users/marco/devel/ChickenWorld/ChickenDocs/ChickenSpaceTimeLib/ChickenSpaceTimeLib_PROJECT_STRUCTURE.md) - Example with ESP-specific notes

### 3. Organize Investigation Findings

**For investigation-specific content:**

**Option A**: Move to ChickenDocs/[ProjectName]/ when investigation is complete
- File naming: `INVESTIGATION_YYYY-MM-DD.md` or `TOPIC_FIX_YYYY-MM-DD.md`

**Option B**: Keep in project's `investigation/` folder during active work
- File naming: `SESSION_YYYYMMDD.md`, `FINDINGS_YYYYMMDD.md`

**Reference**:
- [ChickenDocs/Common/GIT_COMMIT_GUIDELINES.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/GIT_COMMIT_GUIDELINES.md) - When to commit investigation docs
- [development_guidelines.md](/Users/marco/devel/ChickenWorld/ChickenDocs/development_guidelines.md) - Documentation-First Investigation rule

### 4. Follow Common Guidelines

**Check for applicable Common guidelines:**

**Coding patterns**:
- [LOGGING_BEST_PRACTICES.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/LOGGING_BEST_PRACTICES.md) - Logging setup and macros
- [LOOPED_LISTENER_CIRCULAR_REFERENCE_2025-12-06.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/LOOPED_LISTENER_CIRCULAR_REFERENCE_2025-12-06.md) - Circular reference avoidance
- [TLS_SNI_REQUIREMENT_2025-11-25.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/TLS_SNI_REQUIREMENT_2025-11-25.md) - TLS SNI requirements

**Development practices**:
- [development_guidelines.md](/Users/marco/devel/ChickenWorld/ChickenDocs/development_guidelines.md) - Debugging, coding, testing guidelines
- [GIT_COMMIT_GUIDELINES.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/GIT_COMMIT_GUIDELINES.md) - Commit message and handling rules

### 5. Align with Standards

**Verify alignment with ChickenWorld standards:**

**API documentation**:
- [API_DOCUMENTATION_GUIDELINES.md](/Users/marco/devel/ChickenWorld/ChickenDocs/API_DOCUMENTATION_GUIDELINES.md) - Doxygen standards
- [INLINE_EXAMPLE_GUIDELINES.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/Documentation/Guidelines/INLINE_EXAMPLE_GUIDELINES.md) - Example code standards

**Process**:
- [PROJECT_DOCUMENTATION_PROCESS.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/Documentation/Process/PROJECT_DOCUMENTATION_PROCESS.md) - 12-phase verification workflow

---

## File Structure

### ChickenDocs/[ProjectName]/
```
ChickenDocs/ChickenSoftwareUpdateLib/
├── README.md  # Project documentation index
├── ChickenSoftwareUpdateLib_PROJECT_STRUCTURE.md  # Directory, dependencies
├── TEST_ARCHITECTURE.md  # Test system architecture
├── TEST_SEQUENCING.md  # Test sequence documentation
├── INVESTIGATION_YYYY-MM-DD.md  # Investigation reports
└── LESSONS_LEARNED_YYYY-MM-DD.md  # Lessons from investigations
```

### Project's `investigation/` (active work)
```
investigation/
├── STATUS.md  # Current status
├── SESSION_YYYYMMDD.md  # Session notes
├── FINDINGS_YYYYMMDD.md  # Key findings
└── [Active investigation files...]
```

---

## Key Decision Points

### Where Does Content Go?

1. **Generic ChickenWorld knowledge** → ChickenDocs/Common/
2. **Project-specific architecture** → ChickenDocs/[ProjectName]/
3. **Active investigation work** → project/investigation/
4. **Developer-facing docs** → project/docs/ (symlink)
5. **AGENTS.md** → Only minimal references and index

**Reference**: [DOCUMENTATION_ORGANIZATION_RULES.md](DOCUMENTATION_ORGANIZATION_RULES.md) - Complete organization rules

### When to Create New vs Use Existing

**Create new documentation when**:
- Finding new bug/issue with unique root cause
- Discovering project-specific architectural pattern
- Documenting test system unique to this project

**Use existing guidelines when**:
- Issue matches existing ChickenDocs/Common pattern
- Coding guideline already documented
- Debugging procedure already exists

---

## Quick Reference

**Core ChickenDocs locations**:
- Generic guidelines: [ChickenDocs/Common/](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/)
- Development practices: [development_guidelines.md](/Users/marco/devel/ChickenWorld/ChickenDocs/development_guidelines.md)
- Documentation process: [PROJECT_DOCUMENTATION_BLUEPRINT.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/Documentation/Process/PROJECT_DOCUMENTATION_BLUEPRINT.md)
- Organization rules: [DOCUMENTATION_ORGANIZATION_RULES.md](DOCUMENTATION_ORGANIZATION_RULES.md)

**ChickenSoftwareUpdateLib-specific**:
- Project structure: ChickenDocs/ChickenSoftwareUpdateLib/ChickenSoftwareUpdateLib_PROJECT_STRUCTURE.md (to be created)
- Active investigations: investigation/ folder

---

## Skills This Skill Relies On

1. **Search ChickenDocs** - Methodically find relevant documentation
2. **Organize Documentation** - Apply documentation organization rules
3. **Create Investigation Reports** - Document investigation findings
4. **Align with Standards** - Ensure consistency with ChickenWorld guidelines

---

**Created**: 2026-05-21  
**Purpose**: Framework for organizing project-specific documentation following ChickenWorld standards
