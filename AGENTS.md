# AGENTS.md

Instructions for AI coding agents working with this codebase.

## Project Overview

CLI tool for tracking [OpenCode](https://github.com/sst/opencode) AI coding assistant usage and costs.

### Tech Stack

- **Runtime**: Bun (uses `bun:sqlite` for data loading)
- **Language**: TypeScript
- **Build**: Bun bundler + tsc for .d.ts
- **Package Manager**: Bun

## Project Structure

```
src/
├── index.ts      # Entry point
├── cli.ts        # CLI argument parsing (node:util parseArgs)
├── loader.ts     # Data loading (bun:sqlite from opencode.db)
├── aggregator.ts # Date/provider aggregation
├── renderer.ts   # Terminal table output
├── pricing.ts    # Model pricing config
└── types.ts      # Type definitions
```

## Development Commands

```bash
bun run dev              # Run from source
bun run dev --days 7     # Run with arguments
bun run check            # Format + lint + typecheck
bun run build            # Build for npm (JS + .d.ts)
bun run compile          # Create standalone binary
bun run ck:warmup        # Index codebase for semantic search
```

## Code Guidelines

### TypeScript Best Practices

- Use `type` instead of `interface`
- Use `??` (nullish coalescing) instead of `||` for defaults
- Use `.js` extensions in imports (ESM requirement)
- Keep code simple - this is a small CLI tool

### File Naming

All filenames must use **kebab-case**: `pricing-config.ts`, `date-utils.ts`

### Code Style

- Functions over classes
- Explicit parameters
- No unnecessary abstractions

## Build & Publish

### Local Testing

```bash
bun run dev --days 3           # Test from source
bun run build && bun dist/index.js --days 3  # Test built output
```

### Publishing

Uses GitHub Actions with OIDC Trusted Publishing (no NPM_TOKEN needed):

```bash
git tag v0.1.0
git push --tags
```

## MCP Tools Available

| Tool         | Description                      |
| ------------ | -------------------------------- |
| **CK**       | Semantic code search             |
| **Context7** | Library documentation            |
| **Exa**      | Web search for APIs and examples |

## Quick Reference

| Command           | Description       |
| ----------------- | ----------------- |
| `bun run dev`     | Run from source   |
| `bun run build`   | Build JS + types  |
| `bun run compile` | Standalone binary |

## Important Reminders

1. **Keep it simple** - this is a small CLI tool
2. **Run build** before committing to verify it works
3. **All markdown in English**

<!-- opensrc:start -->

## Source Code Reference

Source code for dependencies is available in `opensrc/` for deeper understanding of implementation details.

See `opensrc/sources.json` for the list of available packages and their versions.

Use this source code when you need to understand how a package works internally, not just its types/interface.

### Fetching Additional Source Code

To fetch source code for a package or repository you need to understand, run:

```bash
npx opensrc <package>           # npm package (e.g., npx opensrc zod)
npx opensrc pypi:<package>      # Python package (e.g., npx opensrc pypi:requests)
npx opensrc crates:<package>    # Rust crate (e.g., npx opensrc crates:serde)
npx opensrc <owner>/<repo>      # GitHub repo (e.g., npx opensrc vercel/ai)
```

<!-- opensrc:end -->
