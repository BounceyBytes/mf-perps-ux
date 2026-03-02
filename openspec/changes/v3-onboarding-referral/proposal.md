## Why

After KYC verification, users land on the referral code screen — a lightweight, optional step that drives viral growth by letting users enter an invite code for mutual trading rewards. The screen must feel low-friction: a single input with clear incentive text, an obvious Skip path, and a satisfying validation animation when a code is entered.

## What Changes

- Create `ReferralScreen` component (`src/components/screens/ReferralScreen.tsx`) — full-height screen with back navigation, heading, code input, incentive text, and CTA area
- Back arrow: ChevronLeft icon (Lucide) top-left, navigates to 'kyc' via `store.navigate('kyc')`
- Heading: "Got an invite code?" — text-2xl font-bold, pt-16
- Single text input (mt-8): centered text, text-xl, tracking-widest for code-entry feel, placeholder "Enter code", auto-capitalize, maxLength 12. Uses the Input base component with text-center className override.
- Incentive text (mt-4): "You'll both earn trading rewards" — text-sm text-secondary, centered
- CTA area (mt-auto, pb-8):
  - Primary Button "Continue" — full width
  - Below (mt-3): "Skip" as text-secondary underline link, centered. Tapping Skip navigates to 'youre-in'.
- If input has text + tap Continue: show a green checkmark animation (scale 0→1) next to the input, then navigate to 'youre-in' after 500ms
- If input is empty + tap Continue or tap Skip: navigate directly to 'youre-in'
- Framer Motion: content slides in from right on mount (x: 30→0, opacity 0→1)
- Wire `ReferralScreen` into the screen router in `page.tsx` for `screen === 'referral'`
- No BottomNav rendered on this screen

## Capabilities

### New Capabilities
- `referral-screen`: ReferralScreen component with back navigation, heading, code input with centered tracking-widest styling, incentive text, Continue button with green checkmark validation animation, Skip link, and slide-in entrance animation

### Modified Capabilities

## Impact

- Adds 1 new file under `src/components/screens/`
- Updates `page.tsx` screen router to render ReferralScreen for the 'referral' screen state
- Depends on: PhoneFrame, Button, Input, Zustand store (from core-components change)
- Depends on: Lucide icons (ChevronLeft, Check)
- Depends on: Framer Motion for entrance and checkmark animations
