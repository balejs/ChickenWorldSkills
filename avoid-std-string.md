# Skill: Avoid std::string

**Purpose**: Ensure ChickenWorld string types are used instead of std::string

**Use when**: Creating or modifying C++ code in ChickenWorld projects

**CRITICAL RULES**:
1. **NEVER** use std::string unless explicitly requested
2. **ALWAYS** use String, SBuffer, or Buffer instead
3. **ALWAYS** use MakeBaseString() for formatted strings
4. **NEVER** call std::remove() on ChickenWorld object paths

**Workflow**:
1. Use [SString](../ChickenFundamentalsLib/include/SString.h) / [String](../ChickenFundamentalsLib/include/String.h) for text
2. Use [Buffer](../ChickenFundamentalsLib/include/Buffer.h) / [SBuffer](../ChickenFundamentalsLib/include/SBuffer.h) for raw data
3. Use [MakeBaseString()](../ChickenFundamentalsLib/include/BaseString.h) for formatting
4. Read [FORMATTED_STRING_BEST_PRACTICES.md](../../ChickenDocs/Common/FORMATTED_STRING_BEST_PRACTICES.md)

**Key references**:
- [development_guidelines.md](../../ChickenDocs/development_guidelines.md#avoiding-stdstring) - Avoiding std::string rule
- [FORMATTED_STRING_BEST_PRACTICES.md](../../ChickenDocs/Common/FORMATTED_STRING_BEST_PRACTICES.md) - MakeBaseString usage
- [CHICKENWORLD_LIFECYCLE_MANAGEMENT.md](../../ChickenDocs/Common/CHICKENWORLD_LIFECYCLE_MANAGEMENT.md) - Lifecycle safety

**Skills this relies on**:
- [chickenworld-coding](chickenworld-coding.md) - General coding standards
