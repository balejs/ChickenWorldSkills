---
name: git-remote-setup
description: Configure GitHub host aliases and create new ChickenWorld repositories
---

# Skill: Git Remote Setup

**Purpose**: Set up multi-account GitHub SSH access and create correctly-configured repos

**Use when**: First clone on a machine, adding a repo, or a remote/SSH failure

**Last Updated**: 2026-11-05

Split from `chickenworld-git-workflow` (472 lines) - remote configuration is a different
task from writing commits and is needed at a different time.

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


---

**Key references**:
- [MULTIPLE_GITHUB_USERS_SSH_SETUP.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/MULTIPLE_GITHUB_USERS_SSH_SETUP.md) - SSH host configuration
- [GIT_COMMIT_GUIDELINES.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/GIT_COMMIT_GUIDELINES.md) - Commit format and rules

**Skills this relies on**:
- [git-commit-conventions](../git-commit-conventions/SKILL.md) - What to write in the commits
- [git-investigation-branches](../git-investigation-branches/SKILL.md) - Branch policy after creation
