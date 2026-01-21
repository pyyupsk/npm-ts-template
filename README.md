# npm-ts-template

[![CI](https://github.com/pyyupsk/npm-ts-template/actions/workflows/ci.yml/badge.svg)](https://github.com/pyyupsk/npm-ts-template/actions/workflows/ci.yml)
[![npm version](https://img.shields.io/npm/v/@pyyupsk/npm-ts-template)](https://www.npmjs.com/package/@pyyupsk/npm-ts-template)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Zero-config TypeScript library template with Bun, tsdown, Prettier, ESLint, Vitest, and git-cliff.

## Features

- **TypeScript 5.x** with `@tsconfig/strictest` for maximum type safety
- **Dual ESM/CJS** output via tsdown with automatic type declarations
- **Prettier** for consistent code formatting
- **ESLint** with SonarJS, JSDoc enforcement, and import sorting
- **Vitest** for fast testing with v8 coverage (80% threshold)
- **Lefthook** for pre-commit hooks (lint + typecheck)
- **git-cliff** for automated changelog generation
- **GitHub Actions** for CI/CD with manual release workflow
- **VitePress** documentation site

## Quick Start

1. Click **[Use this template](https://github.com/pyyupsk/npm-ts-template/generate)** to create your repository

2. Clone and install:

   ```bash
   git clone https://github.com/YOUR_USERNAME/YOUR_REPO.git
   cd YOUR_REPO
   bun install
   ```

3. Configure repository settings:

   ```bash
   ./scripts/setup-repo.sh
   ```

4. Add required secrets in GitHub Settings → Secrets → Actions:
   - `NPM_TOKEN` - npm automation token
   - `GH_PAT` - Personal access token with `repo` scope

5. Update `package.json` with your package details and start coding in `src/index.ts`

## Scripts

| Script                  | Description                       |
| ----------------------- | --------------------------------- |
| `bun run build`         | Build ESM/CJS bundles to `dist/`  |
| `bun run dev`           | Build in watch mode               |
| `bun run test`          | Run tests                         |
| `bun run test:coverage` | Run tests with coverage report    |
| `bun run lint`          | Check code quality with ESLint    |
| `bun run lint:fix`      | Auto-fix linting issues           |
| `bun run format`        | Format code with Prettier         |
| `bun run typecheck`     | TypeScript type checking          |
| `bun run knip`          | Find unused code and dependencies |
| `bun run docs:dev`      | Start documentation dev server    |

## Project Structure

```
├── src/                 # Source code
│   └── index.ts         # Library entry point
├── tests/               # Test files
├── docs/                # VitePress documentation
├── scripts/             # Utility scripts
│   └── setup-repo.sh    # Repository configuration script
├── .github/
│   ├── workflows/       # CI/CD workflows
│   └── dependabot.yml   # Dependency updates
├── eslint.config.ts     # ESLint configuration
├── tsconfig.json        # TypeScript configuration
├── tsdown.config.ts     # Build configuration
└── cliff.toml           # Changelog configuration
```

## Releasing

Releases are triggered manually via GitHub Actions:

1. Go to **Actions** → **Release**
2. Click **Run workflow**
3. Select version type (`patch`, `minor`, `major`)

The workflow automatically:

- Bumps version in `package.json`
- Generates `CHANGELOG.md` with git-cliff
- Publishes to npm with provenance
- Creates GitHub release

## Documentation

📚 **[View Full Documentation](https://pyyupsk.github.io/npm-ts-template/)**

## Prerequisites

- [Bun](https://bun.sh/) (latest)
- [Node.js](https://nodejs.org/) >= 20
- [GitHub CLI](https://cli.github.com/) (for setup script)

## License

This project is licensed under the [MIT License](LICENSE) - free for personal and commercial use.

Copyright © 2026 [pyyupsk](https://github.com/pyyupsk)
