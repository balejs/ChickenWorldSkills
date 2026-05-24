---
name: new-chickenworld-project
description: Create new ChickenWorld projects with proper structure
---

# Skill: New ChickenWorld Project

**Purpose**: Create new ChickenWorld library projects with proper structure

**Use when**: Starting a new ChickenWorld library or component

**CRITICAL RULES**:
1. **ALWAYS** use standard directory layout (include/, src/, test/, docs/)
2. **ALWAYS** create platformio.ini with native and esp32dev environments
3. **ALWAYS** follow PROJECT_DOCUMENTATION_BLUEPRINT.md for documentation
4. **ALWAYS** document project structure in ChickenDocs/[ProjectName]/

**Project structure**:
```
NewLibrary/
├── include/
│   └── NewLibrary.h          # Public API with slim @file blocks
├── src/
│   └── NewLibrary.cpp         # Implementation
├── test/
│   └── test.cpp              # Unit tests with test_server.py if needed
├── platformio.ini            # Native + esp32dev environments
├── library.json              # Library metadata and dependencies
└── docs/                     # Symlink to ChickenDocs/NewLibrary/
```

**ChickenDocs/NewLibrary/**:
- ChickenDocs/NewLibrary_PROJECT_STRUCTURE.md
- API_DOCUMENTATION_VERIFICATION.md
- Architecture/*.md (if complex)
- INVESTIGATION_*.md (as needed)

**Key references**:
- [Common/Documentation/Process/PROJECT_DOCUMENTATION_BLUEPRINT.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/Documentation/Process/PROJECT_DOCUMENTATION_BLUEPRINT.md) - Project blueprint
- [ChickenNetworkingLib/ChickenNetworkingLib_PROJECT_STRUCTURE.md](/Users/marco/devel/ChickenWorld/ChickenDocs/ChickenNetworkingLib/ChickenNetworkingLib_PROJECT_STRUCTURE.md) - Project template
- [ChickenSpaceTimeLib/ChickenSpaceTimeLib_PROJECT_STRUCTURE.md](/Users/marco/devel/ChickenWorld/ChickenDocs/ChickenSpaceTimeLib/ChickenSpaceTimeLib_PROJECT_STRUCTURE.md) - ESP project template
- [ChickenFundamentalsLib/REFACTORING_COMPLETE_2025-11-09.md](/Users/marco/devel/ChickenWorld/ChickenDocs/ChickenFundamentalsLib/REFACTORING_COMPLETE_2025-11-09.md) - Documentation refactoring

**Initial setup steps**:
1. Create directory structure
2. Add platformio.ini with native + esp32dev
3. Create library.json with dependencies
4. Add README.md with overview
5. Set up ChickenDocs/NewLibrary/ folder
6. Write initial API documentation in headers

**Skills this relies on**:
- [document-project](../document-project/SKILL.md) - Project documentation
- [chickenworld-coding](../chickenworld-coding/SKILL.md) - Coding standards
