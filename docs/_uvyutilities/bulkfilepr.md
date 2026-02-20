---
layout: default
title: bulkfilepr
---

# bulkfilepr

`bulkfilepr` is a command-line tool for batch-updating standardized files across many local GitHub repositories. It handles everything from creating a new branch to pushing the change and opening a pull request, so you don't have to manually repeat that workflow for every repository.

- **GitHub Repository**: [UnitVectorY-Labs/bulkfilepr](https://github.com/UnitVectorY-Labs/bulkfilepr)
- **Documentation**: [bulkfilepr.unitvectorylabs.com](https://bulkfilepr.unitvectorylabs.com/)

## Motivation

Keeping shared files consistent across many repositories—GitHub Actions workflows, CODEOWNERS files, issue templates, Dockerfiles, lint configurations—requires the same repetitive git workflow every time: switch to the default branch, create a branch, copy the file, commit, push, open a PR. Multiply that by tens or hundreds of repositories and it becomes a significant maintenance burden.

`bulkfilepr` automates that entire sequence with a single command. It is conservative by design: it refuses to run against anything other than a clean working tree on the default branch, supports three update modes to avoid unintended overwrites, and provides a dry-run option so you can audit changes before applying them.

## Example

Update a CI workflow file across a repository:

```bash
bulkfilepr apply \
  --mode upsert \
  --repo-path .github/workflows/ci.yml \
  --new-file ~/standards/ci.yml
```

This single command:

1. Verifies you are on the default branch with a clean working tree
2. Creates a new branch (e.g., `bulkfilepr/a1b2c3d4e5f6`)
3. Copies the new file content to `.github/workflows/ci.yml`
4. Commits the changes
5. Pushes the branch to origin
6. Opens a pull request via the GitHub CLI
7. Switches back to the default branch

For a safe rollout across many repositories, use `--dry-run` first to preview what would change:

```bash
for repo_dir in ~/work/myorg/*; do
  [ -d "$repo_dir/.git" ] || continue
  echo "=== $repo_dir ==="
  (
    cd "$repo_dir"
    bulkfilepr apply \
      --mode exists \
      --repo-path .github/workflows/ci.yml \
      --new-file ~/standards/ci.yml \
      --dry-run
  )
done
```

You can also use the `match` mode to update files only when they match a known baseline hash, preventing accidental overwrites of customized files:

```bash
bulkfilepr apply \
  --mode match \
  --repo-path .github/workflows/ci.yml \
  --new-file ~/standards/ci-v3.yml \
  --expect-sha256 "4b7c0e1a2b3c4d5e..."
```
