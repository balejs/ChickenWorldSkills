---
name: dependency-management
description: Manage PlatformIO dependencies across ChickenWorld repos - keep .pio/libdeps in sync without wiping the cache
---

# Skill: Dependency Management

**Purpose**: Keep vendored dependencies correct in both direction - source of truth and
local cache

**Use when**: Adding, updating or debugging a library dependency, or when a build behaves
like it is using stale code

**Last Updated**: 2026-11-05

---

## CRITICAL RULES

1. **NEVER** edit a library under `.pio/libdeps/` on a release branch. Create a dedicated
   testing branch in that library's own repo first, and commit there
2. **NEVER** commit library changes into the consuming project - they belong to the
   dependency's repository
3. **ALWAYS** land the change in the dependency repo before updating anything that consumes it
4. **ALWAYS** update `library.json` / `platformio.ini` to the version or tag you intend, and
   pin it - a floating branch silently changes under you
5. **NEVER** blanket-delete `.pio/libdeps/` - see the sync rule below
6. **ALWAYS** re-verify consumers after a dependency change; a bump that compiles the
   dependency may still break the caller

## The `.pio/libdeps` sync rule

The goal is **freshness**, not emptiness. Deleting the whole cache throws away work that
has not been pushed and costs a full re-resolve of every library.

```bash
# Check every vendored lib: where is it, and is it clean?
for d in .pio/libdeps/*/; do
  for l in "$d"*/; do
    [ -d "$l/.git" ] || continue
    printf "%-34s %-46s %s\n" "${l#".pio/libdeps/"}" \
      "$(git -C "$l" branch --show-current)" \
      "$(git -C "$l" status --porcelain | wc -l | tr -d ' ') dirty"
  done
done
```

Act on what that reports:

| State | Action |
|---|---|
| Clean, on the pinned ref, up to date | **Do nothing** - the cache is correct |
| Clean, behind its remote | `git -C <lib> pull --ff-only` |
| **Dirty** | **STOP** - uncommitted edits exist. Commit them to a testing branch in that lib's repo before touching the cache |
| On a release branch with probe lines | Move to a testing branch first |
| Stale cache giving unexplained behaviour | Remove **only that library's** directory, not the tree |

Only remove a single library directory, and only after confirming it holds no uncommitted
work:

```bash
git -C .pio/libdeps/esp32dev/ChickenHttpLib status --porcelain   # must be empty
rm -rf .pio/libdeps/esp32dev/ChickenHttpLib
pio update -e esp32dev
```

## Workflow

1. **Change the dependency in its own repo**, on a testing branch if it is instrumentation
   (`investigation/<yymmddHHMM>-<topic>`)
2. **Commit and push** there, then tag or merge to the release ref when it is proven
3. **Update the consumer** - point `platformio.ini` / `library.json` at the new tag
4. **Refresh only what changed** - `pio update -e <env>`, or delete that one lib directory
5. **Verify consumers** - `pio test -e native`, then the ESP32 environment

```bash
# Full cross-project validation
~/devel/ChickenWorld/ChickenTools/bin/build_and_test_all.py --incremental
```

---

**Key references**:
- [PlatformIO_Dependency_Management.md](/Users/marco/devel/ChickenWorld/ChickenDocs/BUILD_PROCEDURES/PlatformIO_Dependency_Management.md) - Dependency management guide
- [Fixing_Issues_In_Library_Dependencies.md](/Users/marco/devel/ChickenWorld/ChickenDocs/BUILD_PROCEDURES/Fixing_Issues_In_Library_Dependencies.md) - Fixing dependency issues
- [DEPENDENCY_MODIFICATION_WORKFLOW.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/DEPENDENCY_MODIFICATION_WORKFLOW.md) - Modifying vendored code
- [ChickenNetworkingLib_PROJECT_STRUCTURE.md](/Users/marco/devel/ChickenWorld/ChickenDocs/ChickenNetworkingLib/ChickenNetworkingLib_PROJECT_STRUCTURE.md) - Multi-repo structure

**Skills this relies on**:
- [git-investigation-branches](../git-investigation-branches/SKILL.md) - Testing branch requirement
- [build-and-test-all](../build-and-test-all/SKILL.md) - Cross-project validation
- [chickenworld-testing](../chickenworld-testing/SKILL.md) - Project testing
