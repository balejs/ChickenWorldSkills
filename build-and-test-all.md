# Skill: Build and Test All

**Purpose**: Use ChickenTools build_and_test_all.py for comprehensive validation

**Use when**: Testing multiple ChickenWorld projects or validating changes across dependencies

**CRITICAL RULES**:
1. **ALWAYS** use incremental mode (`--incremental`) for development
2. **ALWAYS** test on target environment (native or esp32dev)
3. **ALWAYS** review dependency tree before major changes
4. Generate HTML reports for detailed analysis

**Workflow**:
```bash
# 1. Test all projects on main branch (native)
./bin/build_and_test_all.py

# 2. Incremental test - only changed projects + dependents
./bin/build_and_test_all.py --incremental

# 3. Test on ESP32 hardware
./bin/build_and_test_all.py --env esp32dev --branch 1.1.0

# 4. Generate dependency visualization
./bin/build_and_test_all.py --deps-html
```

**Key references**:
- [ChickenTools/README.md](../../ChickenTools/README.md) - Complete tool guide
- [ChickenDocs/Common/CHICKENTOOLS.md](../../ChickenDocs/Common/CHICKENTOOLS.md) - Documentation reference
- [ChickenTools/QUICK_REFERENCE.md](../../ChickenTools/QUICK_REFERENCE.md) - Quick command reference
- [BUILD_PROCEDURES/PlatformIO_Dependency_Management.md](../../ChickenDocs/BUILD_PROCEDURES/PlatformIO_Dependency_Management.md) - Dependency handling

**Options summary**:
- `-i, --incremental` - Only test changed projects and dependents
- `-e, --env` - Environment (native/esp32dev/all)
- `-b, --branch` - Branch or tag to test
- `--deps-html` - Generate interactive HTML dependency graph

**Skills this relies on**:
- [chickenworld-testing](chickenworld-testing.md) - Testing procedures
- [dependency-management](dependency-management.md) - Dependency handling
