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
6. **Default to Python 3; shell is the exception and needs a reason.** Anything with a loop, a
   branch, or more than ~5 lines is Python. Shell only for: (a) mutating the caller's
   environment (`source`, `export`, `cd`), (b) a literal 1–3 command invocation with no
   branching, (c) job/signal control (`trap`, `wait`), (d) a `/bin/sh` toolchain hook we
   can't change. Never Perl, Ruby, PHP or node unless Marco explicitly asks.
   See ChickenDocs → *Scripting Language Convention*.

## Scripting

Scripts live in `ChickenTools/bin/*.py` (workspace-wide) or `<project>/*.py` (project-local,
like `classify_failures.py`). **Python is the default** — see critical rule 6 for the only
four cases where shell is legitimate.

Express ordered decision logic as a **named list of rules, each carrying its own rationale**,
not as a compact `if/elsif` chain with the explanation in a comment 50 lines away. The reader
has to be able to see *why* a gate sits where it sits at the point of decision.

Always give a shebang (`#!/usr/bin/env python3`) and `chmod +x` — a script without one runs
under `sh` when invoked directly, which is how `classify_failures.pl` failed on 2026-11-06.

Parse device logs in Python (`open(p,"rb").read().decode("utf-8","replace")`), not shell
`grep`: NUL bytes make plain `grep` silently return nothing.

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
