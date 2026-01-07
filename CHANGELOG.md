# Changelog

## 0.1.1

### Patch Changes

- Refactored release workflow to use official `changesets/action`
- Extended `@tsconfig/strictest` for multi-target flexibility
- Updated changelog format to match changesets style
- Fixed CI workflow npm authentication and tag publishing
- Fixed release workflow issues
- Fixed esbuild vulnerability (GHSA-67mh-4wv8-2f99) via package override

## 0.1.0

### Minor Changes

- Added ESLint with eslint-plugin-jsdoc for documentation enforcement
- Added ESLint with eslint-plugin-sonarjs for code quality analysis
- Added VitePress documentation site with guides and configuration docs
- Added GitHub Actions workflow for docs deployment to GitHub Pages
- Added Markdownlint for changeset file validation
- Updated README to focus on template usage with quick start guide

## 0.0.0

### Initial Release

- Initial TypeScript library template with Bun, tsdown, Biome, Vitest
- Lefthook for git hooks with commitlint
- Changesets for versioning and publishing
- GitHub Actions for CI/CD
