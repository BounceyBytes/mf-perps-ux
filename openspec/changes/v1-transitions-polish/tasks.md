## 1. Toast Notification System

- [ ] 1.1 Add `toast: string | null` field and `showToast(message: string)` action to the Zustand store in `src/lib/store.ts` — sets toast to message and schedules setTimeout to clear it after 2500ms
- [ ] 1.2 Create `src/components/Toast.tsx` — fixed pill at top of phone frame (below status bar), z-50, rounded-full, surface-light bg, px-4 py-2, text-sm, green left accent border, AnimatePresence with slide from y:-20, opacity fade

## 2. Screen Transitions

- [ ] 2.1 Define transition variant maps in `page.tsx` — onboarding screens (welcome, kyc, referral, youre-in) get slide-right (x:30→0, exit x:-30, 300ms), tab screens (home, trade, portfolio) get crossfade (opacity, 200ms), modal screens (deposit, deposit-amount, withdraw) get slide-up (y:50→0, 300ms)
- [ ] 2.2 Wrap screen router content in AnimatePresence mode="wait" with motion.div keyed by store.screen, applying the correct variant based on screen category
- [ ] 2.3 Render Toast component inside PhoneFrame (after screen content, before overlay layer) so toasts appear on all screens

## 3. Animated Number Component

- [ ] 3.1 Create `src/components/AnimatedNumber.tsx` — accepts value, prefix, suffix, decimals props; uses Framer Motion useSpring to animate from 0 to value on mount (~500ms); renders with tabular-nums class

## 4. Button Micro-Interactions

- [ ] 4.1 Update `src/components/Button.tsx` to render as motion.button with whileTap={{ scale: 0.97 }}
- [ ] 4.2 Add whileHover brightness increase to the primary variant in Button.tsx

## 5. Loading States

- [ ] 5.1 Update KYC screen CTA ("Start verification") in `src/components/screens/KYCScreen.tsx` to show Loader2 animate-spin icon and disable the button during simulated loading
- [ ] 5.2 Update deposit amount CTA ("Fund $X.XX") in `src/components/screens/DepositAmountScreen.tsx` to show Loader2 animate-spin icon and disable during loading, then navigate and showToast on completion

## 6. Scroll & Demo Flow

- [ ] 6.1 Update `src/components/PhoneFrame.tsx` to add overscroll-behavior: contain and -webkit-overflow-scrolling: touch to the scrollable container
- [ ] 6.2 Verify store default screen is 'welcome' and the full onboarding→home→trade→deposit demo flow runs end-to-end with all transitions, toasts, and animations working
