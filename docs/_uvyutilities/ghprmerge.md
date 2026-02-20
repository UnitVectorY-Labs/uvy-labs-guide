---
layout: default
title: ghprmerge
---

# ghprmerge

`ghprmerge` is a command-line tool that automatically evaluates, rebases, and merges GitHub pull requests sharing the same source branch across an entire organization—without requiring you to click through each repository individually.

- **GitHub Repository**: [UnitVectorY-Labs/ghprmerge](https://github.com/UnitVectorY-Labs/ghprmerge)
- **Documentation**: [ghprmerge.unitvectorylabs.com](https://ghprmerge.unitvectorylabs.com/)

## Motivation

When you maintain many repositories under a GitHub organization, automated dependency update tools like Dependabot can quickly generate dozens or hundreds of open pull requests. Reviewing, rebasing, and merging each one by navigating to every repository becomes impractical.

`ghprmerge` solves this by letting you act on all matching pull requests across your organization from a single command. It operates entirely through the GitHub API—no local checkouts—and is **safe by default**: without explicit action flags it only reports what it would do, never making changes unless you opt in.

A PR is only merged when it is fully ready: all checks passing, no merge conflicts, and the branch up to date with the default branch (unless `--skip-rebase` is used).

## Example

```bash
# Set your GitHub token
export GITHUB_TOKEN=ghp_xxxxxxxxxxxx

# Step 1: Analyze what's available (no changes made)
ghprmerge --org myorg --source-branch dependabot/

# Step 2: Rebase out-of-date branches (with confirmation prompt)
ghprmerge --org myorg --source-branch dependabot/ --rebase --confirm

# Step 3: Merge PRs that are ready
ghprmerge --org myorg --source-branch dependabot/ --merge
```

You can also scope the run to specific repositories or limit how many are processed at once:

```bash
# Only process two specific repos
ghprmerge --org myorg --source-branch dependabot/ --repo repo1 --repo repo2 --merge

# Cap the run at 10 repositories
ghprmerge --org myorg --source-branch dependabot/ --repo-limit 10 --merge
```

For automation or scripting, structured JSON output is available:

```bash
ghprmerge --org myorg --source-branch dependabot/ --json | jq '.summary'
```
