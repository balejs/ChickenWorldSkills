# Skill: ChickenWorld Git Workflow

**Purpose**: Standard Git procedures for ChickenWorld projects, including repository setup and commit guidelines

**Use when**: Creating new ChickenWorld repositories, managing git workflows, or committing code changes

**CRITICAL RULES**:
1. **NEVER** reference AI tools in commit messages - write as human developer
2. **ALWAYS** use GitHub host aliases (balejs.github.com) in remote URLs
3. **ALWAYS** commit library changes to respective library repos, not main project
4. **ALWAYS** separate code and documentation changes into distinct commits
5. **ALWAYS** create investigation branches locally only (don't push unless collaborating)

---

## Git Host Configuration

### ~/.ssh/config Setup (Required for All ChickenWorld Projects)

**For balejs GitHub account**:
```ssh-config
Host balejs.github.com
    Hostname github.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_rsa_marcoballesio_gmail
```

**For quantumboar GitHub account** (rare exceptions):
```ssh-config
Host quantumboar.github.com
    Hostname github.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_rsa_quantumboar
```

**Testing SSH configuration**:
```bash
ssh -T git@balejs.github.com
# Expected: "Hi marcoballesio_gmail! You've successfully authenticated..."
```

---

## New Repository Creation

### ChickenWorld Project (Standard Pattern)

**1. Create SSH config** (if not exists):
```bash
cat >> ~/.ssh/config << EOF
Host balejs.github.com
    Hostname github.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_rsa_marcoballesio_gmail
EOF
chmod 600 ~/.ssh/config
```

**2. Create repo on GitHub** (manual step at github.com):
- Go to https://github.com/balejs
- Click "New repository"
- Repository name: `ChickenXyzLib` (follow ChickenWorld naming)
- Visibility: Public
- Initialize: Do NOT initialize (clean start)

**3. Initialize local repo**:
```bash
cd /path/to/ChickenXyzLib
git init
git remote add origin git@balejs.github.com:balejs/ChickenXyzLib.git
git checkout -b main
```

**4. Configure branch settings**:
```bash
# Set main branch as default
git config branch.main.remote origin
git config branch.main.merge refs/heads/main

# Add version branches if needed
git config branch.1.1.0.remote origin
git config branch.1.1.0.merge refs/heads/1.1.0
```

**5. First commit and push**:
```bash
git add README.md include/ src/ test/
git commit -m "feat: Initial ChickenXyzLib implementation

Core structure with API headers and platform test support"

git push -u origin main
```

### Verification

```bash
git remote -v
# Should show: origin	git@balejs.github.com:balejs/ChickenXyzLib.git (fetch/push)

cat .git/config
# Should show remote origin with balejs.github.com host alias
```

---

## Commit Message Format

### Structure
```
<component>: <brief summary>

<optional detailed description>

<optional footer with issue references>
```

### Component Names
Use the **object or component being modified** as the preamble:
- `ReferenceCounter:` - Changes to reference counting
- `LoopScheduler:` - Changes to scheduler
- `HttpExchange:` - Changes to HTTP exchange
- `Buffer:` - Changes to buffer implementation
- `Generic:` - Multiple components or general changes

### Modular Commit Principle
**Prioritize atomic, focused commits**:
1. **Break down large changes** - If a change touches multiple independent areas, split into separate commits
2. **Functionally grouped changes** - Changes that must stay together (e.g., API change + usage updates) can be in one commit
3. **Never mix source with non-source** - Code changes must be isolated from docs/config/documentation changes

### Separation Rules

**Must be separate commits**:
- **Source code** (`src/`, `include/`) → One commit
- **Documentation** (`ChickenDocs/`, `docs/`) → Separate commit
- **Configuration** (`platformio.ini`, `.gitignore`, etc.) → Separate commit
- **AGENTS.md or README.md** → Separate commit

**Good practice** (can be together):
```
Commit 1: ReferenceCounter: Add mutex protection
         - src/ReferenceCounter.cpp: Add mutex lock
         - include/ReferenceCounter.h: Add lock/unlock methods

Commit 2: docs: Document ReferenceCounter thread safety
         - ChickenDocs/Common/CHICKENWORLD_LIFECYCLE_MANAGEMENT.md

Commit 3: platformio.ini: Enable lifecycle checks
         - platformio.ini: Add build_flag
```

**Bad practice** (should be split):
```
❌ ONE COMMIT:
   - src/ReferenceCounter.cpp: Add mutex lock
   - include/ReferenceCounter.h: Add methods
   - ChickenDocs/Common/CHICKENWORLD_LIFECYCLE_MANAGEMENT.md: Document thread safety
   - platformio.ini: Add build_flag
```

### Examples

**Good commits** (modular, focused):
```
ReferenceCounter: Add mutex protection to helper functions

The addStrongRef and releaseRef functions were missing mutex
protection, leading to race conditions in multi-threaded scenarios.
Added Lock/NoLock versions to allow internal callers to skip locking.

Closes #123
```

```
LoopScheduler: Remove Weakling dependency

Eliminated Weakling reference from LoopScheduler to reduce
stack usage and improve performance. Weakling usage moved
to private implementations only.
```

```
ChickenHttpLib: Update to use new NetworkExchange API

Updated HttpClient to use NetworkExchange instead of SQuery.
All call sites migrated to new factory methods.
```

**Bad commits** (avoid these):
```
update ReferenceCounter with mutex                # Too vague
referencecounter: add mutex and update docs and fix config  # Mixed concerns
AI suggested this fix                             # References AI
```

---

## Investigation Branches

### Naming Convention
```bash
# Format: investigation/yymmddhhmm-short_description
git checkout -b investigation/2605211430-memory_leak
```

**IMPORTANT**: Investigation branches are LOCAL ONLY
```bash
# ❌ DON'T push investigation branches
git push origin investigation/2605211430-memory_leak

# ✅ DO keep them local unless explicit collaboration needed
```

### Workflow
1. Create investigation branch
2. Document findings in `ChickenDocs/[Project]/INVESTIGATION_*.md`
3. When solution found, apply fix to main branch
4. Cherry-pick code fixes to main, leave investigation docs in ChickenDocs

---

## Library File Management

### Changes in `.pio/libdeps/`

Files under `.pio/libdeps/` are **compiled dependencies**, not source.

**When modifying library files**:

1. **Test in main project**:
   ```bash
   # Make changes in .pio/libdeps/native/ChickenFundamentalsLib/
   # Test the changes
   ```

2. **Commit to library repo** (NOT main project):
   ```bash
   cd .pio/libdeps/native/ChickenFundamentalsLib
   git add -A
   git commit -m "fix: Implement mutex protection"
   git push origin main
   
   cd /path/to/main/project
   ```

3. **Update main project** (if needed):
   ```bash
   # Update library.json or platformio.ini with new version/branch
   git add library.json
   git commit -m "chore: Update ChickenFundamentalsLib to latest"
   ```

### Warning
**ALWAYS alert** when committing changes that affect library repos:
```
⚠️ WARNING: Modified files in .pio/libdeps/
These changes must be committed to: ChickenFundamentalsLib
```

---

## Separating Code and Documentation Changes

### When Mixed Changes Occur

**Use `git add -p`** to split changes:

```bash
# Interactive patch mode
git add -p include/LoopScheduler.h

# Press 's' to split hunks
# Press 'y' to stage code changes
# Press 'n' to skip documentation changes

# Commit code changes
git commit -m "refactor: Remove Weakling dependency"

# Stage remaining documentation changes
git add include/LoopScheduler.h docs/
git commit -m "docs: Update API documentation"
```

### Safety Branch Workflow

```bash
# 1. Save current state
git checkout -b temp-safety-branch
git commit -am "temp: save before reorganization"

# 2. Return to working branch
git checkout original-branch
git reset --soft HEAD~1

# 3. Split and commit separately
git add <code-files>
git commit -m "fix: <code changes>"

git add <doc-files>
git commit -m "docs: <doc changes>"

# 4. Verify against safety branch
git diff temp-safety-branch
# Should show no output

# 5. Clean up
git branch -D temp-safety-branch
```

---

## Key References

- [GIT_COMMIT_GUIDELINES.md](../../ChickenDocs/Common/GIT_COMMIT_GUIDELINES.md) - Commit format and rules
- [MULTIPLE_GITHUB_USERS_SSH_SETUP.md](../../ChickenDocs/Common/MULTIPLE_GITHUB_USERS_SSH_SETUP.md) - SSH host configuration
- [INVESTIGATION_PROCEDURE.md](../../ChickenDocs/INVESTIGATION_PROCEDURE.md) - Investigation workflow
- [ChickenNetworkingLib/ChickenNetworkingLib_PROJECT_STRUCTURE.md](../../ChickenDocs/ChickenNetworkingLib/ChickenNetworkingLib_PROJECT_STRUCTURE.md) - Multi-repo structure

---

**Skills this relies on**:
- [chickenworld-coding](chickenworld-coding.md) - General coding standards
- [document-project](document-project.md) - Project documentation
