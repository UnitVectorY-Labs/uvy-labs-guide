---
layout: default
title: Custom Properties
---

# Custom Properties

GitHub allows for [Custom Properties](https://docs.github.com/en/organizations/managing-organization-settings/managing-custom-properties-for-repositories-in-your-organization) to be set on your repositories.

GitHub's documentation describes custom properties as a way to "...allow you to decorate your repositories with information such as compliance frameworks, data sensitivity, or project details."

In the case of UnitVectorY Labs these properies are used to describe the characteristis of the repository to help with automated analysis of the repositories configuration.

## Project Status

The `project-status` property is used to specify the development status of the project matching the badge that is included in the README.md

The [status]({{ site.baseurl }}{% link _bestpractices/status.md %}) page describes what each of these status levels mean.

- `Unknown`
- `Concept`
- `Work in Progress`
- `Active`
- `Suspended`
- `Abandoned`

## Programming Language

The `programming-language` property is used to specify which programming language is used by the project.

- `unknown` is used as the default option as this property is mandatory
- `java-17` is used for Java 17 projects
- `go` is use for Go projects

## Project Type

The `project-type` property is used to specify the type of project is used.

- `unknown` is used as the default option as this property is mandatory
- `documentation` is used for a project that is just used for documentation
- `java-maven-library` is used for a Java Maven Library
- `java-docker` is used for a Java application distributed inside a Docker image
- `go-utility` is a command line application written in Go
- `go-docker` is used for a Go application distributed inside a Docker image
- `opentofu-module` is a OpenTofu module that is meant to be used by other projects
- `opentofu-deployment` is a complete OpenTofu project meant to deploy to an envirionment

# Distribution

The `distribution` is used to specify how the project is distributed.

- `unknown` is used as the default option as this property is mandatory
- `maven-central` is used for Java applications published to Maven Central
- `github-repository` is used when the distribution is intended to be throught he GitHub repository itself
- `github-packages` is used when the artifact is published to GitHub Packages

