---
name: cross-thread-safe-code
description: Write cross-thread safe code for ESP32 and native platforms
---

# Skill: Cross-Thread Safe Code

**Purpose**: Write code safe for multi-threaded ESP32 environments

**Use when**: Creating classes that may be called from multiple threads (LWIP callbacks, timers, etc.)

**CRITICAL RULES**:
1. **ALWAYS** pass explicit LoopScheduler parameter for cross-thread calls
2. **NEVER** rely solely on thread_local storage for cross-thread safety
3. **ALWAYS** use weakPtr() for callbacks to prevent use-after-free
4. **ALWAYS** use shared_ptr instead of raw pointers for shared ownership

**Workflow**:
1. Read [ARCHITECTURAL_PATTERNS.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/ARCHITECTURAL_PATTERNS.md#cross-thread-safe-scheduler-passing)
2. Check [ESP32_PLATFORM_DIFFERENCES.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/ESP32_PLATFORM_DIFFERENCES.md)
3. Review [ChickenSpaceTimeLib/INVESTIGATION_ESP32DEV_CRASH_2026-05-03.md](/Users/marco/devel/ChickenWorld/ChickenDocs/ChickenSpaceTimeLib/INVESTIGATION_ESP32DEV_CRASH_2026-05-03.md)
4. Implement explicit scheduler parameter pattern

**Key references**:
- [ARCHITECTURAL_PATTERNS.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/ARCHITECTURAL_PATTERNS.md) - Cross-thread safe scheduler passing
- [ESP32_PLATFORM_DIFFERENCES.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/ESP32_PLATFORM_DIFFERENCES.md) - Thread model differences
- [CHICKENWORLD_LIFECYCLE_MANAGEMENT.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/CHICKENWORLD_LIFECYCLE_MANAGEMENT.md) - Lifecycle safety

**Skills this relies on**:
- [chickenworld-coding](../chickenworld-coding/SKILL.md) - General coding standards
- [chickenworld-testing](../chickenworld-testing/SKILL.md) - Test cross-thread safety
