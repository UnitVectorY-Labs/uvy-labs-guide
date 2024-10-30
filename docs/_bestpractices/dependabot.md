---
layout: default
title: Dependabot
---

# Dependabot

[Dependabot](https://docs.github.com/en/code-security/dependabot) is a tool that automatically updates dependencies in a project.  It is a GitHub application that creates pull requests to update dependencies in a project.  The pull requests are created when a new version of a dependency is available.

UnitVectorY labs project are configured to automatically update dependencies using Dependabot.

The current convention for UnitVectorY labs is weekly updates on Saturday at 7:00 AM Eastern Time.

## Example Configuration

The file `.github/dependabot.yml` is used to configure Dependabot.  The following is an example configuration file for a Java project:

```yaml
# To get started with Dependabot version updates, you'll need to specify which
# package ecosystems to update and where the package manifests are located.
# Please see the documentation for all configuration options:
# https://docs.github.com/code-security/dependabot/dependabot-version-updates/configuration-options-for-the-dependabot.yml-file

version: 2
updates:
  - package-ecosystem: "maven"
    directory: "/"
    schedule:
      interval: "weekly"
      day: "saturday"
      time: "07:00"
      timezone: "America/New_York"
    open-pull-requests-limit: 20
  - package-ecosystem: "github-actions"
    directory: "/"
    schedule:
      interval: "weekly"
      day: "saturday"
      time: "07:00"
      timezone: "America/New_York"
    open-pull-requests-limit: 20
  - package-ecosystem: "devcontainers"
    directory: "/"
    schedule:
      interval: weekly
      day: "saturday"
      time: "07:00"
      timezone: "America/New_York"
    open-pull-requests-limit: 20
```

This configuration file updates Maven dependencies, GitHub Actions, and Devcontainers weekly on Saturday at 7:00 AM Eastern Time.

Other programming languages such as JavaScript can be configured to use Dependabot.  The following is an example configuration file for a JavaScript project:

```yaml
# To get started with Dependabot version updates, you'll need to specify which
# package ecosystems to update and where the package manifests are located.
# Please see the documentation for all configuration options:
# https://docs.github.com/code-security/dependabot/dependabot-version-updates/configuration-options-for-the-dependabot.yml-file

version: 2
updates:
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "weekly"
      day: "saturday"
      time: "07:00"
      timezone: "America/New_York"
    open-pull-requests-limit: 20
```

The following is the example for a Go project:

```yaml
# To get started with Dependabot version updates, you'll need to specify which
# package ecosystems to update and where the package manifests are located.
# Please see the documentation for all configuration options:
# https://docs.github.com/code-security/dependabot/dependabot-version-updates/configuration-options-for-the-dependabot.yml-file

version: 2
updates:
  - package-ecosystem: "gomod"
    directory: "/"
    schedule:
      interval: "weekly"
      day: "saturday"
      time: "07:00"
      timezone: "America/New_York"
    open-pull-requests-limit: 20
```

The following is an example for a repository using Terraform:

```
# To get started with Dependabot version updates, you'll need to specify which
# package ecosystems to update and where the package manifests are located.
# Please see the documentation for all configuration options:
# https://docs.github.com/code-security/dependabot/dependabot-version-updates/configuration-options-for-the-dependabot.yml-file

version: 2
updates:
  - package-ecosystem: "github-actions"
    directory: "/"
    schedule:
      interval: "weekly"
      day: "saturday"
      time: "07:00"
      timezone: "America/New_York"
    open-pull-requests-limit: 20
  - package-ecosystem: 'terraform'
    directory: '/'
    schedule:
      interval: "weekly"
      day: "saturday"
      time: "07:00"
      timezone: "America/New_York"
    open-pull-requests-limit: 20
```

The following is an example for a repository using gitsubmodules:

```yaml
# To get started with Dependabot version updates, you'll need to specify which
# package ecosystems to update and where the package manifests are located.
# Please see the documentation for all configuration options:
# https://docs.github.com/code-security/dependabot/dependabot-version-updates/configuration-options-for-the-dependabot.yml-file

version: 2
updates:
  - package-ecosystem: "gitsubmodule"
    directory: "/"
    schedule:
      interval: "weekly"
      day: "saturday"
      time: "07:00"
      timezone: "America/New_York"
    open-pull-requests-limit: 20
  - package-ecosystem: "github-actions"
    directory: "/"
    schedule:
      interval: "weekly"
      day: "saturday"
      time: "07:00"
      timezone: "America/New_York"
    open-pull-requests-limit: 20
```
