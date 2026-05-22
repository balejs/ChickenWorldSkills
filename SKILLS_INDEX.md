# ChickenWorld Skills Index

**Purpose**: Quick navigation and overview of all available skills

**Last Updated**: 2026-05-21

---

## Skill Categories

### 🎯 Universal Development Skills

**Core skills for all ChickenWorld projects**:

| Skill | Purpose | Priority |
|-------|---------|----------|
| [chickenworld-coding](chickenworld-coding.md) | Enforce ChickenWorld coding standards | ⭐⭐⭐ |
| [chickenworld-testing](chickenworld-testing.md) | Follow testing procedures | ⭐⭐⭐ |
| [build-and-test-all](build-and-test-all.md) | Use ChickenTools automation | ⭐⭐⭐ |
| [cross-thread-safe-code](cross-thread-safe-code.md) | Write cross-thread safe code | ⭐⭐⭐ |

### 🐛 Debugging & Crash Analysis

**Skills for troubleshooting and debugging**:

| Skill | Purpose | Priority |
|-------|---------|----------|
| [esp32-crash-analysis](esp32-crash-analysis.md) | Analyze ESP32 crashes | ⭐⭐⭐ |
| [native-crash-analysis](native-crash-analysis.md) | Analyze native crashes | ⭐⭐ |
| [esp32-heap-debugging](esp32-heap-debugging.md) | Debug heap poisoning | ⭐⭐ |
| [callstack-decoding](callstack-decoding.md) | Decode ESP32 backtraces | ⭐⭐ |
| [investigation-workflow](investigation-workflow.md) | Systematic investigation | ⭐⭐⭐ |

### 🔧 Networking & TLS

**Skills for networking issues**:

| Skill | Purpose | Priority |
|-------|---------|----------|
| [tls-debugging](tls-debugging.md) | Debug TLS/HTTPS issues | ⭐⭐ |
| [networking-debugging](networking-debugging.md) | Debug networking issues | ⭐⭐ |

### 📝 Documentation

**Skills for documentation tasks**:

| Skill | Purpose | Priority |
|-------|---------|----------|
| [document-project](document-project.md) | Document new projects | ⭐⭐⭐ |
| [verify-api-documentation](verify-api-documentation.md) | Verify API docs | ⭐⭐ |

### 🏗️ Project Management

**Skills for project setup and maintenance**:

| Skill | Purpose | Priority |
|-------|---------|----------|
| [new-chickenworld-project](new-chickenworld-project.md) | Create new projects | ⭐⭐ |
| [dependency-management](dependency-management.md) | Manage dependencies | ⭐⭐ |

### 🗂️ Organization

**Skills for documentation organization**:

| Skill | Purpose | Priority |
|-------|---------|----------|
| [organize-agents](organize-agents.md) | Organize AGENTS.md content | ⭐⭐ |
| [document-project-docs](document-project-docs.md) | Document project-specific details | ⭐⭐ |

### 🛠️ Meta-Skills

**Skills for skill management**:

| Skill | Purpose | Priority |
|-------|---------|----------|
| [create-skills](create-skills.md) | Create new skills | ⭐⭐⭐ |

---

## Skill Detail Level

All skills follow **Option B**:
- 10-15 lines with workflow + links
- Integration with ChickenTools where applicable
- References to detailed ChickenDocs documentation
- Cross-references to related skills

---

## ChickenTools Integration

Skills that integrate with ChickenTools tools:

| Tool | Skill Integration |
|------|-------------------|
| [build_and_test_all.py](../../ChickenTools/bin/build_and_test_all.py) | [build-and-test-all](build-and-test-all.md), [chickenworld-testing](chickenworld-testing.md) |
| [decode_callstack.py](../../ChickenTools/bin/decode_callstack.py) | [callstack-decoding](callstack-decoding.md), [esp32-crash-analysis](esp32-crash-analysis.md) |
| [test_esp32_crash_repeat.py](../../ChickenTools/bin/test_esp32_crash_repeat.py) | [esp32-crash-analysis](esp32-crash-analysis.md), [esp32-heap-debugging](esp32-heap-debugging.md) |
| [parse_watchdog_crash_log.py](../../ChickenTools/bin/parse_watchdog_crash_log.py) | [esp32-heap-debugging](esp32-heap-debugging.md) |

---

## Quick Start Guide

### Starting a New Project

1. Run [new-chickenworld-project](new-chickenworld-project.md)
2. Follow with [document-project](document-project.md)
3. Verify with [verify-api-documentation](verify-api-documentation.md)

### Writing Code

1. Follow [chickenworld-coding](chickenworld-coding.md)
2. If cross-thread: use [cross-thread-safe-code](cross-thread-safe-code.md)
3. Always test with [chickenworld-testing](chickenworld-testing.md)

### Debugging Issues

1. **Native crash**: [native-crash-analysis](native-crash-analysis.md)
2. **ESP32 crash**: [esp32-crash-analysis](esp32-crash-analysis.md)
3. **Heap issues**: [esp32-heap-debugging](esp32-heap-debugging.md)
4. **Follow workflow**: [investigation-workflow](investigation-workflow.md)

### Building & Testing

1. Use [build-and-test-all](build-and-test-all.md) for multi-project testing
2. Manage dependencies with [dependency-management](dependency-management.md)

---

## Reference Documentation

**ChickenDocs locations**:
- Generic guidelines: [ChickenDocs/Common/](../../ChickenDocs/Common/)
- Development practices: [ChickenDocs/development_guidelines.md](../../ChickenDocs/development_guidelines.md)
- ChickenTools: [ChickenTools/](../../ChickenTools/)
- Project docs: [ChickenDocs/ChickenSoftwareUpdateLib/](../../ChickenDocs/ChickenSoftwareUpdateLib/)

**Skill Creation Rules**:
- Follow [create-skills](create-skills.md) for creating new skills
- All documentation must exist in ChickenDocs first
- Include ChickenTools integration when applicable

---

**Skills Total**: 19 (3 original + 16 new)
**Updated**: 2026-05-21
