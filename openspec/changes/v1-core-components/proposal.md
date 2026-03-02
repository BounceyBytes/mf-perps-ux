## Why

The project has no reusable components, app shell, state management, or mock data. Every screen in the prototype depends on a shared set of base components (Button, Card, Input), a phone frame wrapper, navigation infrastructure (Zustand store, BottomNav), and mock data. These must exist before any screen can be built.

## What Changes

- Create `PhoneFrame` component — 390×844 centered phone frame with rounded corners, border, overflow scroll
- Create `StatusBar` component — fake iOS status bar (time, signal, wifi, battery)
- Create `BottomNav` component — three-tab navigation (Home, Trade, Portfolio) with active state and navigate on tap
- Create `Button` component — three variants (primary/accent, secondary/surface-light, ghost/transparent) with press animation
- Create `Card` component — surface background card with padding, border, and rounded corners
- Create `Input` component — dark-themed text input with accent focus ring
- Create Zustand store (`src/lib/store.ts`) — screen state, overlay state, selectedPair, navigation functions
- Create mock data (`src/lib/mock-data.ts`) — markets, open positions, user data
- Wire app shell in `src/app/page.tsx` — PhoneFrame containing StatusBar, screen router, overlay layer, conditional BottomNav

## Capabilities

### New Capabilities
- `phone-frame`: PhoneFrame wrapper component that renders all screens inside an iPhone-sized frame with StatusBar
- `bottom-nav`: BottomNav three-tab navigation component with active state indicators
- `base-components`: Reusable Button (primary/secondary/ghost), Card, and Input components
- `app-state`: Zustand store for screen navigation, overlay management, selected pair, and mock data
- `app-shell`: Page.tsx wiring that renders the phone frame, routes screens based on store state, and renders overlays

### Modified Capabilities

## Impact

- Creates 8 new files under `src/components/`, `src/lib/`, and `src/app/`
- Establishes the navigation system all screens use
- Provides mock data all screens reference
- Every subsequent change depends on these components
