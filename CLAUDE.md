# Claude Code Instructions

## Branching Strategy

This project follows **Git Flow**. Always adhere to these rules:

### Branch Rules

- `master` — Production-ready code. Never commit directly. Only receives merges from `release/*` and `hotfix/*` branches.
- `develop` — Integration branch. Never commit directly. Only receives merges from `feature/*` and `release/*` branches.
- `feature/*` — Branch from `develop`, merge back into `develop` via PR.
- `release/*` — Branch from `develop`, merge into `master` AND back into `develop`.
- `hotfix/*` — Branch from `master`, merge into `master` AND back into `develop`.

### Branch Naming

- Features: `feature/SHORT-DESCRIPTION` or `feature/TICKET-ID-description`
- Releases: `release/MAJOR.MINOR.PATCH`
- Hotfixes: `hotfix/SHORT-DESCRIPTION`
- Use lowercase and hyphens only.

### When Creating Branches

- Always pull the latest from the base branch before branching.
- For new features: `git checkout develop && git pull && git checkout -b feature/name`
- For releases: `git checkout develop && git pull && git checkout -b release/x.y.z`
- For hotfixes: `git checkout master && git pull && git checkout -b hotfix/name`

### When Creating PRs

- Feature PRs target `develop` as the base branch.
- Release PRs target `master` as the base branch.
- Hotfix PRs target `master` as the base branch.
- Always include a descriptive title and summary.

### Commit Messages

Use conventional commit format: `<type>: <description>`
Types: feat, fix, docs, refactor, test, chore, style, perf

### Protected Branches

- Never force-push to `master` or `develop`.
- Never commit directly to `master` or `develop` — always use PRs.
- Never delete `master` or `develop`.

### After Merging

- After merging a release into `master`, remind the user to tag the release: `git tag -a vX.Y.Z -m "Release X.Y.Z"`
- After merging a release or hotfix into `master`, also merge back into `develop`.
- Delete feature, release, and hotfix branches after they are merged.

## Project Info

- Repository: github.com/etafoh/cursor-claude
- Primary language: HTML/CSS/JavaScript
- This is the NetBiz AI Consultancy website.
