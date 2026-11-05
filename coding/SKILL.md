---
name: coding
description: ChickenWorld C++ coding standards - string types, logging macros, lifecycle ownership, schedulers
---

# Skill: Coding Standards

**Purpose**: Write C++ that matches ChickenWorld conventions

**Use when**: Writing or reviewing any ChickenWorld C++

**Last Updated**: 2026-11-05

Merges `chickenworld-coding` and `avoid-std-string` - the latter restated rule 1 below
and nothing else.

---

## CRITICAL RULES

1. **NEVER** use `std::string` unless explicitly asked. Use `String` / `SString` for text
   and `Buffer` / `SBuffer` for raw bytes; format with `MakeBaseString()`
2. **NEVER** call `std::remove()` on a path holding a ChickenWorld object - it bypasses
   lifecycle and leaves the allocator inconsistent
3. **ALWAYS** use the ChickenWorld logging macros (`_debug`, `_info`, `_warning`, `_error`)
   and never `std::cout` / `std::cerr`
4. **ALWAYS** let `ChickenPtr` own lifetime - never `delete` manually
5. **ALWAYS** pass an explicit `LoopScheduler` into anything that may run cross-thread
   (see cross-thread-safe-code)

## Types

Public surface is the umbrella header `ChickenFundamentalsLib/include/Buffering.h`; the
concrete classes live under `src/Buffering/`.

```cpp
#include <Buffering.h>

SString    text   = MakeBaseString("connected to %s:%d", host, port);
SBuffer    raw    = MakeBuffer(data, len);
```

## Workflow

1. Read [FORMATTED_STRING_BEST_PRACTICES.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/FORMATTED_STRING_BEST_PRACTICES.md)
2. Read [CHICKENWORLD_LIFECYCLE_MANAGEMENT.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/CHICKENWORLD_LIFECYCLE_MANAGEMENT.md)
3. Check [ESP32_PLATFORM_DIFFERENCES.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/ESP32_PLATFORM_DIFFERENCES.md) for platform-specific code
4. For cross-thread work, read [ARCHITECTURAL_PATTERNS.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/ARCHITECTURAL_PATTERNS.md)
5. When modifying a dependency, follow [DEPENDENCY_MODIFICATION_WORKFLOW.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/DEPENDENCY_MODIFICATION_WORKFLOW.md)

**Key references**:
- [development_guidelines.md](/Users/marco/devel/ChickenWorld/ChickenDocs/development_guidelines.md) - Tokenizer use, avoiding std::string
- [LOGGING_BEST_PRACTICES.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/LOGGING_BEST_PRACTICES.md) - Logging macros and setup

**Skills this relies on**:
- [chickenworld-testing](../chickenworld-testing/SKILL.md) - Verify what you wrote
- [cross-thread-safe-code](../cross-thread-safe-code/SKILL.md) - Multi-threaded safety
