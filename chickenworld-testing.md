# Skill: ChickenWorld Testing

**Purpose**: Follow ChickenWorld testing procedures and best practices

**Use when**: Testing any ChickenWorld library or application

**CRITICAL RULES**:
1. **ALWAYS** use testing tools (build_and_test_all.py, test_esp32_crash_repeat.py)
2. **ALWAYS** enable verbose logging (-vvv) for ESP32 tests
3. **ALWAYS** use crash detection scripts for ESP32 tests that may crash/reboot
4. **NEVER** run pio test directly for crash-prone tests

**Workflow**:
1. Read [ChickenTools/QUICK_REFERENCE.md](../../ChickenTools/QUICK_REFERENCE.md)
2. Check [ChickenDocs/Common/TESTING_QUICK_REFERENCE.md](../../ChickenDocs/Common/TESTING_QUICK_REFERENCE.md)
3. Review [Debugging/ESP32_Testing_Procedures.md](../../ChickenDocs/Debugging/ESP32_Testing_Procedures.md)
4. Run tests with appropriate flags

**Key references**:
- [ChickenTools/README.md](../../ChickenTools/README.md) - ChickenTools overview
- [ChickenDocs/Common/CHICKENTOOLS.md](../../ChickenDocs/Common/CHICKENTOOLS.md) - build_and_test_all.py usage
- [ChickenDocs/Common/TESTING_REMINDERS.md](../../ChickenDocs/Common/TESTING_REMINDERS.md) - Testing reminders
- [BUILD_PROCEDURES/README.md](../../ChickenDocs/BUILD_PROCEDURES/README.md) - Build procedures

**Skills this relies on**:
- [build-and-test-all](build-and-test-all.md) - Automated test runner
- [esp32-crash-analysis](esp32-crash-analysis.md) - ESP32 crash analysis
