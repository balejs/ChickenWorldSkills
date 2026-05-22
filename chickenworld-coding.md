# Skill: ChickenWorld Coding Standards

**Purpose**: Enforce ChickenWorld coding standards and best practices

**Use when**: Writing or reviewing any ChickenWorld C++ code

**CRITICAL RULES**:
1. **NEVER** use std::string - use String, SBuffer, Buffer instead
2. **ALWAYS** use ChickenWorld logging macros (_debug, _info, _error, etc.)
3. **ALWAYS** let ChickenPtr manage lifecycle - never delete objects manually
4. **ALWAYS** pass explicit scheduler for cross-thread code
5. **ALWAYS** use MakeBaseString() for formatted strings

**Workflow**:
1. Read [FORMATTED_STRING_BEST_PRACTICES.md](../../ChickenDocs/Common/FORMATTED_STRING_BEST_PRACTICES.md)
2. Review [CHICKENWORLD_LIFECYCLE_MANAGEMENT.md](../../ChickenDocs/Common/CHICKENWORLD_LIFECYCLE_MANAGEMENT.md)
3. Check [ESP32_PLATFORM_DIFFERENCES.md](../../ChickenDocs/Common/ESP32_PLATFORM_DIFFERENCES.md) for platform-specific code
4. Review [ARCHITECTURAL_PATTERNS.md](../../ChickenDocs/Common/ARCHITECTURAL_PATTERNS.md) for cross-thread patterns

**Key references**:
- [development_guidelines.md](../../ChickenDocs/development_guidelines.md) - Tokenizer optimization, avoid std::string
- [LOGGING_BEST_PRACTICES.md](../../ChickenDocs/Common/LOGGING_BEST_PRACTICES.md) - Logging macros and setup
- [FORMATTED_STRING_BEST_PRACTICES.md](../../ChickenDocs/Common/FORMATTED_STRING_BEST_PRACTICES.md) - MakeBaseString usage
- [CHICKENWORLD_LIFECYCLE_MANAGEMENT.md](../../ChickenDocs/Common/CHICKENWORLD_LIFECYCLE_MANAGEMENT.md) - Lifecycle management
- [ARCHITECTURAL_PATTERNS.md](../../ChickenDocs/Common/ARCHITECTURAL_PATTERNS.md) - Cross-thread safe patterns

**Skills this relies on**:
- [chickenworld-testing](chickenworld-testing.md) - Verify code works correctly
- [cross-thread-safe-code](cross-thread-safe-code.md) - Multi-threaded safety
