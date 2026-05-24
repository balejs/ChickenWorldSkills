---
name: esp32-heap-debugging
description: Debug heap poisoning issues on ESP32
---

# Skill: ESP32 Heap Debugging

**Purpose**: Debug ESP32 heap poisoning and memory corruption issues

**Use when**: ESP32 shows heap corruption, memory poisoning, or Watchdog Timer (WDT) resets

**CRITICAL RULES**:
1. **ALWAYS** use heap tracing and crash detection scripts
2. **ALWAYS** enable heap poisoning for debugging (`CONFIG(heap_poisoning)`)
3. **ALWAYS** capture full crash logs before analysis
4. **NEVER** ignore memory corruption warnings

**Workflow**:
```bash
# 1. Enable heap poisoning in menuconfig
idf.py fullclean
idf.py build

# 2. Run crash test with monitoring
./ChickenWorld/ChickenTools/bin/test_esp32_crash_repeat.py -n 20

# 3. Parse watchdog crash log
./ChickenWorld/ChickenTools/bin/parse_watchdog_crash_log.py crash.log

# 4. Analyze heap corruption patterns
```

**Key references**:
- [ChickenTools/bin/parse_watchdog_crash_log.py](../../ChickenTools/bin/parse_watchdog_crash_log.py) - Watchdog log parser
- [Debugging/ESP32_Heap_Poisoning_Guide.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Debugging/ESP32_Heap_Poisoning_Guide.md) - Heap debugging guide
- [ChickenHttpLib_Heap_Poisoning_Investigation.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Debugging/ChickenHttpLib_Heap_Poisoning_Investigation.md) - Real case study
- [Debugging/ESP32_Testing_Procedures.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Debugging/ESP32_Testing_Procedures.md) - Testing procedures

**Common causes**:
- Buffer overflow/underflow
- Use-after-free
- Double free
- Stack overflow
- Race conditions with shared memory

**Skills this relies on**:
- [esp32-crash-analysis](../esp32-crash-analysis/SKILL.md) - Crash analysis workflow
- [chickenworld-testing](../chickenworld-testing/SKILL.md) - ESP32 testing procedures
