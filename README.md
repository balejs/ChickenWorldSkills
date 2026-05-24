# ChickenWorld Skills

**Purpose**: Collection of AI agent skills for ChickenWorld development workflows

**Location**: Skills are loaded from `~/.opencode/skills/`

**Repository**: `~/devel/ChickenWorld/ChickenWorldSkills/` (clone of active skills)

---

## Overview

This repository contains **20 skills** that enforce ChickenWorld coding standards, testing procedures, and best practices across all projects.

Skills follow **Option B** format:
- 10-15 lines with workflow + links
- Integration with ChickenTools where applicable
- References to detailed ChickenDocs documentation

**Key Principle**: All detailed documentation must exist in ChickenDocs first

---

## Skills Catalog

### 🎯 Universal Development Skills

| Skill | Purpose |
|-------|---------|
| [chickenworld-coding](chickenworld-coding/SKILL.md) | Enforce ChickenWorld coding standards |
| [chickenworld-testing](chickenworld-testing/SKILL.md) | Follow testing procedures |
| [build-and-test-all](build-and-test-all/SKILL.md) | Use ChickenTools automation |
| [cross-thread-safe-code](cross-thread-safe-code/SKILL.md) | Write cross-thread safe code |

### 🐛 Crash Analysis & Debugging

| Skill | Purpose |
|-------|---------|
| [esp32-crash-analysis](esp32-crash-analysis/SKILL.md) | Analyze ESP32 crashes |
| [native-crash-analysis](native-crash-analysis/SKILL.md) | Analyze native crashes |
| [callstack-decoding](callstack-decoding/SKILL.md) | Decode ESP32 backtraces |
| [esp32-heap-debugging](esp32-heap-debugging/SKILL.md) | Debug heap poisoning |
| [investigation-workflow](investigation-workflow/SKILL.md) | Systematic investigation |

### 🔧 Networking & TLS

| Skill | Purpose |
|-------|---------|
| [tls-debugging](tls-debugging/SKILL.md) | Debug TLS/HTTPS issues |
| [networking-debugging](networking-debugging/SKILL.md) | Debug networking issues |

### 📝 Documentation

| Skill | Purpose |
|-------|---------|
| [document-project](document-project/SKILL.md) | Document new projects |
| [verify-api-documentation](verify-api-documentation/SKILL.md) | Verify API documentation |
| [document-project-docs](document-project-docs/SKILL.md) | Document project-specific details |

### 🏗️ Project Management

| Skill | Purpose |
|-------|---------|
| [new-chickenworld-project](new-chickenworld-project/SKILL.md) | Create new projects |
| [dependency-management](dependency-management/SKILL.md) | Manage dependencies |

### 🗂️ Organization

| Skill | Purpose |
|-------|---------|
| [organize-agents](organize-agents/SKILL.md) | Organize AGENTS.md content |
| [create-skills](create-skills/SKILL.md) | Create new skills |

### 🗄️ Git & Configuration

| Skill | Purpose |
|-------|---------|
| [chickenworld-git-workflow](chickenworld-git-workflow/SKILL.md) | ChickenWorld Git procedures |

---

## Path Convention

### ChickenDocs Paths

All skill files use **absolute paths** for ChickenDocs references:

```
/Users/marco/devel/ChickenWorld/ChickenDocs/Common/LOGGING_BEST_PRACTICES.md
```

This convention:
- Ensures reliability regardless of current working directory
- Matches the convention used in `~/.config/opencode/skills/`
- Remains valid as long as ChickenDocs stays at `/Users/marco/devel/ChickenWorld/ChickenDocs/`

### Skill-to-Skill Links

Skill references use relative paths from the skill directory:

```markdown
[chickenworld-testing](../chickenworld-testing/SKILL.md)
```

This keeps the skill repository portable when cloned to different locations.

---

## ChickenTools Integration

Tools used by skills with corresponding skill links:

| Tool | Skill Integration |
|------|-------------------|
| [build_and_test_all.py](https://github.com/balejs/ChickenTools/blob/main/bin/build_and_test_all.py) | [build-and-test-all](build-and-test-all/SKILL.md), [chickenworld-testing](chickenworld-testing/SKILL.md) |
| [decode_callstack.py](https://github.com/balejs/ChickenTools/blob/main/bin/decode_callstack.py) | [callstack-decoding](callstack-decoding/SKILL.md), [esp32-crash-analysis](esp32-crash-analysis/SKILL.md) |
| [test_esp32_crash_repeat.py](https://github.com/balejs/ChickenTools/blob/main/bin/test_esp32_crash_repeat.py) | [esp32-crash-analysis](esp32-crash-analysis/SKILL.md), [esp32-heap-debugging](esp32-heap-debugging/SKILL.md) |
| [parse_watchdog_crash_log.py](https://github.com/balejs/ChickenTools/blob/main/bin/parse_watchdog_crash_log.py) | [esp32-heap-debugging](esp32-heap-debugging/SKILL.md) |

---

## Quick Start Guide

### Starting a New Project

1. Run [new-chickenworld-project](new-chickenworld-project/SKILL.md)
2. Follow with [document-project](document-project/SKILL.md)
3. Verify with [verify-api-documentation](verify-api-documentation/SKILL.md)

### Writing Code

1. Follow [chickenworld-coding](chickenworld-coding/SKILL.md)
2. If cross-thread: use [cross-thread-safe-code](cross-thread-safe-code/SKILL.md)
3. Always test with [chickenworld-testing](chickenworld-testing/SKILL.md)

### Debugging Issues

1. **Native crash**: [native-crash-analysis](native-crash-analysis/SKILL.md)
2. **ESP32 crash**: [esp32-crash-analysis](esp32-crash-analysis/SKILL.md)
3. **Heap issues**: [esp32-heap-debugging](esp32-heap-debugging/SKILL.md)
4. **Follow workflow**: [investigation-workflow](investigation-workflow/SKILL.md)

### Building & Testing

1. Use [build-and-test-all](build-and-test-all/SKILL.md) for multi-project testing
2. Manage dependencies with [dependency-management](dependency-management/SKILL.md)

---

## Skill Creation

When creating new skills:
1. Follow [create-skills](create-skills/SKILL.md) guidelines
2. Document details in ChickenDocs first
3. Keep skill to 10-15 lines with references
4. Ensure proper ChickenTools integration

---

## References

- **ChickenDocs**: `/Users/marco/devel/ChickenWorld/ChickenDocs/`
- **ChickenTools**: https://github.com/balejs/ChickenTools
- **ChickenNetworkingLib**: https://github.com/balejs/ChickenNetworkingLib
- **ChickenFundamentalsLib**: https://github.com/balejs/ChickenFundamentalsLib

---

**Total Skills**: 20  
**Last Updated**: 2026-05-24  
**Location**: `~/.config/opencode/skills/` (active), `~/devel/ChickenWorld/ChickenWorldSkills/` (repository)
