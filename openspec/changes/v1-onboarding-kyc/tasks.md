## 1. KycScreen Component

- [ ] 1.1 Create `src/components/screens/KycScreen.tsx` with a full-height flex column layout (min-h-full, flex, flex-col, px-6)
- [ ] 1.2 Add back arrow: ChevronLeft icon (Lucide) at the top-left, tappable, calls `store.navigate('welcome')`
- [ ] 1.3 Add heading: "Verify your identity" — text-2xl font-bold, pt-16
- [ ] 1.4 Add subtext: "Usually takes ~30 seconds. Verification helps keep the venue trusted." — text-sm text-secondary, below heading
- [ ] 1.5 Add two step cards in a vertical stack (mt-8, gap-3): each card with horizontal layout — accent icon (FileText / Camera), title, text-xs text-secondary description, ChevronRight icon
- [ ] 1.6 Add trust badge section (mt-auto, pb-8): Lock icon + "Bank-grade encryption. Your data is never shared." in text-xs text-muted, centered
- [ ] 1.7 Add primary Button "Start verification" — full width, near bottom of screen

## 2. Loading & Navigation

- [ ] 2.1 Add `isLoading` local state (useState) to KycScreen, default false
- [ ] 2.2 On CTA tap: set `isLoading` to true, show Loader2 spinning icon (animate-spin) in the button, disable the button
- [ ] 2.3 After 1.5s timeout: call `store.navigate('referral')` — clean up timeout on unmount via useEffect return

## 3. Animations

- [ ] 3.1 Wrap KycScreen content in a `motion.div` with initial={{ x: 30, opacity: 0 }} animate={{ x: 0, opacity: 1 }} transition (ease, ~0.4s)

## 4. App Shell Wiring

- [ ] 4.1 Add KycScreen to the screen router in `page.tsx` so it renders when `store.screen === 'kyc'`
- [ ] 4.2 Confirm BottomNav is not rendered when screen is 'kyc' (should already be handled by core-components conditional logic, update if needed)

## 5. Verification

- [ ] 5.1 Run the app and confirm the KYC screen renders inside PhoneFrame with back arrow, heading, step cards, trust badge, and CTA
- [ ] 5.2 Tap back arrow and confirm navigation to 'welcome' screen
- [ ] 5.3 Tap "Start verification" and confirm spinner shows for ~1.5s then navigates to 'referral'
- [ ] 5.4 Confirm slide-in animation plays on mount
