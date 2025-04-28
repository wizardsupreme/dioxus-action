# Dioxus GitHub Action

A GitHub Action for building Dioxus applications with WASM support.

## Usage

```yaml
steps:
  - uses: actions/checkout@v3
  
  - name: Build Dioxus App
    uses: wizardsupreme/dioxus-action@v1
    with:
      # Optional: Specify Rust version (default: stable)
      rust-version: 'stable'
      
      # Optional: Specify Dioxus CLI version, tag, or branch (default: latest)
      # - When using default repo: specifies version from crates.io
      # - When using custom repo: specifies tag (if starts with 'v' or a number) or branch
      cli-version: 'my-feature-branch'
      
      # Optional: Specify GitHub repository for Dioxus CLI (format: owner/repo)
      cli-repo: 'wizardsupreme/dioxus'
      
      # Optional: Custom build command (default: dx build --release)
      build-command: 'dx build --release --features web'
      
      # Optional: Working directory (default: .)
      working-directory: './my-dioxus-app'
      
      # Optional: Enable/disable caching (default: true)
      cache: 'true'
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `rust-version` | Rust version to use | No | `stable` |
| `cli-version` | Dioxus CLI version, tag, or branch name | No | `latest` |
| `cli-repo` | GitHub repository to install Dioxus CLI from | No | `dioxuslabs/dioxus` |
| `build-command` | Custom build command | No | `dx build --release` |
| `working-directory` | Directory containing the Dioxus project | No | `.` |
| `cache` | Whether to cache dependencies | No | `true` |

## Example Workflow

```yaml
name: Build Dioxus App

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Build Dioxus App
        uses: wizardsupreme/dioxus-action@v1
        with:
          repo: 'wizardsupreme/dioxus'
          version: 'feature-branch'
          cache: 'true'
```

## License

Apache License 2.0
