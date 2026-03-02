## Context

The `project-setup` change has initialized the Next.js project with design tokens and global styles. Now we need the component layer and app shell. This is a clickable prototype — no real backend, no real auth, no real data. All screens render inside a single phone frame on one Next.js page, controlled by a Zustand state machine.

## Goals / Non-Goals

**Goals:**
- A runnable app shell showing a phone frame with StatusBar and BottomNav
- Reusable Button/Card/Input components used by every screen
- Zustand store managing screen navigation, overlays, and selected pair
- Mock data representing markets, positions, and user account
- Screen router in page.tsx switching content based on store state

**Non-Goals:**
- No actual screens built (separate changes)
- No real API calls or authentication
- No animations/transitions between screens yet (handled in transitions-polish)

## Decisions

1. **Zustand over React context** — Simple, minimal boilerplate, no provider nesting. State machine pattern for screen/overlay routing.
2. **Single-page app with state router** — All screens render inside one PhoneFrame on `page.tsx`. No Next.js file-based routing since everything lives in one phone-sized viewport.
3. **PhoneFrame dimensions: 390×844px** — Matches iPhone 15. Max-width container centered on page. Browser page bg is `#1a1a1a` to frame it.
4. **Button variants via props** — Single Button component with `variant` prop (primary/secondary/ghost). All variants share press animation (`whileTap scale 0.97`).
5. **BottomNav conditional rendering** — Only visible on Home, Trade, Portfolio screens. Hidden during onboarding and modal screens.
6. **Overlay renders on top of screen content** — When `store.overlay` is set, the overlay component renders above the current screen within the PhoneFrame.

## Risks / Trade-offs

- [Zustand store becomes large] → Keep it flat. Only navigation state in v1, no complex nested objects.
- [Mock data diverges from real API shape] → Acceptable for prototype. Shape mock types to match expected API responses where possible.
