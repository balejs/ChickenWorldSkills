---
name: git-commit-conventions
description: Write ChickenWorld commit messages - component prefixes, atomic commits, no AI references
---

# Skill: Git Commit Conventions

**Purpose**: Write commits that are atomic, correctly prefixed and human-authored

**Use when**: Committing anything to a ChickenWorld repository

**Last Updated**: 2026-11-05

Split from `chickenworld-git-workflow`.

**CRITICAL RULES**:
1. **NEVER** reference AI tools in commit messages - write as a human developer
2. **ALWAYS** use the `<component>: <summary>` form
3. **ALWAYS** keep a commit to one logical change
4. **ALWAYS** separate code and documentation into distinct commits
5. **ALWAYS** check `git diff --cached --stat` before committing - `git add <file>` stages
   every pre-existing change to that file, including deletions made earlier in the session

---

## Commit Message Format

### Structure
```
<component>: <brief summary>

<optional detailed description>

<optional footer with issue references>
```

### Component Names
Use the **object or component being modified** as the preamble:
- `ReferenceCounter:` - Changes to reference counting
- `LoopScheduler:` - Changes to scheduler
- `HttpExchange:` - Changes to HTTP exchange
- `Buffer:` - Changes to buffer implementation
- `Generic:` - Multiple components or general changes

### Modular Commit Principle
**Prioritize atomic, focused commits**:
1. **Break down large changes** - If a change touches multiple independent areas, split into separate commits
2. **Functionally grouped changes** - Changes that must stay together (e.g., API change + usage updates) can be in one commit
3. **Never mix source with non-source** - Code changes must be isolated from docs/config/documentation changes

### Separation Rules

**Must be separate commits**:
- **Source code** (`src/`, `include/`) → One commit
- **Documentation** (`ChickenDocs/`, `docs/`) → Separate commit
- **Configuration** (`platformio.ini`, `.gitignore`, etc.) → Separate commit
- **AGENTS.md or README.md** → Separate commit

**Good practice** (can be together):
```
Commit 1: ReferenceCounter: Add mutex protection
         - src/ReferenceCounter.cpp: Add mutex lock
         - include/ReferenceCounter.h: Add lock/unlock methods

Commit 2: docs: Document ReferenceCounter thread safety
         - ChickenDocs/Common/CHICKENWORLD_LIFECYCLE_MANAGEMENT.md

Commit 3: platformio.ini: Enable lifecycle checks
         - platformio.ini: Add build_flag
```

**Bad practice** (should be split):
```
❌ ONE COMMIT:
   - src/ReferenceCounter.cpp: Add mutex lock
   - include/ReferenceCounter.h: Add methods
   - ChickenDocs/Common/CHICKENWORLD_LIFECYCLE_MANAGEMENT.md: Document thread safety
   - platformio.ini: Add build_flag
```

### Examples

**Good commits** (modular, focused):
```
ReferenceCounter: Add mutex protection to helper functions

The addStrongRef and releaseRef functions were missing mutex
protection, leading to race conditions in multi-threaded scenarios.
Added Lock/NoLock versions to allow internal callers to skip locking.

Closes #123
```

```
LoopScheduler: Remove Weakling dependency

Eliminated Weakling reference from LoopScheduler to reduce
stack usage and improve performance. Weakling usage moved
to private implementations only.
```

```
ChickenHttpLib: Update to use new NetworkExchange API

Updated HttpClient to use NetworkExchange instead of SQuery.
All call sites migrated to new factory methods.
```

**Bad commits** (avoid these):
```
update ReferenceCounter with mutex                # Too vague
referencecounter: add mutex and update docs and fix config  # Mixed concerns
AI suggested this fix                             # References AI
```

---


---

**Key references**:
- [GIT_COMMIT_GUIDELINES.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/GIT_COMMIT_GUIDELINES.md) - Commit format and rules

**Skills this relies on**:
- [git-investigation-branches](../git-investigation-branches/SKILL.md) - Squash and merge procedure
