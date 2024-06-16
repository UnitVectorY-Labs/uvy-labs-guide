---
layout: default
title: Custom Properties
parent: Best Practices
---

# Custom Properties

GitHub allows for [Custom Properties](https://docs.github.com/en/organizations/managing-organization-settings/managing-custom-properties-for-repositories-in-your-organization) to be set on your repositories.

GitHub's documentation describes custom properties as a way to "...allow you to decorate your repositories with information such as compliance frameworks, data sensitivity, or project details."

In the case of UnitVectorY Labs these properies are used to describe the characteristis of the repository to help with automated analysis of the repositories configuration.

## Programming Language

The `programming-language` is used to specify which programming language is used by the project.

The following programming language options are available

- `unknown` is used as the default option as this property is mandatory
- `java-17` is used for Java 17 projects

## Project Type

The `project-type` is used to specify the type of project is used.

- `unknown` is used as the default option as this property is mandatory
- `documentation` is used for a project that is just used for documentation
- `java-maven-library` is used for a Java Maven Library
