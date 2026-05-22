# ChickenWorld Skills

**Purpose**: Collection of AI agent skills for ChickenWorld development workflows

**Location**: Skills are loaded from `~/.opencode/skills/`

---

## Overview

This repository contains 19 skills that enforce ChickenWorld coding standards, testing procedures, and best practices across all projects.

**Skills are auto-loaded by opencode** from `~/.opencode/skills/`

---

## Skills Catalog

### 🎯 Universal Development Skills

| Skill | Purpose |
|-------|---------|
| [chickenworld-coding](chickenworld-coding.md) | Enforce ChickenWorld coding standards |
| [chickenworld-testing](chickenworld-testing.md) | Follow testing procedures |
| [build-and-test-all](build-and-test-all.md) | Use ChickenTools automation |
| [cross-thread-safe-code](cross-thread-safe-code.md) | Write cross-thread safe code |

### 🐛 Crash Analysis & Debugging

| Skill | Purpose |
|-------|---------|
| [esp32-crash-analysis](esp32-crash-analysis.md) | Analyze ESP32 crashes |
| [native-crash-analysis](native-crash-analysis.md) | Analyze native crashes |
| [callstack-decoding](callstack-decoding.md) | Decode ESP32 backtraces |
| [esp32-heap-debugging](esp32-heap-debugging.md) | Debug heap poisoning |

### 🔧 Debugging & Troubleshooting

| Skill | Purpose |
|-------|---------|
| [tls-debugging](tls-debugging.md) | Debug TLS/HTTPS issues |
| [networking-debugging](networking-debugging.md) | Debug networking issues |
| [investigation-workflow](investigation-workflow.md) | Systematic investigation workflow |

### 📝 Documentation

| Skill | Purpose |
|-------|---------|
| [document-project](document-project.md) | Document new projects |
| [verify-api-documentation](verify-api-documentation.md) | Verify API documentation |

### 🏗️ Project Management

| Skill | Purpose |
|-------|---------|
| [new-chickenworld-project](new-chickenworld-project.md) | Create new projects |
| [dependency-management](dependency-management.md) | Manage dependencies |

### 🗂️ Organization

| Skill | Purpose |
|-------|---------|
| [organize-agents](organize-agents.md) | Organize AGENTS.md content |
| [document-project-docs](document-project-docs.md) | Document project-specific details |
| [create-skills](create-skills.md) | Create new skills |

### ⚙️ Git & Configuration

| Skill | Purpose |
|-------|---------|
| [chickenworld-git-workflow](chickenworld-git-workflow.md) | ChickenWorld Git procedures |

---

## Using Skills

### Automatic Loading

Skills are automatically loaded by opencode from `~/.opencode/skills/`

### Invocation

Simply reference skills by name when working on related tasks:
- "Follow chickenworld-coding when writing new code"
- "Use chickenworld-testing to validate changes"
- "Apply investigation-workflow for debugging"

### Customizing Skills

Skills follow Option B format (10-15 lines with workflow + links):
- Minimal workflow instructions
- References to detailed ChickenDocs
- ChickenTools integration where applicable

**Rule**: All actual documentation must exist in ChickenDocs first

---

## Skill Creation

When creating new skills:
1. Follow [create-skills](create-skills.md) guidelines
2. Document details in ChickenDocs first
3. Keep skill to 10-15 lines with references
4. Ensure proper ChickenTools integration

---

## References

- **ChickenDocs**: https://github.com/balejs/ChickenDocs
- **ChickenTools**: https://github.com/balejs/ChickenTools
- **ChickenSoftwareUpdateLib**: https://github.com/balejs/ChickenSoftwareUpdateLib

---

**Total Skills**: 19  
**Last Updated**: 2026-05-21  
**Location**: ~/.opencode/skills/
