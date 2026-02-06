# Contributing to NetBiz AI Consultancy

## Branching Strategy (Git Flow)

We use **Git Flow** to manage our codebase. All developers must follow this strategy.

### Branch Overview

```
master ────────────────────────────────── production (tagged releases)
 │
 └── develop ─────────────────────────── integration branch
      │
      ├── feature/PROJ-123-description ── individual work
      ├── release/1.2.0 ──────────────── release prep & QA
      └── hotfix/fix-description ──────── emergency fixes
```

### Branches

| Branch | Purpose | Branches from | Merges into | Protected |
|--------|---------|---------------|-------------|-----------|
| `master` | Production-ready code, tagged with version numbers | — | — | Yes |
| `develop` | Integration of completed features | `master` | `master` (via release branch) | Yes |
| `feature/*` | New features and non-emergency work | `develop` | `develop` | No |
| `release/*` | Release stabilization and QA | `develop` | `master` + `develop` | Yes |
| `hotfix/*` | Emergency production fixes | `master` | `master` + `develop` | No |

### Branch Naming Conventions

```
feature/SHORT-DESCRIPTION         e.g. feature/user-auth
feature/TICKET-ID-description     e.g. feature/PROJ-123-user-auth
release/MAJOR.MINOR.PATCH         e.g. release/1.2.0
hotfix/SHORT-DESCRIPTION          e.g. hotfix/fix-login-crash
```

- Use lowercase and hyphens (no underscores or spaces)
- Keep names short but descriptive
- Include ticket IDs when available

## Workflows

### 1. Working on a Feature

```bash
# Start from develop
git checkout develop
git pull origin develop
git checkout -b feature/PROJ-123-my-feature

# Work on your feature...
git add <files>
git commit -m "Add feature description"

# Push and open a PR into develop
git push -u origin feature/PROJ-123-my-feature
# Open PR: base=develop, compare=feature/PROJ-123-my-feature
```

- All feature PRs target `develop`
- Require at least **2 approving reviews** before merge
- Stale approvals are dismissed when new commits are pushed
- Delete the feature branch after merge

### 2. Creating a Release

```bash
# Create release branch from develop
git checkout develop
git pull origin develop
git checkout -b release/1.2.0

# Perform QA, fix bugs, bump version numbers...
git commit -m "Bump version to 1.2.0"

# When ready, open a PR into master
# After merge, tag the release:
git checkout master
git pull origin master
git tag -a v1.2.0 -m "Release 1.2.0"
git push origin v1.2.0

# Merge release back into develop
git checkout develop
git merge release/1.2.0
git push origin develop

# Clean up
git branch -d release/1.2.0
git push origin --delete release/1.2.0
```

### 3. Hotfixing Production

```bash
# Branch from master
git checkout master
git pull origin master
git checkout -b hotfix/fix-critical-bug

# Fix the issue...
git commit -m "Fix critical bug in payment processing"

# Open PR into master
# After merge, tag the patch release:
git checkout master
git pull origin master
git tag -a v1.2.1 -m "Hotfix 1.2.1"
git push origin v1.2.1

# Merge hotfix back into develop
git checkout develop
git merge hotfix/fix-critical-bug
git push origin develop

# Clean up
git branch -d hotfix/fix-critical-bug
git push origin --delete hotfix/fix-critical-bug
```

## Pull Request Guidelines

### Before Opening a PR

- [ ] Code builds without errors
- [ ] All existing tests pass
- [ ] New tests written for new functionality
- [ ] No secrets or credentials committed
- [ ] Branch is up to date with its base branch

### PR Requirements

- **Title**: Short, descriptive (under 70 characters)
- **Description**: Explain what changed and why
- **Reviews**: Minimum 2 approving reviews required
- **Base branch**: `develop` for features, `master` for releases and hotfixes

### Commit Messages

Write clear, descriptive commit messages:

```
<type>: <short summary>

<optional body explaining the "why">
```

Types: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `style`, `perf`

Examples:
```
feat: add user authentication flow
fix: resolve null pointer in checkout process
docs: update API documentation for v2 endpoints
refactor: simplify database connection pooling
```

## Version Tagging

We follow [Semantic Versioning](https://semver.org/):

- **MAJOR** (x.0.0): Breaking changes
- **MINOR** (0.x.0): New features, backwards compatible
- **PATCH** (0.0.x): Bug fixes, backwards compatible

Tags are created on `master` after a release or hotfix merge: `v1.2.0`, `v1.2.1`, etc.
