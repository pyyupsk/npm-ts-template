# TypeScript Configuration

The template uses TypeScript 5.x with strict mode enabled.

## Configuration File

The `tsconfig.json` is configured for library development:

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "ESNext",
    "moduleResolution": "bundler",
    "lib": ["ES2022"],
    "strict": true,
    "noEmit": true,
    "skipLibCheck": true,
    "esModuleInterop": true,
    "resolveJsonModule": true,
    "isolatedModules": true,
    "verbatimModuleSyntax": true,
    "declaration": true,
    "declarationMap": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noFallthroughCasesInSwitch": true,
    "noUncheckedIndexedAccess": true
  },
  "include": ["src"],
  "exclude": ["node_modules", "dist"]
}
```

## Key Settings

### Strict Mode

All strict type-checking options are enabled:

- `strict` - Enable all strict type-checking options
- `noUnusedLocals` - Report errors on unused local variables
- `noUnusedParameters` - Report errors on unused parameters
- `noFallthroughCasesInSwitch` - Report errors for fallthrough cases in switch
- `noUncheckedIndexedAccess` - Add undefined to indexed access results

### Module System

- `module: "ESNext"` - Modern ES modules
- `moduleResolution: "bundler"` - Works with modern bundlers
- `verbatimModuleSyntax` - Enforce explicit type imports

## Customization

### Adding Path Aliases

```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"]
    }
  }
}
```

::: warning
If you add path aliases, update `tsdown.config.ts` to handle them during build.
:::

### Relaxing Strict Mode (Not Recommended)

If migrating existing code:

```json
{
  "compilerOptions": {
    "strict": false,
    "noImplicitAny": false
  }
}
```

## Type Checking

Run type checking without emitting files:

```bash
bun run typecheck
```

This is also run automatically on pre-commit via Lefthook.
