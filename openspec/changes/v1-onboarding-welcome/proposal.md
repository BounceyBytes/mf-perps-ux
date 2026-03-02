## Why

Users need a first screen that introduces the MF Perps brand and provides frictionless sign-up via social login (Apple, Google) or email/phone. This is the top of the acquisition funnel — it must load fast, look premium, and route every auth action into the KYC onboarding flow.

## What Changes

- Create `WelcomeScreen` component (`src/components/screens/WelcomeScreen.tsx`) — full-height screen with MF Perps logo, tagline, three auth buttons, and sign-in link
- Logo block: bold "MF" in accent (#7B61FF) + "Perps" in white, text-3xl, centered in the top third with pt-24
- Tagline: "Trade BTC, ETH & more" (text-lg) and "Up to 100x leverage" (text-sm, text-secondary)
- Three auth buttons stacked vertically (gap-3, px-6): "Continue with Apple" (white bg, black text, Apple icon), "Continue with Google" (surface-light bg, white text, Google icon), "Use email or phone" (ghost variant, Mail icon)
- Bottom link: "Already have an account? Sign in" in text-muted with accent "Sign in"
- All auth buttons and sign-in link navigate to `kyc` screen via `store.navigate('kyc')`
- Framer Motion: container fades in on mount (opacity 0→1, 500ms), buttons stagger in from below (y:20→0, staggered 100ms delay), whileTap scale 0.97
- Wire `WelcomeScreen` into the screen router in `page.tsx` for `screen === 'welcome'`
- No BottomNav rendered on this screen

## Capabilities

### New Capabilities
- `welcome-screen`: WelcomeScreen component with brand logo, tagline, social/email auth buttons, sign-in link, and entrance animations

### Modified Capabilities

## Impact

- Adds 1 new file under `src/components/screens/`
- Updates `page.tsx` screen router to render WelcomeScreen for the 'welcome' screen state
- Depends on: PhoneFrame, StatusBar, Button, Zustand store (from core-components change)
