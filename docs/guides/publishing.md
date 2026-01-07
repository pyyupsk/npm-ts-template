# Publishing

This guide covers the publishing workflow using Changesets.

## Overview

The template uses [Changesets](https://github.com/changesets/changesets) for:

- Version management
- Changelog generation
- Automated npm publishing

## Workflow

### 1. Make Changes

Develop your feature or fix:

```bash
git checkout -b feat/my-feature
# Make changes
git commit -m "feat: add new feature"
```

### 2. Create a Changeset

```bash
bunx changeset
```

This interactive prompt asks:

1. **Which packages?** - Select your package
2. **Bump type?** - major, minor, or patch
3. **Summary?** - Brief description

Creates a file in `.changeset/`:

```markdown
---
"@pyyupsk/npm-ts-template": minor
---

Added new feature
```

### 3. Format the Changeset

Edit the changeset file to match Keep a Changelog format:

```markdown
---
"@pyyupsk/npm-ts-template": minor
---

### Added

- New feature X for better performance
- New option `format` for custom output

### Fixed

- Null pointer error in parse function
```

This content will be added directly to `CHANGELOG.md`.

> **Note:** Changeset files are linted with markdownlint before commit.

### 4. Commit and Push

```bash
git add .
git commit -m "feat: add new feature"
git push
```

### 5. Release PR Created

The release workflow (using [changesets/action](https://github.com/changesets/action)) automatically:

1. Detects changeset files
2. Bumps version in `package.json`
3. Updates `CHANGELOG.md` with your formatted content
4. Creates PR: `chore(release): version packages`

### 6. Merge to Publish

Merge the release PR to:

1. Publish to npm
2. Create GitHub release (via changelogithub)
3. Push version tag

## CHANGELOG Format

We follow [Keep a Changelog](https://keepachangelog.com) format:

```markdown
## [1.2.0] - 2026-01-05

### Added

- New features

### Changed

- Changes to existing features

### Fixed

- Bug fixes

### Removed

- Removed features
```

## Version Types

| Type    | When to Use                       | Example       |
| ------- | --------------------------------- | ------------- |
| `patch` | Bug fixes, no API changes         | 1.0.0 → 1.0.1 |
| `minor` | New features, backward compatible | 1.0.0 → 1.1.0 |
| `major` | Breaking changes                  | 1.0.0 → 2.0.0 |

## Changeset Examples

### Bug Fix (patch)

```markdown
---
"@pyyupsk/npm-ts-template": patch
---

### Fixed

- Null pointer error in parse function
- Memory leak in event handler
```

### New Feature (minor)

```markdown
---
"@pyyupsk/npm-ts-template": minor
---

### Added

- `format` option to customize output
- Support for async callbacks
```

### Breaking Change (major)

```markdown
---
"@pyyupsk/npm-ts-template": major
---

### Changed

- **BREAKING:** Rename `parse` to `parseInput`

### Migration

Replace `parse(x)` with `parseInput(x)`
```

## Configuration

The `.changeset/config.json` controls behavior:

::: tip Why local `$schema`?
We use `../node_modules/...` instead of remote URLs. This ensures the schema matches your installed package version, works offline, and provides accurate autocomplete in your editor.
:::

```json
{
  "$schema": "../node_modules/@changesets/config/schema.json",
  "changelog": "@changesets/cli/changelog",
  "commit": false,
  "fixed": [],
  "linked": [],
  "access": "public",
  "baseBranch": "main",
  "updateInternalDependencies": "patch",
  "ignore": []
}
```

Key settings:

- `changelog` - Changelog generator (uses content from changeset files)
- `access: "public"` - Publish as public package
- `baseBranch: "main"` - PR target branch

## npm Setup

### For New Packages

1. Create npm account at [npmjs.com](https://www.npmjs.com/)
2. Generate access token (Automation type)
3. Add `NPM_TOKEN` secret to GitHub repository

### Scoped Packages

For `@scope/package-name`:

1. Create or join an npm organization
2. Ensure `access: "public"` in changeset config

## Manual Publishing

If needed, publish manually:

```bash
# Build first
bun run build

# Publish
npm publish --access public
```

## Troubleshooting

### Release PR Not Created

- Ensure `.changeset/*.md` files exist (not just README.md)
- Check GitHub Actions logs
- Verify workflow has PR creation permissions

### Publish Failed

- Verify `NPM_TOKEN` is set correctly
- Check npm account permissions
- Ensure package name is available

### Markdownlint Errors

Fix formatting issues in changeset files:

```bash
# Check manually
bunx markdownlint-cli2 ".changeset/*.md"
```

Common fixes:

- Add blank line after headings
- Remove trailing spaces
- Use consistent list markers
