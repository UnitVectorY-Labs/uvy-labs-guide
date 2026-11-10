---
layout: default
title: ghorgsync
---

# ghorgsync

`ghorgsync` is a command-line tool that clones and updates repositories from a GitHub organization or user account in a single local directory. It also audits local changes, repositories on non-default branches, and unexpected folders, making it easier to keep a workspace ready for daily development.

- **GitHub Repository**: [UnitVectorY-Labs/ghorgsync](https://github.com/UnitVectorY-Labs/ghorgsync)
- **Documentation**: [ghorgsync.unitvectorylabs.com](https://ghorgsync.unitvectorylabs.com/)

## Motivation

Working across many repositories means repeatedly cloning new projects, pulling updates, and checking which repositories still have unfinished work. As an organization grows, manually keeping a local workspace in sync becomes a daily maintenance task.

`ghorgsync` brings those tasks together in one command. A `.ghorgsync` configuration file identifies the organization or user account for that directory, with optional filters for repository visibility, archived repositories, and exclusions.

During a normal sync, it clones missing repositories, fetches existing ones, and updates their default branches. Clean repositories on another branch are switched back to their default branch automatically. Repositories with local changes are reported and have checkout and pull skipped, preserving unfinished work. Unknown folders and excluded repositories that are still present locally are reported so you can review them.

## Example

Create a directory for your organization's repositories and add a `.ghorgsync` configuration file:

```bash
mkdir -p ~/repos/myorg
cd ~/repos/myorg
cat > .ghorgsync <<'EOF'
organization: myorg
exclude_repos:
  - "^sandbox-"
EOF
```

Authenticate with the GitHub CLI, then sync the directory:

```bash
gh auth login
ghorgsync
```

This clones missing repositories and updates existing ones, reporting local changes and other findings along the way. Run `ghorgsync` again from the same directory whenever you want to refresh your workspace.

You can also check for unfinished work without fetching, switching branches, or pulling updates, or clone new repositories without processing existing checkouts:

```bash
# Report local changes and repositories on non-default branches
ghorgsync --status

# Only clone missing repositories
ghorgsync --clone
```

To sync a personal account instead, replace `organization: myorg` with `user: myusername` in `.ghorgsync`. Each directory can target either an organization or a user account.
