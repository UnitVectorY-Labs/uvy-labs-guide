---
layout: default
title: Containers
---

# Containers

Projects under UnitVectorY Labs that are published as Docker images use [GitHub Packages](https://github.com/orgs/UnitVectorY-Labs/packages) to publish artifacts.

## Development Version

The `main` branch for each GitHub repository has the most recent version and is used for development and a GitHub action is used to publish this with the `dev` tag.  This tag for the project is only intended to be used for development and could contain bugs or breaking changes.

```yaml
name: Build and Push Development Docker Images

on:
  push:
    branches: [ "main" ]
jobs:
  build-and-push:
    runs-on: ubuntu-latest
    timeout-minutes: 30
    concurrency:
      group: docker

    permissions:
      contents: read
      packages: write

    steps:
    - name: Checkout code
      uses: actions/checkout@v4
    
    - name: Set up Docker Buildx
      uses: docker/setup-buildx-action@v3
    
    - name: Login to GitHub Container Registry
      uses: docker/login-action@v3
      with:
        registry: ghcr.io
        username: ${{ github.actor }}
        password: ${{ secrets.GITHUB_TOKEN }}

    - name: Set lowercase repository name
      run: |
        echo "REPO_LC=${GITHUB_REPOSITORY,,}" >> $GITHUB_ENV

    - name: Build and push Docker image
      uses: docker/build-push-action@v6
      with:
        context: .
        push: true
        platforms: linux/amd64,linux/arm64
        tags: ghcr.io/${{ env.REPO_LC }}:dev
```

## Published Versions

Released versions of applications are triggered based on published releases of tags on GitHub.  This triggers the build of the image and uses the symantic version to create 3 tags, one for the major version, one for the major and minor version, and one for the complete tag.  This allows for clients to choose which version they want to use.

```yaml
name: Build and Push Docker Image on Release

on:
  release:
    types: [published]

jobs:
  build-and-push:
    runs-on: ubuntu-latest
    timeout-minutes: 30
    concurrency:
      group: docker

    permissions:
      id-token: write
      contents: read
      attestations: write
      packages: write

    steps:
    - name: Checkout code
      uses: actions/checkout@v4
    
    - name: Set up Docker Buildx
      uses: docker/setup-buildx-action@v3
    
    - name: Login to GitHub Container Registry
      uses: docker/login-action@v3
      with:
        registry: ghcr.io
        username: ${{ github.actor }}
        password: ${{ secrets.GITHUB_TOKEN }}

    - name: Set lowercase repository name
      run: |
        echo "REPO_LC=${GITHUB_REPOSITORY,,}" >> $GITHUB_ENV

    - name: Extract release version
      id: meta
      uses: docker/metadata-action@v5
      with:
        images: ghcr.io/${{ env.REPO_LC }}
        tags: |
          type=sha
          type=semver,pattern=v{{version}}
          type=semver,pattern=v{{major}}.{{minor}}
          type=semver,pattern=v{{major}}

    - name: Build and push Docker image
      id: push
      uses: docker/build-push-action@v6
      with:
        context: .
        push: true
        platforms: linux/amd64,linux/arm64
        tags: ${{ steps.meta.outputs.tags }}

    - name: Generate artifact attestation
      uses: actions/attest-build-provenance@v1
      with:
        subject-name: ghcr.io/${{ env.REPO_LC }}
        subject-digest: ${{ steps.push.outputs.digest }}
        push-to-registry: true
```

## Attestations

The published versions, but not the `dev` tag, all use GitHub Attestations to attest to the provenance of the build.
