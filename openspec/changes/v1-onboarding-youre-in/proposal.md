## Why

After completing KYC, users need a clear confirmation that onboarding is complete and a path forward into the app. The "You're all set" screen closes the onboarding funnel with a celebratory moment and two clear CTAs — deposit to start trading, or explore markets first.

## What Changes

- Create `YoureInScreen` component (`src/components/screens/YoureInScreen.tsx`) — centered confirmation screen with check icon, heading, and two action buttons
- Large CheckCircle2 icon (from Lucide) in accent color (#7B61FF), size 64px, centered horizontally
- "You're all set" heading — text-2xl font-bold, mt-4, centered
- Two full-width action buttons (mt-8, gap-3, px-6): "Deposit & Trade" (primary/accent bg → navigates to 'deposit') and "Explore Markets" (secondary/surface-light bg → navigates to 'home')
- Framer Motion: check icon scales from 0→1 with spring animation (type: "spring", stiffness: 200) on mount. Buttons stagger in from below after 300ms delay.
- Wire `YoureInScreen` into the screen router in `page.tsx` for `screen === 'youre-in'`
- No BottomNav rendered on this screen
- Content centered on both axes with px-6

## Capabilities

### New Capabilities
- `youre-in-screen`: YoureInScreen component with check icon, confirmation heading, two action buttons, and entrance animations

### Modified Capabilities

## Impact

- Adds 1 new file under `src/components/screens/`
- Updates `page.tsx` screen router to render YoureInScreen for the 'youre-in' screen state
- Depends on: PhoneFrame, StatusBar, Button, Zustand store (from core-components change)
