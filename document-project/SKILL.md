---
name: document-project
description: Create and document a ChickenWorld project - scaffolding, header API docs and verification
---

# Skill: Document Project

**Purpose**: Take a project from empty directory to documented and verified

**Use when**: Starting a new library, or documenting/auditing an existing one

**Last Updated**: 2026-11-05

Merges `document-project`, `verify-api-documentation` and `new-chickenworld-project` -
verification is a phase of documenting, and scaffolding decides what gets documented.

---

## CRITICAL RULES

1. **ALWAYS** follow `PROJECT_DOCUMENTATION_BLUEPRINT.md`; it defines the phases, this does not
2. **ALWAYS** create `<Project>_PROJECT_STRUCTURE.md` for multi-repo projects
3. **ALWAYS** document **every** header, public in `include/` and internal in `src/`
4. **ALWAYS** verify documentation against the implementation - a doc that describes a
   signature the code does not have is a defect, not a draft
5. **NEVER** put architecture prose in headers - `@file` blocks stay ≤15 lines with `@see`
   pointers to ChickenDocs
6. **ALWAYS** name investigation documents `<TOPIC>_<YYYY-MM-DD>.md` - topic first, matching
   the ~160 existing files; date-first names are not used here

## Scaffolding

```
NewLibrary/
├── include/NewLibrary.h     # public API, slim @file blocks
├── src/NewLibrary.cpp
├── test/test.cpp            # plus test_server.py if the tests need one
├── platformio.ini           # native + esp32dev environments
├── library.json             # metadata and dependencies
└── docs -> ChickenDocs/NewLibrary/
```

## Workflow

1. **Scaffold** the layout above; add `platformio.ini` with both environments and
   `library.json` with dependencies
2. **Inventory** - `find include src -name "*.h"` and record every undocumented header in
   `ChickenDocs/<Project>/API_DOCUMENTATION_VERIFICATION.md`
3. **Document** - `@file` ≤15 lines, `@param` and `@return` on every public function
4. **Verify against code** - cross-check each claim against the `.cpp`; fix discrepancies in
   the doc, and confirm inline examples actually compile
5. **Structure** - architecture to `ChickenDocs/<Project>/Architecture/*.md`, findings to
   `ChickenDocs/<Project>/<TOPIC>_<YYYY-MM-DD>.md`
6. **Wire in** - link from `AGENTS.md` and `ChickenDocs/README.md` so it is discoverable

## Verification checklist

- [ ] Every header in `include/` and `src/` has an `@file` block ≤15 lines
- [ ] Every public class and function has `@param` / `@return`
- [ ] Inline examples compile and were actually run
- [ ] Documentation matches the implementation, not the intention
- [ ] Architecture detail lives in ChickenDocs, not in headers
- [ ] New docs are linked from an index

---

**Key references**:
- [PROJECT_DOCUMENTATION_BLUEPRINT.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/Documentation/Process/PROJECT_DOCUMENTATION_BLUEPRINT.md) - The blueprint
- [PROJECT_DOCUMENTATION_PROCESS.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/Documentation/Process/PROJECT_DOCUMENTATION_PROCESS.md) - Phase detail
- [API_DOCUMENTATION_GUIDELINES.md](/Users/marco/devel/ChickenWorld/ChickenDocs/API_DOCUMENTATION_GUIDELINES.md) - Doxygen standards
- [INLINE_EXAMPLE_GUIDELINES.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/Documentation/Guidelines/INLINE_EXAMPLE_GUIDELINES.md) - Example code
- [DOCUMENTATION_VERIFICATION_QUALITY_PROCESS.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/Documentation/Process/DOCUMENTATION_VERIFICATION_QUALITY_PROCESS.md) - Verification
- [ChickenNetworkingLib_PROJECT_STRUCTURE.md](/Users/marco/devel/ChickenWorld/ChickenDocs/ChickenNetworkingLib/ChickenNetworkingLib_PROJECT_STRUCTURE.md) - Structure template

**Skills this relies on**:
- [document-project-docs](../document-project-docs/SKILL.md) - Where project content goes
- [organize-agents](../organize-agents/SKILL.md) - AGENTS.md organisation
- [documentation-maintenance](../documentation-maintenance/SKILL.md) - The three principles
