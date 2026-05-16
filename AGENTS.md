# AGENTS.md

Guidelines for AI agents (Ona, Copilot, Cursor, etc.) working in this repository.

## Repository Overview

- **Name:** Kaylasyafiqah-
- **Purpose:** E-commerce product catalog — browse and display barang (goods/items) for sale.
- **Stack:** Next.js 14 (App Router), React, TypeScript, CSS Modules
- **Backend:** Next.js API routes (no separate server)
- **Runtime:** Node.js 20+

## Repository Structure

```
.
├── .devcontainer/
│   └── devcontainer.json       # Dev container config
├── public/                     # Static assets (images, icons, fonts)
├── src/
│   ├── app/                    # Next.js App Router pages and layouts
│   │   ├── layout.tsx          # Root layout
│   │   ├── page.tsx            # Home / product listing page
│   │   ├── products/
│   │   │   └── [id]/
│   │   │       └── page.tsx    # Product detail page
│   │   └── api/                # API route handlers
│   │       └── products/
│   │           └── route.ts    # GET /api/products
│   ├── components/             # Shared UI components
│   │   └── *.module.css        # CSS Module per component
│   ├── lib/                    # Utilities, data fetching helpers
│   └── types/                  # Shared TypeScript types
├── .gitignore
├── next.config.ts
├── package.json
├── tsconfig.json
├── README.md
└── AGENTS.md                   # This file
```

> The structure above is the target layout. Create directories as features are added — do not scaffold empty folders.

## Development Environment

- Dev container: `mcr.microsoft.com/devcontainers/javascript-node:22`
- Node.js 20+ required
- Package manager: `npm`

## Build & Run Commands

```bash
# Install dependencies
npm install

# Start development server (http://localhost:3000)
npm run dev

# Production build
npm run build

# Start production server
npm start

# Type-check without emitting
npx tsc --noEmit
```

## Testing

No test framework is configured yet. When one is added:
- Document the test command here.
- Run tests before marking any task complete.
- Do not remove this section — update it instead.

## Code Style

No formatter or linter is configured yet. Until one is added, follow these rules manually:

### TypeScript
- Strict mode is on (`"strict": true` in `tsconfig.json`).
- Prefer `interface` over `type` for object shapes.
- No `any` — use `unknown` and narrow, or define a proper type.
- Export types from `src/types/` when shared across more than one file.

### React / Next.js
- Use the App Router (`src/app/`). Do not use the Pages Router.
- Server Components by default. Add `"use client"` only when the component needs browser APIs or React state/effects.
- One component per file. File name matches the component name in PascalCase (e.g. `ProductCard.tsx`).
- Co-locate the CSS Module with its component: `ProductCard.tsx` + `ProductCard.module.css`.

### CSS Modules
- Class names in camelCase (e.g. `.productCard`, `.priceTag`).
- No global styles except in `src/app/globals.css`.
- Do not use inline styles unless the value is dynamic and cannot be expressed in CSS.

### General
- No unused imports or variables — TypeScript strict mode will catch most of these.
- Prefer `const` over `let`. Never use `var`.
- Use named exports. Avoid default exports except for Next.js page/layout files (required by the framework).

## Git

- Default branch: `main`
- Commit message format: `<type>: <short description>`
  - Types: `feat`, `fix`, `chore`, `refactor`, `docs`, `style`
  - Example: `feat: add product detail page`
- Do not commit `node_modules/`, `.next/`, `.env*`, or build artifacts.
- Never push directly to `main` without explicit user instruction.
- Create a feature branch for each task: `git checkout -b feat/your-feature-name`

## Agent Conventions

### General
- Read this file at the start of every session.
- Do not invent data models or API shapes — ask the user if the schema is unclear.
- Always read a file before editing it.
- Clean up temporary files before completing a task.

### Adding a New Page
1. Create `src/app/<route>/page.tsx` as a Server Component.
2. Add a corresponding CSS Module at `src/app/<route>/page.module.css` if styling is needed.
3. Update the directory map in this file if the route is permanent.

### Adding a New Component
1. Create `src/components/<ComponentName>.tsx`.
2. Create `src/components/<ComponentName>.module.css` alongside it.
3. Export the component as a named export.

### Adding an API Route
1. Create `src/app/api/<resource>/route.ts`.
2. Export named HTTP method handlers (`GET`, `POST`, etc.).
3. Return `NextResponse.json(...)` with appropriate status codes.
4. Define request/response types in `src/types/`.

### Security
- Never commit `.env` or `.env.local` files.
- `.env.example` (with placeholder values only) is safe to commit.
- Validate and sanitise all inputs in API routes before use.
