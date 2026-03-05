# Action to release a R package

This action allows you to prepare the R package before, during and after the release process on GitHub.
It includes version bumping, changelog update, tagging, and preparing a GitHub draft release.


## 🚀 Features

- Validation of the version tags (`vX.Y.Z`)
- Updates `DESCRIPTION` and `NEWS.md` automatically
- Merges between **develop** and **main** branches
- Creates a version tag and a GitHub draft release
- Bumps the development version after release


## 🧩 Example usage

### Basic example (no dev/main distinction)

```yaml
name: Publish Release

on:
  workflow_dispatch:
    inputs:
      tag:
        description: "Release tag (e.g. v1.2.0)"
        required: true
        type: string

jobs:
  release:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - uses: actions/checkout@v4

      - uses: TanguyBarthelemy/r-release-action@v1.0.1
        with:
          tag: ${{ github.event.inputs.tag }}
          gh_repo: "TanguyBarthelemy/IssueTrackeR"
          github_token: ${{ github.token }}
```


## Advanced example (with main and develop branches)

```yaml
name: Publish Release

on:
  workflow_dispatch:
    inputs:
      tag:
        description: "Release tag (e.g. v1.2.0)"
        required: true
        type: string

jobs:
  release:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    env:
      GITHUB_PAT: ${{ secrets.WORKFLOW_TOKEN }}

    steps:
      - uses: actions/checkout@v4

      - uses: TanguyBarthelemy/r-release-action@v1.0.1
        with:
          tag: ${{ github.event.inputs.tag }}
          gh_repo: "TanguyBarthelemy/IssueTrackeR"
          main-branch: "main"
          dev-branch: "develop"
          github_token: ${{ env.GITHUB_PAT }}
```


## Workflow:

1) Validation of the version tags (`vX.Y.Z`)
2) Checkout develop branch
3) Updates `DESCRIPTION` and `NEWS.md` (with the [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) convention) automatically
4) Commit the changes
5) Checkout to main branch and merge develop -> main
6) Create new tag version
7) Checkout to develop branch and merge back main -> develop
8) Bumps the development version
9) Commit develop version
10) Push main, develop and tag
11) Creates a GitHub draft release


## ⚙️ Inputs

| Name | Required | Description |
|------|-----------|-------------|
| `tag` | ✅ | New version tag (e.g. `v1.2.3`) |
| `gh_repo` | ✅ | Repository name in the form `user/repo` |
| `github_token` | ✅ | GitHub token with `contents: write` permission |
| `main-branch` | ❌ | Main branch name (defaults to repository’s default branch) |
| `dev-branch` | ❌ | Development branch name (optional) |


## 🔒 Authentication

The action requires a GitHub token with permission to push commits and create releases.

### Option 1 — Default GitHub token (recommended)

```yaml
permissions:
  contents: write

github_token: ${{ github.token }}
```

GitHub automatically provides a temporary token with appropriate rights.


### Option 2 — Personal Access Token (PAT)

If you need to push across organizations or private repositories, create a secret (e.g. WORKFLOW_TOKEN) with your PAT:

```yaml
env:
  GITHUB_PAT: ${{ secrets.WORKFLOW_TOKEN }}

steps:
  - uses: TanguyBarthelemy/r-release-action@v1.0.1
    with:
      github_token: ${{ env.GITHUB_PAT }}
```


## 🧰 dependencies

The action automatically installs:

- R
- The [{releaser}](http://github.com/tanguyBarthelemy/releaser) R package
- The [{desc}](https://github.com/r-lib/desc) R package
- the `softprops/action-gh-release` github action
