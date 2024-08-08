---
layout: default
title: Tofu Documentation
---

# Tofu Documentation

For custom developed Tofu modules the [terraform-docs/terraform-docs](https://github.com/terraform-docs/terraform-docs) project is used in the form of a GitHub action via [terraform-docs/gh-actions](https://github.com/terraform-docs/gh-actions).

This GitHub Action is specified in `.github/workflows/documentation.yml` with the following:

```xml
name: Generate terraform docs
on:
  - pull_request
jobs:
  docs:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
      with:
        ref: ${{ github.event.pull_request.head.ref }}

    - name: Render terraform docs inside the README.md and push changes back to PR branch
      uses: terraform-docs/gh-actions@v1.2.0
      with:
        working-dir: .
        output-file: README.md
        output-method: inject
        git-push: "true"
```

This allows for the documentation on the README file to be generated between the following:

```
<!-- BEGIN_TF_DOCS -->
GENERATED CONTENT HERE
<!-- END_TF_DOCS -->
```