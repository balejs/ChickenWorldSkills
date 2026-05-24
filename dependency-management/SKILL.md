---
name: dependency-management
description: Manage PlatformIO dependencies across ChickenWorld projects
---

# Skill: Dependency Management

**Purpose**: Manage PlatformIO dependencies and library.json updates

**Use when**: Adding, updating, or fixing library dependencies in ChickenWorld projects

**CRITICAL RULES**:
1. **ALWAYS** clean `.pio/libdeps/` after dependency changes
2. **ALWAYS** commit dependency changes to the dependency repo first
3. **ALWAYS** update library.json with correct version/branch
4. Test dependent projects after updating dependencies

**Workflow**:
```bash
# 1. Make changes in dependency repo (e.g., ChickenFundamentalsLib)
cd .pio/libdeps/native/ChickenFundamentalsLib
git add .
git commit -m "Fix bug"
git push origin main

# 2. Clean dependent project cache
cd ../ChickenNetworkingLib  # or any dependent project
rm -rf .pio/libdeps/

# 3. Rebuild to fetch fresh dependencies
pio test -e native

# 4. Or use ChickenTools for full validation
./ChickenWorld/ChickenTools/bin/build_and_test_all.py --incremental
```

**Key references**:
- [BUILD_PROCEDURES/PlatformIO_Dependency_Management.md](/Users/marco/devel/ChickenWorld/ChickenDocs/BUILD_PROCEDURES/PlatformIO_Dependency_Management.md) - Dependency management guide
- [BUILD_PROCEDURES/Fixing_Issues_In_Library_Dependencies.md](/Users/marco/devel/ChickenWorld/ChickenDocs/BUILD_PROCEDURES/Fixing_Issues_In_Library_Dependencies.md) - Fixing dependency issues
- [ChickenNetworkingLib/ChickenNetworkingLib_PROJECT_STRUCTURE.md](/Users/marco/devel/ChickenWorld/ChickenDocs/ChickenNetworkingLib/ChickenNetworkingLib_PROJECT_STRUCTURE.md) - Multi-repo structure
- [ChickenDocs/Common/CHICKENTOOLS.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/CHICKENTOOLS.md) - ChickenTools integration

**Common scenarios**:
- **Update dependency**: Push to dependency repo, clean `.pio/libdeps/`, rebuild
- **Test local changes**: Copy files to `.pio/libdeps/` for quick iteration
- **Production update**: Commit/push dependency, update library.json, test all dependents

**Skills this relies on**:
- [build-and-test-all](../build-and-test-all/SKILL.md) - Automated dependency validation
- [chickenworld-testing](../chickenworld-testing/SKILL.md) - Project testing
