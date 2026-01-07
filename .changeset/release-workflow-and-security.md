---
"@pyyupsk/npm-ts-template": patch
---

### Changed

- Refactored release workflow to use official `changesets/action`
- Extended `@tsconfig/strictest` for multi-target flexibility

### Fixed

- CI workflow npm authentication and tag publishing
- Release workflow issues

### Security

- Fixed esbuild vulnerability (GHSA-67mh-4wv8-2f99) via package override
