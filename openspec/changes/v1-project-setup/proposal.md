## Why

There is no project yet. We need a Next.js 14 prototype project initialized with the correct tech stack, design tokens, Tailwind configuration, and global styles before any screens can be built. This is the foundation everything else depends on.

## What Changes

- Initialize a new Next.js 14 (App Router) project with TypeScript, Tailwind CSS, and `--src-dir`
- Install core dependencies: `framer-motion`, `lucide-react`, `zustand`
- Define design tokens as exported JS constants in `src/lib/tokens.ts` (colors, typography, spacing, radius)
- Extend Tailwind theme with custom dark-mode colors: background, surface, surface-light, border, text-primary, text-secondary, text-muted, accent, green, red, yellow, orange
- Configure `globals.css` with Tailwind imports, Inter font from Google Fonts, dark background (`#0A0A0F`), and hidden scrollbar styles
- Set up `src/app/layout.tsx` with Inter font and dark background as the global layout

## Capabilities

### New Capabilities
- `design-tokens`: Design token constants and Tailwind theme extension for the dark-mode color palette, typography, spacing, and radius values
- `global-styles`: Global CSS setup including Tailwind imports, Inter font, dark background, and scrollbar hiding

### Modified Capabilities

## Impact

- Creates the entire project directory (`mf-perps-prototype/`)
- Establishes the tech stack and build tooling (Next.js 14, TypeScript, Tailwind CSS 4)
- All subsequent changes depend on this project existing with the correct configuration
