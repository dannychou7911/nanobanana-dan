# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Nano Banana is a **Gemini CLI extension** that provides image generation and manipulation via an MCP (Model Context Protocol) server. It uses Google's Gemini image models (`gemini-3.1-flash-image-preview` by default) through the `@google/genai` SDK.

The extension registers 7 MCP tools: `generate_image`, `edit_image`, `restore_image`, `generate_icon`, `generate_pattern`, `generate_story`, `generate_diagram`.

## Build & Development Commands

```bash
# Install all dependencies (root + mcp-server)
npm run install-deps

# Build the MCP server (TypeScript -> dist/)
npm run build

# Development mode with file watching
npm run dev

# Type checking without emitting
npm run typecheck

# Lint (with auto-fix)
npm run lint

# Format with Prettier
npm run format

# Full preflight check (clean, install, format, lint, build, typecheck)
npm run preflight
```

All npm scripts proxy into `mcp-server/` via `cd mcp-server && ...`.

## Architecture

```
nanobanana-dan/
├── gemini-extension.json     # Extension manifest (MCP server config, settings)
├── GEMINI.md                 # Instructions for the Gemini model (image generation guidelines)
├── commands/*.toml           # Gemini CLI slash commands (prompt templates with {{args}})
├── mcp-server/               # The actual MCP server (TypeScript, compiled to dist/)
│   └── src/
│       ├── index.ts          # NanoBananaServer class - MCP server setup, tool handlers, prompt builders
│       ├── imageGenerator.ts # ImageGenerator class - Gemini API calls, batch prompts, preview handling
│       ├── fileHandler.ts    # FileHandler class - file I/O, filename generation, input file search
│       └── types.ts          # Shared interfaces (ImageGenerationRequest, response types, prompt args)
└── package.json              # Root package.json (proxies scripts to mcp-server/)
```

**Data flow:** Gemini CLI -> MCP stdio transport -> `NanoBananaServer` (index.ts) routes tool calls -> `ImageGenerator` calls Gemini API -> `FileHandler` saves base64 images to `nanobanana-output/`.

## Key Conventions

- **License header required** on all `.ts`/`.js` files (enforced by eslint-plugin-license-header):
  ```
  /**
   * @license
   * Copyright 2025 Google LLC
   * SPDX-License-Identifier: Apache-2.0
   */
  ```
- **ESM only** - `"type": "module"` in both package.json files. Use ES6 imports, never `require()` (enforced by eslint).
- **Consistent type imports** - Use `import type { ... }` for type-only imports (enforced by `@typescript-eslint/consistent-type-imports`).
- **No `any`** - `@typescript-eslint/no-explicit-any` is set to error.
- **Strict TypeScript** - `strict: true` in tsconfig.
- Node.js import protocol required (e.g., `import * as fs from 'fs'`).

## API Key Resolution Order

`ImageGenerator.validateAuthentication()` checks env vars in this order:
1. `NANOBANANA_API_KEY` (primary)
2. `NANOBANANA_GEMINI_API_KEY`
3. `NANOBANANA_GOOGLE_API_KEY`
4. `GEMINI_API_KEY`
5. `GOOGLE_API_KEY`

Model selection: `NANOBANANA_MODEL` env var overrides the default `gemini-3.1-flash-image-preview`.

## Release Process

Tags matching `v*` trigger the GitHub Actions workflow (`.github/workflows/release.yaml`):
1. `npm ci` + build
2. Updates version in `gemini-extension.json` from tag
3. Creates a tar.gz archive (includes `mcp-server/node_modules` but excludes root `node_modules`)
4. Creates a GitHub Release with the archive
