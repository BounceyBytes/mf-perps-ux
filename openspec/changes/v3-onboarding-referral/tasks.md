## 1. ReferralScreen Component

- [ ] 1.1 Create `src/components/screens/ReferralScreen.tsx` with a full-height flex column layout (min-h-full, flex, flex-col, px-6)
- [ ] 1.2 Add back arrow: ChevronLeft icon (Lucide) top-left, tapping calls `store.navigate('kyc')`
- [ ] 1.3 Add heading: "Got an invite code?" in text-2xl font-bold with pt-16
- [ ] 1.4 Add Input component (mt-8) with text-center, text-xl, tracking-widest, placeholder "Enter code", autoCapitalize, maxLength 12
- [ ] 1.5 Add incentive text (mt-4): "You'll both earn trading rewards" in text-sm text-secondary, text-center
- [ ] 1.6 Add CTA area (mt-auto, pb-8): primary Button "Continue" full width
- [ ] 1.7 Add "Skip" link (mt-3) below Continue: text-secondary, underline, text-center, navigates to 'youre-in'

## 2. Validation & Navigation Logic

- [ ] 2.1 Add local state for input value (`useState<string>('')`) and validated flag (`useState<boolean>(false)`)
- [ ] 2.2 On Continue tap with non-empty input: set validated to true, show green checkmark, then `setTimeout(() => store.navigate('youre-in'), 500)`
- [ ] 2.3 On Continue tap with empty input: navigate directly to 'youre-in'
- [ ] 2.4 On Skip tap: navigate directly to 'youre-in'

## 3. Animations

- [ ] 3.1 Wrap the ReferralScreen root content in a `motion.div` with initial={{ opacity: 0, x: 30 }} animate={{ opacity: 1, x: 0 }} for slide-in from right
- [ ] 3.2 Add green Check icon (Lucide) next to the input, wrapped in `motion.div` with initial={{ scale: 0 }} animate={{ scale: 1 }}, rendered conditionally when validated is true

## 4. App Shell Wiring

- [ ] 4.1 Add ReferralScreen to the screen router in `page.tsx` so it renders when `store.screen === 'referral'`
- [ ] 4.2 Confirm BottomNav is not rendered when screen is 'referral' (should already be handled by core-components conditional logic)

## 5. Verification

- [ ] 5.1 Run the app and confirm the Referral screen renders inside PhoneFrame with heading, input, incentive text, Continue button, and Skip link
- [ ] 5.2 Enter a code and tap Continue — confirm green checkmark animates in, then navigates to 'youre-in' after 500ms
- [ ] 5.3 Tap Continue with empty input — confirm direct navigation to 'youre-in'
- [ ] 5.4 Tap Skip — confirm direct navigation to 'youre-in'
- [ ] 5.5 Tap back arrow — confirm navigation to 'kyc'
- [ ] 5.6 Confirm slide-in animation plays on mount
