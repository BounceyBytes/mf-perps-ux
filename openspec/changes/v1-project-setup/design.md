## Context

This is a greenfield project. We're building a web-based clickable prototype that simulates a mobile trading app. The prototype runs in a browser with all screens rendered inside a phone frame. No backend — all state is local with mock data. The design is dark-mode-first, targeting iPhone 15 dimensions (390×844).

## Goals / Non-Goals

**Goals:**
- Runnable Next.js project with `npm run dev`
- Design tokens defined once, usable across all components via Tailwind classes and JS imports
- Inter font loaded and applied globally
- Dark-mode defaults matching the brand palette

**Non-Goals:**
- No screens, components, or layouts built yet (those are separate changes)
- No Zustand store or mock data (handled in `core-components`)
- No light mode support
- No production deployment configuration

## Decisions

1. **Next.js 14 App Router** — Modern React patterns, good DX, simple setup. No need for Pages Router complexity.
2. **Tailwind CSS 4 with theme extension** — Design tokens defined as Tailwind theme colors means all styling uses utility classes. No separate CSS-in-JS needed.
3. **Tokens as both JS constants and Tailwind config** — `src/lib/tokens.ts` exports raw values for programmatic use (e.g., Framer Motion color animations). Tailwind config imports them for utility class generation.
4. **Inter font via Google Fonts `@import`** — loaded in `globals.css` for simplicity. No need for `next/font` complexity in a prototype.
5. **`--src-dir` flag** — keeps source code under `src/` for cleaner project root.

## Risks / Trade-offs

- [Tailwind v4 breaking changes] → Pin version in package.json. Only using standard utility classes.
- [Google Fonts import blocks rendering] → Acceptable for a prototype. Production app would use `next/font`.
