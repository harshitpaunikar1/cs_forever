# Version Control with Git

Git is the universal version control system in DevOps. Every artifact — application
code, infrastructure definitions, CI/CD pipelines, documentation — should live in a
Git repository. This page covers Git internals, everyday workflows, branching strategies,
and the practices that make version control useful in a team environment.

---

## Why Version Control Matters in DevOps

- **History and auditability**: every change is recorded with author, timestamp, and message
- **Rollback**: revert to any previous state when a deployment breaks things
- **Collaboration**: multiple people work on the same codebase without stepping on each other
- **Infrastructure as Code**: Terraform, Ansible, and Kubernetes manifests are just text files — they belong in Git
- **CI/CD trigger**: a push to a branch is the canonical event that starts a pipeline

---

## Git Internals

Understanding how Git stores data makes advanced commands intuitive rather than magical.

### Object Types

Git is a content-addressed object store. Everything is stored as one of four object types in `.git/objects/`:

| Object | Description |
|--------|-------------|
| `blob` | File contents (no filename or permissions stored here) |
| `tree` | Directory listing — maps names and permissions to blobs/trees |
| `commit` | Snapshot pointer — points to a tree, parent commit(s), author, message |
| `tag` | Named pointer to a commit (annotated tags) |

```bash
git cat-file -t abc123    # Show object type
git cat-file -p abc123    # Pretty-print object content
git ls-tree HEAD          # List tree at HEAD
```

### Key Concepts

- **Index (staging area)**: a file (`.git/index`) that holds the next commit snapshot
- **HEAD**: a pointer to the current commit (usually via a branch ref)
- **Refs**: files in `.git/refs/` that store commit SHAs — branches are just moveable refs

---

## Setup

```bash
git config --global user.name  "Your Name"
git config --global user.email "you@example.com"
git config --global core.editor "vim"
git config --global init.defaultBranch main
git config --global pull.rebase true   # Rebase on pull instead of merge

# View config
git config --list
git config --global --list

# Config locations
# ~/.gitconfig         global
# .git/config          local (repo-level, overrides global)
# /etc/gitconfig       system (overrides none)
```

---

## Core Commands

```bash
# Initialize
git init                     # New repo in current directory
git clone https://github.com/org/repo.git
git clone --depth 1 ...     # Shallow clone (fastest for CI)

# Stage and commit
git status                   # Working tree status
git add file.txt             # Stage specific file
git add -p                   # Interactive: stage hunks (partial file staging)
git add .                    # Stage all changes in current directory
git commit -m "feat: add login endpoint"
git commit --amend           # Amend last commit (only before push!)

# View history
git log --oneline --graph --decorate --all
git log --author="Alice" --since="2 weeks ago"
git log --grep="fix:"
git show abc123              # Show a specific commit
git diff                     # Unstaged changes
git diff --staged            # Staged changes
git diff main..feature       # Diff between branches
```

---

## Branching

```bash
# Create and switch
git branch feature/login         # Create branch
git switch feature/login         # Switch to branch (modern)
git switch -c feature/login      # Create and switch (modern)
git checkout -b feature/login    # Old equivalent

# List
git branch                       # Local branches
git branch -r                    # Remote branches
git branch -a                    # All branches

# Delete
git branch -d feature/login      # Delete (safe: refuses if not merged)
git branch -D feature/login      # Force delete

# Rename
git branch -m old-name new-name
```

### Merge

```bash
git switch main
git merge feature/login          # Merge (fast-forward if possible)
git merge --no-ff feature/login  # Always create a merge commit
git merge --squash feature/login # Squash all commits into one staged change
git commit -m "feat: login (#42)"
```

**Fast-forward**: when main has no new commits since the branch point — HEAD just moves forward, no merge commit created.

**3-way merge**: when both branches have diverged — Git finds the common ancestor and creates a merge commit.

### Rebase

```bash
git switch feature/login
git rebase main              # Replay feature commits on top of main

# Interactive rebase: squash, reorder, edit, drop commits
git rebase -i main           # Opens editor listing commits
# Commands: pick, squash (s), fixup (f), edit (e), drop (d), reword (r)

# Abort a troubled rebase
git rebase --abort

# Continue after resolving conflicts
git rebase --continue
```

**Rebase vs Merge**:
- Rebase creates a linear history — cleaner `git log`, easier `git bisect`
- Rebase rewrites commit SHAs — **never rebase shared/public branches**
- Merge preserves true history — shows when branches diverged and merged

---

## Remote Operations

```bash
git remote -v                        # List remotes
git remote add upstream https://...  # Add remote
git remote set-url origin https://... # Change URL

git fetch origin                     # Download remote refs (no merge)
git fetch --all --prune              # Fetch all remotes, remove stale refs

git pull                             # fetch + merge (or rebase if configured)
git pull --rebase                    # fetch + rebase

git push origin feature/login        # Push branch
git push -u origin feature/login     # Push and set upstream tracking
git push origin --delete old-branch  # Delete remote branch
git push --tags                      # Push all tags
git push origin v1.2.3               # Push specific tag
```

---

## Undoing Changes

```bash
# Unstage
git restore --staged file.txt      # Remove from staging (file unchanged)

# Discard working tree changes
git restore file.txt               # Discard unstaged changes (irreversible!)

# Undo commits
git reset --soft HEAD~1   # Undo last commit, keep changes staged
git reset --mixed HEAD~1  # Undo last commit, keep changes unstaged (default)
git reset --hard HEAD~1   # Undo last commit, discard all changes

# Safe undo: create a new "undo" commit
git revert HEAD           # Revert last commit
git revert abc123         # Revert specific commit

# Clean untracked files
git clean -n              # Dry run: show what would be removed
git clean -fd             # Remove untracked files and directories
```

---

## Stashing

```bash
git stash                         # Stash current changes
git stash push -m "WIP: login"    # Stash with description
git stash list                    # List all stashes
git stash pop                     # Apply most recent stash and delete it
git stash apply stash@{2}         # Apply specific stash (keep it)
git stash drop stash@{2}          # Delete specific stash
git stash clear                   # Delete all stashes
git stash branch feature/wip      # Create branch from stash
```

---

## Tags

```bash
# Lightweight tag (just a pointer)
git tag v1.2.3

# Annotated tag (full object with message, author, date)
git tag -a v1.2.3 -m "Release v1.2.3"
git tag -a v1.2.3 abc123 -m "Tag old commit"

git tag -l "v1.*"         # List tags matching pattern
git show v1.2.3            # Show tag details
git push origin v1.2.3     # Push specific tag
git push origin --tags     # Push all tags
git tag -d v1.2.3          # Delete local tag
git push origin --delete v1.2.3  # Delete remote tag
```

---

## Advanced Commands

```bash
# Cherry-pick: apply specific commits to current branch
git cherry-pick abc123
git cherry-pick abc123..def456  # Range of commits

# Bisect: binary search for a bug-introducing commit
git bisect start
git bisect bad             # Current commit is bad
git bisect good v1.0.0     # This tag was good
# Git checks out midpoint; test and mark:
git bisect good / git bisect bad
git bisect reset           # End bisect session

# Blame: see who last changed each line
git blame -L 10,20 file.txt    # Lines 10-20

# Log tricks
git shortlog -sn           # Commit count by author
git log --stat             # Files changed per commit
git log --follow file.txt  # Follow renames
```

---

## .gitignore

```gitignore
# Build output
dist/
build/
*.class
*.pyc
__pycache__/

# Dependencies
node_modules/
vendor/

# Environment files
.env
.env.local
*.env

# Editor
.idea/
.vscode/
*.swp

# OS
.DS_Store
Thumbs.db

# Secrets — never commit these
*.pem
*.key
credentials.json
```

```bash
git check-ignore -v file.txt    # Why is this file being ignored?

# Global gitignore (apply to all repos)
git config --global core.excludesfile ~/.gitignore_global
```

---

## Branching Strategies

### GitHub Flow (Simple)

```
main ──── feature/A ──────── (PR) ──── main
     └─── feature/B ──────── (PR) ──┘
```

1. Branch from `main`
2. Make changes, push commits
3. Open a Pull Request
4. Review, pass CI, merge to `main`
5. Deploy immediately (or on merge)

Best for: small teams, continuous deployment, SaaS products.

### GitFlow (Complex)

```
main ──────────── release/1.1 ── hotfix ────────
        develop ─── feature/A ─────────────────
```

- `main`: always production-ready
- `develop`: integration branch
- `feature/*`: new features branch from develop
- `release/*`: stabilization before merge to main
- `hotfix/*`: emergency fixes branch from main

Best for: versioned software, scheduled releases, larger teams.

### Trunk-Based Development

Everyone commits to `main` (trunk) frequently (at least daily). Short-lived branches (< 2 days). Feature flags hide incomplete work. Requires strong CI gates.

Best for: high-velocity teams, Google/Meta scale, mature CI/CD.

---

## Git Hooks

Hooks are scripts in `.git/hooks/` that fire at specific events.

```bash
ls .git/hooks/          # pre-commit.sample, commit-msg.sample, etc.
chmod +x .git/hooks/pre-commit   # Make hook executable
```

**Common hooks**:

| Hook | Fires When | Common Use |
|------|-----------|------------|
| `pre-commit` | Before commit is created | Run linters, format checks |
| `commit-msg` | After commit message is written | Enforce message format |
| `pre-push` | Before push to remote | Run tests, prevent secrets |
| `post-merge` | After merge/pull | Run `npm install` if package.json changed |

```bash
# pre-commit: run tests
#!/usr/bin/env bash
npm test || exit 1

# commit-msg: enforce Conventional Commits
#!/usr/bin/env bash
commit_msg=$(cat "$1")
if ! echo "$commit_msg" | grep -qE "^(feat|fix|docs|style|refactor|test|chore|ci):"; then
  echo "ERROR: Commit must follow Conventional Commits format"
  echo "  feat: add login"
  echo "  fix: handle null pointer"
  exit 1
fi
```

**Use [pre-commit](https://pre-commit.com/) framework** to manage hooks across a team:

```yaml
# .pre-commit-config.yaml
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.4.0
    hooks:
      - id: trailing-whitespace
      - id: detect-private-key
      - id: check-merge-conflict
```

---

## Pull Request Workflow

1. Fork (for open source) or branch (for team repos)
2. Make atomic, well-described commits
3. Push branch, open PR against `main`
4. CI runs automatically (tests, linting, security scans)
5. Request review from CODEOWNERS
6. Address review comments with new commits
7. Squash-merge or merge commit (team policy)

```bash
# CODEOWNERS file (GitHub/GitLab)
# .github/CODEOWNERS
/infra/      @devops-team
/src/auth/   @security-team
*.tf         @devops-team
```

---

## Writing Good Commit Messages

**Conventional Commits** format:
```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

Types: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `chore`, `ci`, `build`

```
feat(auth): add JWT refresh token support

Previously tokens expired after 1 hour with no way to refresh.
This adds a /auth/refresh endpoint that accepts a valid refresh
token and returns a new access token.

Closes #123
```

**Rules**:
- Subject line ≤ 72 characters
- Use imperative mood: "add feature" not "added feature"
- Body explains *why*, not *what* (the diff shows what)
- Reference issues in footer

---

## Monorepo vs Polyrepo

| | Monorepo | Polyrepo |
|---|---------|---------|
| **Code sharing** | Easy (local imports) | Requires package publishing |
| **Atomic changes** | One PR for cross-service change | Coordinated PRs |
| **CI speed** | Slow unless using affected-only (Nx, Turborepo, Bazel) | Fast per repo |
| **Access control** | Harder (all or nothing per repo) | Fine-grained per repo |
| **Used by** | Google, Meta, Microsoft | Most open source projects |

---

## Useful Aliases

```bash
# ~/.gitconfig
[alias]
  st = status
  co = checkout
  sw = switch
  lg = log --oneline --graph --decorate --all
  undo = reset --soft HEAD~1
  unstage = restore --staged
  aliases = config --get-regexp alias
```
