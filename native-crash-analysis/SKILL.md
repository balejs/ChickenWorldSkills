---
name: native-crash-analysis
description: Analyze native platform crashes and stack traces
---

# Skill: Native Crash Analysis

**Purpose**: Analyze native platform crashes using lldb/gdb

**Use when**: Tests crash on native platform (macOS/Linux desktop)

**CRITICAL RULES**:
1. **ALWAYS** get actual callstack before assumptions
2. **ALWAYS** document callstack in investigation notes
3. **ALWAYS** analyze actual frames, not assumptions
4. Use lldb (macOS) or gdb (Linux) consistently

**Workflow**:
```bash
# 1. Capture crash with full backtrace
lldb -o run -o "thread backtrace all" -o quit ./program

# 2. Document the actual crash location
# 3. Form hypothesis based on evidence
# 4. Verify fix by re-running tests
```

**Key references**:
- [development_guidelines.md](/Users/marco/devel/ChickenWorld/ChickenDocs/development_guidelines.md#when-debugging-crashes) - Callstack-first debugging
- [Debugging/FORENSIC_TECHNIQUES.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Debugging/FORENSIC_TECHNIQUES.md) - Forensic techniques
- [ChickenFundamentalsLib/INVESTIGATION_CHICKENPTR_LIFECYCLE_VALIDATION_2026-02-28.md](/Users/marco/devel/ChickenWorld/ChickenDocs/ChickenFundamentalsLib/INVESTIGATION_CHICKENPTR_LIFECYCLE_VALIDATION_2026-02-28.md) - Lifecycle investigation example

**Skills this relies on**:
- [chickenworld-testing](../chickenworld-testing/SKILL.md) - Native testing procedures
- [chickenworld-coding](../chickenworld-coding/SKILL.md) - Coding standards review
