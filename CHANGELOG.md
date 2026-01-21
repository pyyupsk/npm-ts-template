# Changelog

All notable changes to this project will be documented in this file.

## [0.2.0] - 2026-01-21

### 🚀 Features

- Add repository setup script and Dependabot config

### 🚜 Refactor

- _(tooling)_ Migrate from Biome to Prettier and ESLint

### 📚 Documentation

- Update documentation for Prettier and git-cliff migration

## [0.1.2] - 2026-01-16

### 🚀 Features

- _(ci)_ Switch to git-cliff for changelog generation

### 🐛 Bug Fixes

- _(ci)_ Integrate changelogithub into release workflow
- _(ci)_ Avoid expanding secrets in run block
- _(ci)_ Use setup-node for secure npm authentication
- _(ci)_ Use GH_PAT for checkout to bypass branch ruleset

### 🚜 Refactor

- _(ci)_ Replace changesets with manual release workflow

## [0.1.1] - 2026-01-07

### 🐛 Bug Fixes

- _(ci)_ Configure npm auth for publishing
- _(ci)_ Pass npm token via env variable, push tags after publish
- _(ci)_ Resolve release workflow issues ([#3](https://github.com/pyyupsk/npm-ts-template/issues/3))
- _(deps)_ Override esbuild to fix security vulnerability
- _(ci)_ Wrap version command in bash for shell operators
- _(ci)_ Use single quotes for bash command
- _(ci)_ Add changeset:version script to avoid shell quoting issues

### 🚜 Refactor

- _(ts)_ Extend `@tsconfig/strictest` for multi-target flexibility
- _(ci)_ Use changesets/action for release workflow

### ⚙️ Miscellaneous Tasks

- Add changeset for v0.1.1

## [0.1.0] - 2026-01-05

### 🚀 Features

- Add ESLint with JSDoc linting
- Add SonarJS ESLint plugin for code quality analysis

### 🐛 Bug Fixes

- _(ci)_ Use dynamic version in release commit message
- _(ci)_ Add GITHUB_TOKEN for changelog-github plugin

### 📚 Documentation

- Add VitePress documentation site
- Add favicon for documentation site
- Add documentation guide and update CI/CD guide
- Add repository settings documentation to CI/CD guide

### ⚙️ Miscellaneous Tasks

- Add GitHub Actions workflow for docs deployment
- Move permissions to job level in docs workflow
- Add changeset for v0.1.0 and configure changelog-github

## [0.0.0] - 2026-01-05

### 🚀 Features

- Add project tooling, source, and tests
- Add GitHub workflows and project configuration
- Add changelog workflow for release notes generation

### ⚙️ Miscellaneous Tasks

- Initial project setup
- Scope package under @pyyupsk namespace
