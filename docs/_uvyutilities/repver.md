---
layout: default
title: repver
---

# repver

`repver` (short for "replace version") is a command-line tool that automates batch replacement of simple strings—like version numbers—across multiple files in a Git repository, and optionally handles the entire pull request workflow with a single command.

- **GitHub Repository**: [UnitVectorY-Labs/repver](https://github.com/UnitVectorY-Labs/repver)
- **Documentation**: [repver.unitvectorylabs.com](https://repver.unitvectorylabs.com/)

## Motivation

Keeping version numbers and other shared strings consistent across a repository is tedious and error-prone when done manually. Dependabot handles dependencies it understands, but it won't update version strings embedded in documentation, Dockerfiles, CI configuration, or other custom metadata.

`repver` fills that gap. You describe an update once in a `.repver` configuration file—which files to touch, which line patterns to match, and what Git operations to perform—and then run a single command to apply that update consistently across however many files or repositories you need.

A typical `repver` run can:

1. Create a new branch for the change
2. Update multiple files by replacing a matched string with the new value
3. Commit the changes
4. Push the branch to the remote repository
5. Create a pull request via the GitHub CLI
6. Switch back to the original branch and delete the local branch

## Example

The following `.repver` configuration updates Go version references in both `go.mod` and a GitHub Actions workflow file, then opens a pull request:

```yaml
commands:
  - name: "goversion"
    params:
      - name: "version"
        pattern: "^(?P<major>0|[1-9]\\d*)\\.(?P<minor>0|[1-9]\\d*)\\.(?P<patch>0|[1-9]\\d*)$"
    targets:
      - path: "go.mod"
        pattern: "^go (?P<version>.*) // GOVERSION$"
        transform: "{{major}}.{{minor}}"
      - path: ".github/workflows/build-go.yml"
        pattern: "^          go-version: '(?P<version>.*)' # GOVERSION$"
        transform: "{{major}}.{{minor}}.{{patch}}"
    git:
      create_branch: true
      branch_name: "repver/go-v{{version}}"
      commit: true
      commit_message: "Update Go version to {{version}}"
      push: true
      remote: "origin"
      pull_request: "GITHUB_CLI"
      return_to_original_branch: true
      delete_branch: true
```

With this configuration in place, updating to Go 1.23.4 is a single command:

```
repver --command=goversion --param-version=1.23.4
```

`repver` matches the annotated lines in each target file, replaces the version value with the appropriate transform, and drives the full Git workflow automatically.
