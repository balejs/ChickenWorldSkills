# ChickenWorld Skills

**Purpose**: Collection of AI agent skills for ChickenWorld development workflows

**Canonical location**: `~/devel/ChickenWorld/ChickenWorldSkills/` - the only git clone  
**Loaded by**: `~/.config/opencode/skills` and `~/.claude/skills`, both symlinks to the clone

**Do not clone this repository elsewhere.** A second clone drifts silently: each copy accumulates
commits and uncommitted edits the other never sees, and work can sit untracked in one copy while
the other is pushed.

---

## Overview

This repository contains **18 skills** that enforce ChickenWorld coding standards, testing procedures, and best practices across all projects.

Skills follow **Option B** format:
- 10-15 lines with workflow + links
- Integration with ChickenTools where applicable
- References to detailed ChickenDocs documentation

**Key Principle**: All detailed documentation must exist in ChickenDocs first

---

## Skills Catalog

### 🎯 Universal Development

| Skill | Purpose |
|---|---|
| [coding](coding/SKILL.md) | ChickenWorld C++ coding standards - string types, logging macros, lifecycle ownership, schedulers |
| [cross-thread-safe-code](cross-thread-safe-code/SKILL.md) | Write cross-thread safe code for ESP32 and native platforms |
| [chickenworld-testing](chickenworld-testing/SKILL.md) | Follow testing procedures for ChickenWorld projects |
| [build-and-test-all](build-and-test-all/SKILL.md) | Use ChickenTools build_and_test_all.py for comprehensive validation |
### 🐛 Crash, Hang and Debugging

| Skill | Purpose |
|---|---|
| [crash-analysis](crash-analysis/SKILL.md) | Analyse ESP32 and native crashes - backtrace symbolication, heap corruption, watchdog resets |
| [network-debugging](network-debugging/SKILL.md) | Debug ChickenWorld networking and TLS issues - URI paths, state listeners, SNI, certificate failures |
| [timeout-hang-analysis](timeout-hang-analysis/SKILL.md) | Distinguish a legitimate timeout from a hang by testing whether the system was still making progress when the timer fired |
| [investigation-workflow](investigation-workflow/SKILL.md) | Follow systematic investigation procedures for debugging |
### 🔀 Git

| Skill | Purpose |
|---|---|
| [git-remote-setup](git-remote-setup/SKILL.md) | Configure GitHub host aliases and create new ChickenWorld repositories |
| [git-commit-conventions](git-commit-conventions/SKILL.md) | Write ChickenWorld commit messages - component prefixes, atomic commits, no AI references |
| [git-investigation-branches](git-investigation-branches/SKILL.md) | Branch policy for ChickenWorld investigations - naming, libdeps edits, history-rewrite safety, squash and merge |
### 📝 Documentation

| Skill | Purpose |
|---|---|
| [documentation-maintenance](documentation-maintenance/SKILL.md) | Write and revise ChickenWorld documentation under the three quality principles - consistency, conciseness, clarity |
| [document-project](document-project/SKILL.md) | Create and document a ChickenWorld project - scaffolding, header API docs and verification |
| [document-project-docs](document-project-docs/SKILL.md) | Document project-specific details in ChickenDocs |
| [organize-agents](organize-agents/SKILL.md) | Organize AGENTS.md files in ChickenWorld projects |
| [deep-save](deep-save/SKILL.md) | Preserve session context, evidence and lessons before they are lost, routing each to its correct home |
### 🏗️ Project and Dependencies

| Skill | Purpose |
|---|---|
| [dependency-management](dependency-management/SKILL.md) | Manage PlatformIO dependencies across ChickenWorld repos - keep .pio/libdeps in sync without wiping the cache |
### 🗂️ Skill Maintenance

| Skill | Purpose |
|---|---|
| [skill-maintenance](skill-maintenance/SKILL.md) | Create and revise ChickenWorld skills - location, format, path conventions and quality bar |
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
| [decode_callstack.py](https://github.com/balejs/ChickenTools/blob/main/bin/decode_callstack.py) | [crash-analysis](crash-analysis/SKILL.md) |
| [test_esp32_crash_repeat.py](https://github.com/balejs/ChickenTools/blob/main/bin/test_esp32_crash_repeat.py) | [crash-analysis](crash-analysis/SKILL.md) |
| [parse_watchdog_crash_log.py](https://github.com/balejs/ChickenTools/blob/main/bin/parse_watchdog_crash_log.py) | [crash-analysis](crash-analysis/SKILL.md) |

---

## Quick Start Guide

### Starting a New Project

1. Follow [document-project](document-project/SKILL.md) - scaffolding, API docs, verification
2. Organise with [organize-agents](organize-agents/SKILL.md)
3. Set up remotes with [git-remote-setup](git-remote-setup/SKILL.md)

### Writing Code

1. Follow [coding](coding/SKILL.md)
2. If cross-thread: use [cross-thread-safe-code](cross-thread-safe-code/SKILL.md)
3. Always test with [chickenworld-testing](chickenworld-testing/SKILL.md)

### Debugging Issues

1. **Any crash**: [crash-analysis](crash-analysis/SKILL.md) - ESP32, native, callstacks, heap
2. **Stalled, not crashed**: [timeout-hang-analysis](timeout-hang-analysis/SKILL.md)
3. **Network / TLS**: [network-debugging](network-debugging/SKILL.md)
4. **Follow workflow**: [investigation-workflow](investigation-workflow/SKILL.md)

### Building & Testing

1. Use [build-and-test-all](build-and-test-all/SKILL.md) for multi-project testing
2. Manage dependencies with [dependency-management](dependency-management/SKILL.md)

---

## Skill Creation

When creating new skills:
1. Follow [skill-maintenance](skill-maintenance/SKILL.md)
2. Document details in ChickenDocs first
3. Keep the skill thin - workflow plus links, substance stays in ChickenDocs
4. Ensure proper ChickenTools integration
5. Revise under [documentation-maintenance](documentation-maintenance/SKILL.md)
6. Preserve session findings with [deep-save](deep-save/SKILL.md)

---

## References

- **ChickenDocs**: `/Users/marco/devel/ChickenWorld/ChickenDocs/`
- **ChickenTools**: https://github.com/balejs/ChickenTools
- **ChickenNetworkingLib**: https://github.com/balejs/ChickenNetworkingLib
- **ChickenFundamentalsLib**: https://github.com/balejs/ChickenFundamentalsLib

---

**Total Skills**: 18  
**Last Updated**: 2026-11-05  
**Canonical location**: `~/devel/ChickenWorld/ChickenWorldSkills/` (the only git clone)  
**Consumers**: `~/.config/opencode/skills` and `~/.claude/skills` are symlinks to the clone
