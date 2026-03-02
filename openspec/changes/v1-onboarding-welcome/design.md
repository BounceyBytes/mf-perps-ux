## Context

The core-components change established the app shell (PhoneFrame, StatusBar, BottomNav, Zustand store, Button). The Welcome screen is the first screen in the user journey — it renders inside the PhoneFrame at `store.screen === 'welcome'` (the default state). It introduces the brand and funnels users into onboarding via social login or email/phone. This is a clickable prototype; auth buttons don't perform real authentication — they all call `store.navigate('kyc')`.

## Goals / Non-Goals

**Goals:**
- A polished welcome screen that renders inside PhoneFrame with logo, tagline, and auth buttons
- All auth actions route to the KYC screen (no real auth in prototype)
- Smooth entrance animations using Framer Motion (fade-in + staggered buttons)
- No BottomNav visible on this screen

**Non-Goals:**
- No real Privy SDK integration (prototype only — buttons just navigate)
- No dark/light theme toggle (dark mode only)
- No input validation or error handling on auth flows
- No loading states or spinners

## Decisions

1. **Single WelcomeScreen component** — All layout, buttons, and animations in one file. No sub-components needed for a single static screen.
2. **Reuse Button component with variant overrides** — Apple button uses custom white bg/black text via className override. Google button uses secondary variant. Email button uses ghost variant. All share whileTap animation from Button.
3. **Apple/Google icons as inline SVGs** — Small, one-off brand icons rendered inline rather than adding a dependency. Mail icon from Lucide.
4. **All auth paths lead to 'kyc'** — In the prototype, there's no branching auth logic. Every button calls `navigate('kyc')` to keep the flow linear.
5. **Staggered button animation via Framer Motion variants** — Parent container uses `staggerChildren: 0.1` and children animate `y: 20 → 0` with `opacity: 0 → 1`. Cleaner than manual delays.

## Risks / Trade-offs

- [Custom className overrides on Button for Apple style] → Acceptable for prototype. A proper `variant="apple"` could be added later if more screens need it.
- [Inline SVGs for Apple/Google logos] → Keeps the component self-contained. If icons are needed elsewhere, extract to a shared icons file.
- [No real auth means the prototype can't demonstrate Privy flows] → Out of scope for UX prototype. Auth integration happens in the React Native build.
