## Why

The V1 prototype has all screens and flows built, but transitions between screens are instant cuts, numbers appear statically, buttons lack tactile feedback, and there are no success/error notifications. This makes the prototype feel flat and unfinished. A final polish pass adding screen transitions, micro-interactions, toast notifications, number animations, and loading states transforms the prototype from a wireframe walkthrough into something that feels like a real trading app.

## What Changes

- Update `src/app/page.tsx` to wrap the screen router in Framer Motion AnimatePresence with transition variants per screen category:
  - Onboarding screens (welcome, kyc, referral, youre-in): slide from right (x:30→0, exit x:-30, 300ms)
  - Tab screens (home, trade, portfolio): crossfade (opacity 0→1, 200ms, no slide)
  - Modal screens (deposit, deposit-amount, withdraw): slide up from bottom (y:50→0, 300ms)
- Create `src/components/Toast.tsx` — pill-shaped toast notification that slides in from top, auto-dismisses after 2.5s, green left accent for success
- Add toast state to Zustand store (`src/lib/store.ts`): `toast` field, `showToast(message)` action that sets toast and auto-clears after 2.5s
- Create `src/components/AnimatedNumber.tsx` — component that animates dollar amounts and percentages from 0 to target value on mount (500ms) using Framer Motion useSpring, renders with tabular-nums font-variant
- Update all Button usages to include Framer Motion `whileTap={{ scale: 0.97 }}` and primary variant hover brightness
- Update KYC screen "Start verification" button and deposit amount CTA to show Loader2 spinning icon during loading states
- Update `src/components/PhoneFrame.tsx` to add `overscroll-behavior: contain` and `-webkit-overflow-scrolling: touch`
- Ensure app starts at 'welcome' screen and onboarding flows seamlessly through the full demo path

## Capabilities

### New Capabilities
- `screen-transitions`: AnimatePresence wrapper in page.tsx with categorized transition variants for onboarding (slide-right), tabs (crossfade), and modals (slide-up)
- `toast-notification`: Toast component and Zustand toast state for auto-dismissing success notifications
- `number-animations`: AnimatedNumber component that counts from 0 to target on mount using Framer Motion spring
- `button-micro-interactions`: whileTap scale and hover brightness micro-interactions on all buttons
- `loading-states`: Loader2 spinner on KYC and deposit CTAs during async-simulated actions
- `scroll-behavior`: overscroll-contain and touch scrolling on PhoneFrame

### Modified Capabilities

## Impact

- Modifies `src/app/page.tsx` (screen router wrapped in AnimatePresence)
- Modifies `src/lib/store.ts` (toast state and showToast action)
- Modifies `src/components/PhoneFrame.tsx` (scroll behavior styles)
- Modifies `src/components/Button.tsx` (whileTap and hover micro-interactions)
- Modifies `src/components/screens/KYCScreen.tsx` (loading spinner on CTA)
- Modifies `src/components/screens/DepositAmountScreen.tsx` (loading spinner on CTA)
- Adds 2 new files: `src/components/Toast.tsx`, `src/components/AnimatedNumber.tsx`
- Depends on: all previously built screens and components from core-components, onboarding, home-screen, trade-screen, portfolio-screen, deposit-flow, withdraw-screen changes
