# Changelog

## 0.1.1

### Patch Changes

- 5d060c9: ### Changed

  - Refactored release workflow to use official `changesets/action`
  - Extended `@tsconfig/strictest` for multi-target flexibility

  ### Fixed

  - CI workflow npm authentication and tag publishing
  - Release workflow issues

  ### Security

  - Fixed esbuild vulnerability (GHSA-67mh-4wv8-2f99) via package override

All notable changes to this project will be documented in this file.

## [0.1.0] - 2026-01-05

### Added

- ESLint with eslint-plugin-jsdoc for documentation enforcement
- ESLint with eslint-plugin-sonarjs for code quality analysis
- VitePress documentation site with guides and configuration docs
- GitHub Actions workflow for docs deployment to GitHub Pages
- Markdownlint for changeset file validation
- Custom release workflow with dynamic version in commit message

### Changed

- README updated to focus on template usage with quick start guide
- CHANGELOG.md now follows Keep a Changelog format
- Release workflow uses custom script instead of changesets/action

## [0.0.0] - 2026-01-05

### Added

- Initial TypeScript library template with Bun, tsdown, Biome, Vitest
- Lefthook for git hooks with commitlint
- Changesets for versioning and publishing
- GitHub Actions for CI/CD
