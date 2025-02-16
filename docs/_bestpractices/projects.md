---
layout: default
title: Projects
---

# Projects

The issues and pull requests for UnitVectorY-Labs repositories are automatically added to the [UnitVectorY Labs Project](https://github.com/orgs/UnitVectorY-Labs/projects/41/views/1).

This allows for tracking, organization, and management of issues across all repositories.

## GitHub Actions

The pattern with GitHub to have a large number of projects track their issues and/or pull requests in a single project must utilize a GitHub Action, [actions/add-to-project](https://github.com/actions/add-to-project).

`.github/workflows/add-to-project.yml`

```yaml
name: Add all issues and pull requests to project

on:
  issues:
    types:
      - opened
  pull_request:
    types:
      - opened

jobs:
  add-to-project:
    name: Add to project
    runs-on: ubuntu-latest
    steps:
      - uses: actions/add-to-project@v1.0.2
        with:
          project-url: https://github.com/orgs/UnitVectorY-Labs/projects/41
          github-token: ${{ secrets.PROJECT_GITHUB_ACTION }}
```
