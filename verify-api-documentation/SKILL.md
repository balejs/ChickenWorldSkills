---
name: verify-api-documentation
description: Verify API documentation follows ChickenWorld standards
---

# Skill: Verify API Documentation

**Purpose**: Verify API documentation completeness and accuracy

**Use when**: Reviewing or updating API documentation in ChickenWorld headers

**CRITICAL RULES**:
1. **ALWAYS** verify documentation against actual implementation
2. **ALWAYS** document ALL parameters, return values, and edge cases
3. **ALWAYS** keep @file blocks slim (≤15 lines) with @see references
4. **ALWAYS** verify inline examples compile and work correctly

**Workflow**:
1. Scan ALL headers (public in include/, internal in src/)
2. For each header, verify:
   - Has @file block ≤15 lines with context
   - All classes/functions documented
   - Parameters documented with @param
   - Return values documented with @return
   - Inline examples are short and accurate
3. Cross-check documentation vs implementation (.cpp files)
4. Fix any discrepancies

**Key references**:
- [API_DOCUMENTATION_GUIDELINES.md](/Users/marco/devel/ChickenWorld/ChickenDocs/API_DOCUMENTATION_GUIDELINES.md) - Doxygen standards
- [Common/Documentation/Guidelines/INLINE_EXAMPLE_GUIDELINES.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/Documentation/Guidelines/INLINE_EXAMPLE_GUIDELINES.md) - Example code guidelines
- [Common/Documentation/Process/DOCUMENTATION_VERIFICATION_QUALITY_PROCESS.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/Documentation/Process/DOCUMENTATION_VERIFICATION_QUALITY_PROCESS.md) - Verification process
- [ChickenFundamentalsLib/EXAMPLE_VERIFICATION_COMPLETE_2025-11-10.md](/Users/marco/devel/ChickenWorld/ChickenDocs/ChickenFundamentalsLib/EXAMPLE_VERIFICATION_COMPLETE_2025-11-10.md) - Example verification

**Quality checklist**:
- ✅ All headers have @file documentation
- ✅ All classes/functions documented
- ✅ Examples compile and verified
- ✅ Documentation matches implementation
- ✅ Typos and formatting fixed

**Skills this relies on**:
- [document-project](../document-project/SKILL.md) - Project documentation workflow
