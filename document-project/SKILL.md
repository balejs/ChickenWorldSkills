---
name: document-project
description: Document new ChickenWorld projects following established patterns
---

# Skill: Document Project

**Purpose**: Document new ChickenWorld projects following established standards

**Use when**: Starting documentation for a new or existing ChickenWorld project

**CRITICAL RULES**:
1. **ALWAYS** follow PROJECT_DOCUMENTATION_BLUEPRINT.md workflow
2. **ALWAYS** create PROJECT_STRUCTURE.md for multi-repo projects
3. **ALWAYS** verify ALL headers are documented (public and internal)
4. Move architecture details to dedicated docs, not headers

**Workflow**:
```bash
# Phase 1: Discovery
find include src -name "*.h" | xargs grep -l "@file" > headers.txt

# Phase 2: Create tracking document
ChickenDocs/[ProjectName]/API_DOCUMENTATION_VERIFICATION.md

# Phase 3: Follow 12-phase process from blueprints
# Reference: Common/Documentation/Process/PROJECT_DOCUMENTATION_BLUEPRINT.md
```

**Document locations**:
- **Project structure**: `ChickenDocs/[ProjectName]/[ProjectName]_PROJECT_STRUCTURE.md`
- **API documentation**: In header files (slim @file blocks ≤15 lines)
- **Architecture**: `ChickenDocs/[ProjectName]/Architecture/*.md`
- **Investigations**: `ChickenDocs/[ProjectName]/INVESTIGATION_YYYY-MM-DD.md`

**Key references**:
- [Common/Documentation/Process/PROJECT_DOCUMENTATION_BLUEPRINT.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/Documentation/Process/PROJECT_DOCUMENTATION_BLUEPRINT.md) - Complete blueprint
- [Common/Documentation/Process/PROJECT_DOCUMENTATION_PROCESS.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/Documentation/Process/PROJECT_DOCUMENTATION_PROCESS.md) - 12-phase process
- [ChickenNetworkingLib/ChickenNetworkingLib_PROJECT_STRUCTURE.md](/Users/marco/devel/ChickenWorld/ChickenDocs/ChickenNetworkingLib/ChickenNetworkingLib_PROJECT_STRUCTURE.md) - Project structure template
- [ChickenFundamentalsLib/REFACTORING_COMPLETE_2025-11-09.md](/Users/marco/devel/ChickenWorld/ChickenDocs/ChickenFundamentalsLib/REFACTORING_COMPLETE_2025-11-09.md) - Documentation refactoring example

**Skills this relies on**:
- [organize-agents](../organize-agents/SKILL.md) - Documentation organization
