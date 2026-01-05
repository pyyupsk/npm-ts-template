# CI/CD

This guide covers the GitHub Actions workflows included in the template.

## Workflows

### CI Workflow

**File:** `.github/workflows/ci.yml`

Runs on every push and pull request:

```yaml
name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: oven-sh/setup-bun@v2
      - run: bun install
      - run: bun run build
      - run: bun run lint
      - run: bun run typecheck
      - run: bun run test:coverage
```

#### Checks Performed

| Check     | Command                 | Purpose              |
| --------- | ----------------------- | -------------------- |
| Build     | `bun run build`         | Package builds       |
| Lint      | `bun run lint`          | Code quality         |
| Typecheck | `bun run typecheck`     | Type safety          |
| Test      | `bun run test:coverage` | Tests pass, coverage |

### Release Workflow

**File:** `.github/workflows/release.yml`

Handles versioning and publishing:

```yaml
name: Release

on:
  push:
    branches: [main]

jobs:
  release:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: oven-sh/setup-bun@v2
      - run: bun install
      - uses: changesets/action@v1
        with:
          publish: bun run release
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          NPM_TOKEN: ${{ secrets.NPM_TOKEN }}
```

#### What It Does

1. Detects changeset files
2. Creates "Version Packages" PR if changesets exist
3. When PR is merged, publishes to npm

### Changelog Workflow

**File:** `.github/workflows/changelog.yml`

Generates release notes on tag push:

```yaml
name: Changelog

on:
  push:
    tags:
      - "v*"

jobs:
  changelog:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0
      - run: bunx changelogithub
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## Branch Protection

Recommended settings for the `main` branch:

1. Go to Settings → Branches → Add rule
2. Branch name pattern: `main`
3. Enable:
   - Require a pull request before merging
   - Require status checks to pass
   - Select: `build` job from CI workflow

## Secrets

Required secrets in repository settings:

| Secret         | Purpose        | How to Get                |
| -------------- | -------------- | ------------------------- |
| `GITHUB_TOKEN` | Auto-provided  | Automatic                 |
| `NPM_TOKEN`    | npm publishing | npmjs.com → Access Tokens |

### Adding NPM_TOKEN

1. Go to [npmjs.com](https://www.npmjs.com/) → Access Tokens
2. Generate New Token → Automation
3. In GitHub: Settings → Secrets → Actions → New secret
4. Name: `NPM_TOKEN`, Value: your token

## Customization

### Adding Node.js Matrix

Test on multiple Node versions:

```yaml
jobs:
  build:
    strategy:
      matrix:
        node: [20, 22]
    steps:
      - uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node }}
```

### Adding Coverage Upload

Upload to Codecov:

```yaml
- name: Upload coverage
  uses: codecov/codecov-action@v4
  with:
    token: ${{ secrets.CODECOV_TOKEN }}
```

### Adding SonarCloud

```yaml
- name: SonarCloud Scan
  uses: SonarSource/sonarcloud-github-action@master
  env:
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
    SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
```

## Debugging

### View Workflow Logs

1. Go to Actions tab
2. Click on workflow run
3. Click on job to see logs

### Re-run Failed Workflow

1. Go to failed workflow run
2. Click "Re-run jobs" → "Re-run failed jobs"

### Skip CI

Add `[skip ci]` to commit message:

```bash
git commit -m "docs: update readme [skip ci]"
```
