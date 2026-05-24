---
name: esp32-crash-analysis
description: Analyze ESP32 crashes using structured debugging techniques
---

# Skill: ESP32 Crash Analysis

**Purpose**: Analyze and fix ESP32 crashes, Guru Meditation errors, aborts

**Use when**: ESP32 crashes, reboots unexpectedly, or shows Guru Meditation errors

**CRITICAL RULES**:
1. **ALWAYS** use [test_esp32_crash_repeat.py](../../ChickenTools/bin/test_esp32_crash_repeat.py) for crash analysis
2. **ALWAYS** decode backtraces with [decode_callstack.py](../../ChickenTools/bin/decode_callstack.py)
3. **NEVER** run pio test directly for crash-prone tests (device reboots forever)
4. **ALWAYS** capture full crash logs before debugging

**Workflow**:
1. Run crash test: `test_esp32_crash_repeat.py -n 20`
2. Decode backtrace: `decode_callstack.py firmware.elf --file crash.log`
3. Analyze crash location and root cause
4. Verify fix with repeated testing (20 iterations, 0 crashes)

**Key references**:
- [ChickenTools/QUICK_REFERENCE.md](../../ChickenTools/QUICK_REFERENCE.md) - Quick reference
- [Debugging/ESP32_Testing_Procedures.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Debugging/ESP32_Testing_Procedures.md) - ESP32 testing procedures
- [Debugging/FORENSIC_TECHNIQUES.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Debugging/FORENSIC_TECHNIQUES.md) - Forensic techniques
- [ChickenFundamentalsLib/INVESTIGATION_CHICKENPTR_LIFECYCLE_VALIDATION_2026-02-28.md](/Users/marco/devel/ChickenWorld/ChickenDocs/ChickenFundamentalsLib/INVESTIGATION_CHICKENPTR_LIFECYCLE_VALIDATION_2026-02-28.md) - ChickenPtr crash investigation

**Skills this relies on**:
- [callstack-decoding](../callstack-decoding/SKILL.md) - Decode crash backtraces
- [chickenworld-testing](../chickenworld-testing/SKILL.md) - Testing procedures
