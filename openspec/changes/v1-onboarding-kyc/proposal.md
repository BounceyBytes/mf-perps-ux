## Why

After welcome/sign-up, users need a KYC identity verification screen that communicates trust and regulatory compliance. This screen bridges the gap between initial sign-up and the "You're In" confirmation step. It must feel fast, secure, and straightforward — showing exactly what's needed (ID scan + selfie) and setting the expectation that verification takes ~30 seconds.

## What Changes

- Create `KycScreen` component (`src/components/screens/KycScreen.tsx`) — full-height screen with back navigation, heading, two step cards, trust badge, and CTA button
- Back arrow: ChevronLeft icon (Lucide) top-left, navigates to 'welcome' via `store.navigate('welcome')`
- Heading: "Verify your identity" — text-2xl font-bold, pt-16
- Subtext: "Usually takes ~30 seconds. Verification helps keep the venue trusted." — text-sm text-secondary
- Two step cards (mt-8, gap-3): horizontal Card layout with icon, title, description, and chevron-right
  1. FileText icon in accent + "Scan your ID" + "Government-issued ID" (text-xs text-secondary) + ChevronRight
  2. Camera icon in accent + "Take a selfie" + "Quick face match" (text-xs text-secondary) + ChevronRight
- Trust badge (mt-auto, pb-8): Lock icon + "Bank-grade encryption. Your data is never shared." — text-xs text-muted
- CTA: Primary Button "Start verification", full width, near bottom
- On tap: button shows Loader2 spinning icon for 1.5s, then navigates to 'youre-in'
- Framer Motion: content slides in from right (x: 30→0, opacity 0→1)
- Wire `KycScreen` into the screen router in `page.tsx` for `screen === 'kyc'`
- No BottomNav rendered on this screen

## Capabilities

### New Capabilities
- `kyc-screen`: KycScreen component with back navigation, heading/subtext, two verification step cards, trust badge, loading CTA button, and slide-in animation

### Modified Capabilities

## Impact

- Adds 1 new file under `src/components/screens/`
- Updates `page.tsx` screen router to render KycScreen for the 'kyc' screen state
- Depends on: PhoneFrame, Button, Card, Zustand store (from core-components change)
- Depends on: Lucide icons (ChevronLeft, FileText, Camera, Lock, ChevronRight, Loader2)
