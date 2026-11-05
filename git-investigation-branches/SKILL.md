---
name: git-investigation-branches
description: Branch policy for ChickenWorld investigations - naming, libdeps edits, history-rewrite safety, squash and merge
---

# Skill: Git Investigation Branches

**Purpose**: Keep investigation work isolated from release history, and never lose work to
a history rewrite

**Use when**: Starting an investigation, editing a library under `.pio/libdeps/`,
rebasing/squashing/amending, or finalising and merging findings

**Last Updated**: 2026-11-05

Split from `chickenworld-git-workflow`.

**CRITICAL RULES**:
1. **ALWAYS** create investigation branches locally; push only when collaborating
2. **ALWAYS** edit a library under `.pio/libdeps/` on a dedicated testing branch, never on
   a release branch
3. **NEVER** rewrite branch history without a backup ref first
4. **NEVER** merge an investigation branch into `1.1.0` - cherry-pick production changes only
5. **ALWAYS** use `--force-with-lease`, never bare `--force`

---

## ChickenWorld Branching Philosophy

### Standard Branch Structure

| Branch | Purpose | Status |
|--------|---------|--------|
| **1.1.0** | Main development branch | ✅ Active development |
| **investigation/yymmddhhmm-* ** | Investigation branches | 📝 Local only (don't push) |
| **fix/* ** | Bug fix branches | 🔄 For cherry-picking to 1.1.0 |
| **release tags** | Version tags (1.1.0.1, 1.1.0.2, etc.) | 🏷️ When all tests pass |

### Workflow

1. **Start from 1.1.0**: Always branch off the latest 1.1.0
2. **Investigation branch**: `git checkout -b investigation/yymmddhhmm-topic`
3. **Cherry-pick to 1.1.0**: When solution verified, cherry-pick code changes
4. **Keep docs separate**: Investigation docs stay in ChickenDocs repo
5. **Tag releases**: Create incremental tags after full test validation

**Key Principle**: 
- **Code fixes** → Cherry-pick to `1.1.0` branch
- **Investigation docs** → Stay in `ChickenDocs` repository
- **Avoid clutter**: Keep 1.1.0 history clean and focused on production code

### Naming Example

```bash
# Investigation branch (local only)
git checkout -b investigation/2605211430-memory_leak

# When complete, cherry-pick to 1.1.0
git checkout 1.1.0
git cherry-pick <code-commit-hash>

# Tag the release after verification
git tag 1.1.0.3
git push origin 1.1.0.3
```

### Investigation Branches

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
1. Create investigation branch from 1.1.0
2. Document findings in `ChickenDocs/[Project]/INVESTIGATION_*.md`
3. When solution found, verify on 1.1.0 branch
4. Cherry-pick code fixes to 1.1.0, leave docs in ChickenDocs

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

### Safety Branch Workflow (Any History Rewrite)

**Applies to**: `rebase -i`, squashing, rewording, reordering, amending more than one
commit, `reset --soft`/`--hard`, and any force-push. Each of these can silently discard
work; a backup ref is the only reliable recovery point.

```bash
# 1. Pin the current tip WITHOUT checking it out
#    (a branch you are standing on cannot be deleted at step 6)
git branch backup-verification-<YYYYMMDD>
git tag backup-<YYYYMMDD>-<HHMMSS>

# 2. Record the pre-rewrite state outside the repo, in case the repo is re-cloned
git log --oneline -10 > /tmp/backup-log-<YYYYMMDD>.txt

# 3. If the tree is dirty, park the work-in-progress on its own branch first
git checkout -b temp-safety-branch && git add -A && git commit -m "temp: save before reorganization"
git checkout <working-branch>

# 4. Rewrite
git reset --soft HEAD~2 && git commit -m "<combined message>"   # or: git rebase -i <base>

# 5. Verify - content must be identical, only the commit shape may differ
git diff backup-verification-<YYYYMMDD>                    # expect NO output
git log --oneline backup-verification-<YYYYMMDD>..HEAD     # the new commits
pio run -e esp32dev && pio test -e native                # if code was touched

# 6. Keep the backup until the rewrite is pushed and confirmed
git push --force-with-lease origin <working-branch>
git branch -D backup-verification-<YYYYMMDD>
git tag -d backup-<YYYYMMDD>-<HHMMSS>
```

**Key principles**:
- An empty `git diff backup...` is the proof nothing was lost. A commit message that
  *describes* a change is not evidence that the change is intact.
- `git add <file>` stages **every** pre-existing change to that file, including
  deletions made earlier in the session. Check `git diff --cached --stat` first.
- Use `--force-with-lease`, never bare `--force` - it aborts if someone else pushed.
- Delete the backup last, not first.

---

## Key References

- [GIT_COMMIT_GUIDELINES.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/GIT_COMMIT_GUIDELINES.md) - Commit format and rules
- [MULTIPLE_GITHUB_USERS_SSH_SETUP.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/MULTIPLE_GITHUB_USERS_SSH_SETUP.md) - SSH host configuration
- [INVESTIGATION_PROCEDURE.md](/Users/marco/devel/ChickenWorld/ChickenDocs/INVESTIGATION_PROCEDURE.md) - Investigation workflow
- [ChickenNetworkingLib/ChickenNetworkingLib_PROJECT_STRUCTURE.md](/Users/marco/devel/ChickenWorld/ChickenDocs/ChickenNetworkingLib/ChickenNetworkingLib_PROJECT_STRUCTURE.md) - Multi-repo structure

---

**Skills this relies on**:
- [chickenworld-coding](../coding/SKILL.md) - General coding standards
- [document-project](../document-project/SKILL.md) - Project documentation

---

## Investigation Finalization Procedure

When concluding an investigation and preparing to merge changes to the main development branch (e.g., `1.1.0`):

**CRITICAL RULE: Cherry-Pick Individual Commits, NEVER Merge Investigation Branches**

**Correct Pattern**:
```bash
# ✅ GOOD: Cherry-pick production commits individually to 1.1.0
git checkout 1.1.0
git cherry-pick <commit-hash>  # Production source code fix
git cherry-pick <commit-hash>  # Another production fix
git push origin 1.1.0
# Investigation branch remains untouched with all logs/docs

# ❌ WRONG: NEVER merge investigation branch to 1.1.0
git checkout 1.1.0
git merge investigation/branch-name  # This pollutes 1.1.0 with investigation artifacts!
```

**Rationale**: Investigation branches contain temporary findings, logs, and test code that should NEVER be in production history. Only cherry-pick commits that contain production code changes (source/config, not docs/test).

**See complete procedure**: [ChickenDocs/INVESTIGATION_PROCEDURE.md](/Users/marco/devel/ChickenWorld/ChickenDocs/INVESTIGATION_PROCEDURE.md#step-9-squash-and-merge-source-code-changes-to-main-branch)

### Step 1: Create Safety Branch
Before starting, save current state:
```bash
git checkout -b temp-safety-branch
git add -A
git commit -m "temp: save investigation state"
```

### Step 2: Analyze Commits
Review each commit on investigation branch:
```bash
git log --oneline 1.1.0..investigation/branch-name
```

For each commit, determine:
- **Source code** (`src/`, `include/`) → Should go to `1.1.0`
- **Test code** (`test/*.cpp`) → Should go to `1.1.0` (test infrastructure is production code)
- **Configuration** (`platformio.ini`, `.gitignore`, etc.) → Should go to `1.1.0`
- **Documentation** (`ChickenDocs/`, `docs/`) → Should go to `1.1.0` (guidelines, patterns, findings)

**Exclude from 1.1.0** (stay on investigation branch):
- Debug logging lines added for troubleshooting
- Temporary timeout relaxations or test hacks
- Temporary workarounds specifically for investigation
- Investigation-specific test files (e.g., `test_test_*_repeat.py`)
- Investigation log files in `project/investigation/logs/`

**Key Principle**: Most changes made to make tests pass ARE production code. Only exclude clearly temporary/debugging additions.

### Step 3: Pre-Merge Verification (CRITICAL)

**See complete procedure**: [ChickenDocs/INVESTIGATION_PROCEDURE.md](/Users/marco/devel/ChickenWorld/ChickenDocs/INVESTIGATION_PROCEDURE.md#pre-merge-verification)

**Quick checklist**:
- Search for `TODO/FIXME/HACK/TEMP` in source files
- Check for debug logging, hardcoded values, investigation references
- If temporary code found: **STOP and ask user** before merging

### Steps 4-8: Process, Verify, and Clean Up

**See complete procedures**: [ChickenDocs/INVESTIGATION_PROCEDURE.md](/Users/marco/devel/ChickenWorld/ChickenDocs/INVESTIGATION_PROCEDURE.md#step-4-process-commits-systematically)

**Quick reference**:
- **Step 4**: Cherry-pick commits systematically
- **Step 5**: Fix commit messages to proper format
- **Step 6**: Final verification (git log, diff, grep for docs)
- **Step 7**: Summary report (what merged vs what stayed)
- **Step 8**: Cleanup (delete temp safety branch)
# Delete temp-safety-branch
git branch -D temp-safety-branch
```

### Key Principle
**Separate concerns**: Code fixes go to `1.1.0`, investigation documentation stays in `ChickenDocs` repository.

This ensures:
- Clean, reviewable history on `1.1.0`
- Complete investigation trail in ChickenDocs
- Easy to revert code changes without losing documentation
- Investment docs don't clutter production branch history


---

**Key references**:
- [INVESTIGATION_PROCEDURE.md](/Users/marco/devel/ChickenWorld/ChickenDocs/INVESTIGATION_PROCEDURE.md) - Full investigation workflow
- [DEPENDENCY_MODIFICATION_WORKFLOW.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/DEPENDENCY_MODIFICATION_WORKFLOW.md) - Modifying vendored dependencies
- [GIT_COMMIT_GUIDELINES.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/GIT_COMMIT_GUIDELINES.md) - Commit format

**Skills this relies on**:
- [git-remote-setup](../git-remote-setup/SKILL.md) - Remotes and host aliases
- [git-commit-conventions](../git-commit-conventions/SKILL.md) - Message format
- [investigation-workflow](../investigation-workflow/SKILL.md) - The investigation itself
