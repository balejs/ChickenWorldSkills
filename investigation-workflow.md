# Skill: Investigation Workflow

**Purpose**: Follow systematic investigation workflow for bugs/crashes in ChickenWorld projects

**Use when**: Investigating unexpected behavior, crashes, or bugs

**CRITICAL RULES**:
1. **ALWAYS** get callstack before assumptions
2. **ALWAYS** look at similar ChickenWorld code first
3. **ALWAYS** document investigation process
4. **ALWAYS** verify fix with multiple iterations (for crashes: 20 runs, 0 crashes)

**Workflow**:
```bash
# Phase 1: Reproduce
# Get callstack: lldb -o run -o "thread backtrace all" -o quit ./program
# Document: Save to investigation/INVESTIGATION_YYYY-MM-DD.md

# Phase 2: Research
# Search ChickenDocs for similar issues
# Check test code for working patterns

# Phase 3: Hypothesize
# Form hypothesis based on evidence
# Design minimal test case

# Phase 4: Fix
# Implement minimal change
# Document changes in investigation doc

# Phase 5: Verify
# Run 20 iterations: test_esp32_crash_repeat.py -n 20
# 0 crashes = fix verified
```

**Key references**:
- [ChickenDocs/INVESTIGATION_PROCEDURE.md](../../ChickenDocs/INVESTIGATION_PROCEDURE.md) - Complete investigation procedure
- [ChickenDocs/Debugging/DEBUGGING_WORKFLOW_LESSONS.md](../../ChickenDocs/Debugging/DEBUGGING_WORKFLOW_LESSONS.md) - Debugging lessons
- [ChickenDocs/Debugging/FORENSIC_TECHNIQUES.md](../../ChickenDocs/Debugging/FORENSIC_TECHNIQUES.md) - Forensic techniques
- [ChickenDocs/development_guidelines.md](../../ChickenDocs/development_guidelines.md) - When debugging crashes, when fixing issues

**Investigation structure**:
1. Problem statement
2. Reproduction steps
3. Callstack and logs
4. Research and similar patterns
5. Hypothesis
6. Fix implementation
7. Verification results

**Skills this relies on**:
- [native-crash-analysis](native-crash-analysis.md) - Native crash analysis
- [esp32-crash-analysis](esp32-crash-analysis.md) - ESP32 crash analysis
- [chickenworld-testing](chickenworld-testing.md) - Testing procedures
