# Publishing

This guide covers the publishing workflow using Changesets.

## Overview

The template uses [Changesets](https://github.com/changesets/changesets) for:

- Version management
- Changelog generation
- Automated npm publishing

## Workflow

### 1. Make Changes

Develop your feature or fix on a branch:

```bash
git checkout -b feat/my-feature
# Make changes
git commit -m "feat: add new feature"
```

### 2. Create a Changeset

Before merging, create a changeset:

```bash
bun run changeset
```

This interactive prompt asks:

1. **Which packages?** - Select your package
2. **Bump type?** - major, minor, or patch
3. **Summary?** - Describe the change

A file is created in `.changeset/`:

```markdown
---
"your-package": minor
---

Add new feature for better UX
```

### 3. Commit the Changeset

```bash
git add .changeset
git commit -m "chore: add changeset"
git push
```

### 4. Merge to Main

When your PR is merged, the release workflow:

1. Detects changeset files
2. Creates a "Version Packages" PR
3. This PR updates version and CHANGELOG.md

### 5. Release

Merge the "Version Packages" PR to:

1. Update package.json version
2. Update CHANGELOG.md
3. Publish to npm
4. Create a GitHub release

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
"your-package": patch
---

Fix null pointer error in parse function
```

### New Feature (minor)

```markdown
---
"your-package": minor
---

Add `format` option to customize output
```

### Breaking Change (major)

```markdown
---
"your-package": major
---

BREAKING: Rename `parse` to `parseInput`

Migration:

- Replace `parse(x)` with `parseInput(x)`
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

### "Version Packages" PR Not Created

- Ensure `.changeset/*.md` files exist
- Check GitHub Actions logs

### Publish Failed

- Verify `NPM_TOKEN` is set correctly
- Check npm account permissions
- Ensure package name is available

### Wrong Version

- Delete the changeset file
- Create a new one with correct bump type
