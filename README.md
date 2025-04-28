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

## Releases

This action follows semantic versioning. You can use it in your workflows in several ways:

- `@v1` - Use the latest release of major version 1
- `@v1.2` - Use the latest release of version 1.2.x
- `@v1.2.3` - Use the specific version 1.2.3
- `@main` - Use the latest code from the main branch (may be unstable)

For production use, we recommend pinning to a major version like `@v1` to automatically receive compatible bug fixes and new features.

## Contributing

We welcome contributions to improve this GitHub Action! This project uses automated versioning based on commit message conventions.

### Commit Message Conventions

When contributing to this project, please follow these commit message conventions to help our automated release system determine the appropriate version bump:

| Prefix | Version Bump | Example | Description |
|--------|--------------|---------|-------------|
| `BREAKING CHANGE:` or `MAJOR:` | Major (x.0.0) | `BREAKING CHANGE: Renamed input parameters` | Use for incompatible changes that require users to modify their workflows |
| `FEAT:`, `FEATURE:`, or `MINOR:` | Minor (0.x.0) | `FEAT: Added support for custom wasm-opt version` | Use for new features that don't break existing functionality |
| Any other prefix | Patch (0.0.x) | `Fix: Corrected path handling in Windows` | Use for bug fixes and minor improvements |

### Automated Release Process

When code is merged to the main branch:

1. Our automation analyzes commit messages since the last release
2. It determines the appropriate version bump based on the conventions above
3. A new tag is created and pushed automatically
4. A GitHub release is generated with a changelog of all commits

This means you don't need to manually create tags or releases - just follow the commit message conventions when merging PRs.

### Development Workflow

1. Fork the repository
2. Create a feature branch (`git checkout -b my-new-feature`)
3. Make your changes
4. Commit with an appropriate prefix (`git commit -m "FEAT: Add new feature"`)
5. Push to your branch (`git push origin my-new-feature`)
6. Create a new Pull Request

### Testing Locally

To test this action locally before submitting a PR:

1. Make changes to the action files
2. Create a test workflow in your own repository that uses your fork of this action
3. Verify that the action works as expected

## License

Apache License 2.0
