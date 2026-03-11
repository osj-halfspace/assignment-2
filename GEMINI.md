---
alwaysApply: true
description: Main development rules and workflow - essential guidelines for all development work
---

# Main Development Rules

- **ALWAYS** check if the dev server is already running before trying to start a new one
- **NEVER** test changes in the browser on your own, write e2e tests if necessary
- **ALWAYS** run `bun check`, `bun type-check`, and `bun test` after making any changes

## Technology Stack
- **React**: Functional components with hooks
- **TanStack Router**: File-based routing
- **TanStack Query**: All data fetching and server state
- **Zustand**: Global client state when needed
- **shadcn/ui**: Default UI components (in `src/components/ui/`)
- **Tailwind CSS**: Only when customizing shadcn components
- **Playwright**: End-to-end testing
- **bun**: Package manager, Unit tests

## Component Priority
1. **First**: Use existing shadcn/ui components. Use configured shadcn MCP server
2. **Second**: Extend shadcn/ui components with Tailwind
3. **Third**: Download new shadcn/ui components using the MCP server
4. **Last Resort**: Build custom components, preferably composing shadcn components

## State Management Hierarchy
1. **URL State**: TanStack Router search params
2. **Server State**: TanStack Query
3. **Local State**: useState
4. **Global Client State**: Zustand

## Type Safety Requirements
- **CRITICAL**: Type safety is paramount - leverage it everywhere possible
- Use TanStack Router's type-safe routing, params, and search params
- Use TanStack Query's type-safe data fetching and mutations
- Use Zustand's TypeScript integration for store typing
- Prefer `type` over `interface` (use interface only when absolutely necessary)
- Before creating a new type always check if a given type does not already exist

## Project Structure
```
/
├── .cursor/              # Cursor IDE config
│   └── rules/            # AI rules
├── public/               # Static assets
├── src/
│   ├── components/       # Custom components
│   │   └── ui/           # shadcn/ui components
│   ├── hooks/            # Custom React hooks
│   ├── integrations/     # Third-party library configs
│   ├── lib/              # Utilities
│   ├── routes/           # TanStack Router file-based routes
│   ├── ts/               # TypeScript types
│   ├── main.tsx          # App entry point
│   ├── styles.css        # Global styles
│   └── routeTree.gen.ts  # Auto-generated (do not edit)
├── tests/
│   ├── e2e/              # Playwright tests
│   └── unit/             # Bun unit tests
├── biome.json            # Linter/formatter config
├── components.json       # shadcn/ui config
├── index.html            # HTML entry point
├── package.json
├── playwright.config.ts
├── tsconfig.json
└── vite.config.ts
```

# Anonymous Feedback Platform

A simple internal platform for employees to share anonymous feedback and ideas.

## Project Overview

- **Backend:** Python with **FastAPI**. Uses `uv` for package management and development.
- **Frontend:** **React** with **TypeScript** and **Vite**.
- **Storage:** **In-memory** (no persistent database).
- **Architecture:** RESTful API with CORS enabled for development.

## Building and Running

### Development Mode

The easiest way to start the entire stack is using the provided `start.sh` script:

```bash
./start.sh
```

This script will:
1. Sync backend dependencies using `uv`.
2. Start the FastAPI server on `http://localhost:8000`.
3. Install frontend dependencies using `npm`.
4. Start the Vite development server on `http://localhost:5173`.

### Manual Control

#### Backend
```bash
cd backend
uv sync
uv run fastapi dev main.py --port 8000
```

#### Frontend
```bash
cd frontend
npm install
npm run dev -- --port 5173
```

## Development Conventions

- **API Design:** Follows RESTful principles.
- **Backend Style:** Uses `Annotated` for dependency injection and parameter validation.
- **Frontend Style:** Modern React hooks and TypeScript for type safety.
- **Storage:** Temporary in-memory storage; data is lost on server restart.
