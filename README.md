# npm-template

[![CI](https://github.com/pyyupsk/npm-template/actions/workflows/ci.yml/badge.svg)](https://github.com/pyyupsk/npm-template/actions/workflows/ci.yml)
[![npm version](https://img.shields.io/npm/v/npm-template.svg)](https://www.npmjs.com/package/npm-template)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![codecov](https://codecov.io/gh/pyyupsk/npm-template/branch/main/graph/badge.svg)](https://codecov.io/gh/pyyupsk/npm-template)

A TypeScript library template with modern tooling.

## Features

- TypeScript 5.x with strict mode
- Dual ESM/CJS output via tsdown
- Biome for linting and formatting
- Vitest for testing with coverage
- Lefthook for git hooks
- Changesets for versioning
- GitHub Actions for CI/CD

## Installation

```bash
bun add npm-template
# or
npm install npm-template
# or
pnpm add npm-template
```

## Usage

```typescript
import { greet } from "npm-template";

console.log(greet("World")); // "Hello, World!"
```

## Development

### Prerequisites

- [Bun](https://bun.sh/) 1.x or later
- [Node.js](https://nodejs.org/) 20+ (for compatibility)

### Setup

```bash
# Clone the repository
git clone https://github.com/pyyupsk/npm-template.git
cd npm-template

# Install dependencies
bun install
```

### Scripts

| Script                  | Description                       |
| ----------------------- | --------------------------------- |
| `bun run build`         | Build ESM/CJS bundles to `dist/`  |
| `bun run dev`           | Build in watch mode               |
| `bun run test`          | Run tests once                    |
| `bun run test:watch`    | Run tests in watch mode           |
| `bun run test:coverage` | Run tests with coverage report    |
| `bun run lint`          | Check code with Biome             |
| `bun run lint:fix`      | Fix auto-fixable issues           |
| `bun run format`        | Format code with Biome            |
| `bun run typecheck`     | Check TypeScript types            |
| `bun run knip`          | Check for unused code             |
| `bun run changeset`     | Create a changeset for versioning |
| `bun run release`       | Publish to npm (CI only)          |

## API

### `greet(name: string): string`

Greets a person by name.

**Parameters:**

- `name` - The name of the person to greet

**Returns:** A greeting message

**Example:**

```typescript
greet("Alice"); // "Hello, Alice!"
```

## Publishing

1. Create a changeset: `bun run changeset`
2. Push to main branch
3. Merge the "Version Packages" PR created by the release workflow
4. Package is automatically published to npm

**Note:** Requires `NPM_TOKEN` secret configured in GitHub repository settings.

## License

This project is licensed under the [MIT License](LICENSE). See the LICENSE file for details.
