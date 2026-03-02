## 1. YoureInScreen Component

- [ ] 1.1 Create `src/components/screens/YoureInScreen.tsx` with a centered flex layout (min-h-full, flex, flex-col, items-center, justify-center, px-6)
- [ ] 1.2 Add CheckCircle2 icon from Lucide at size 64px in accent color (#7B61FF), centered
- [ ] 1.3 Add "You're all set" heading — text-2xl font-bold mt-4, centered
- [ ] 1.4 Add two full-width action buttons (mt-8, gap-3, w-full): "Fund Account & Trade" (primary/accent bg) and "Explore Markets" (secondary/surface-light bg)
- [ ] 1.5 Wire "Fund Account & Trade" button to call `useStore.getState().navigate('deposit')` on click
- [ ] 1.6 Wire "Explore Markets" button to call `useStore.getState().navigate('home')` on click

## 2. Animations

- [ ] 2.1 Wrap the CheckCircle2 icon in a `motion.div` with initial={{ scale: 0 }} animate={{ scale: 1 }} transition={{ type: "spring", stiffness: 200 }}
- [ ] 2.2 Wrap the button group in a `motion.div` with initial={{ opacity: 0, y: 20 }} animate={{ opacity: 1, y: 0 }} transition={{ delay: 0.3 }} and staggerChildren for each button
- [ ] 2.3 Each button wrapped in a `motion.div` child with stagger offset for sequential reveal

## 3. App Shell Wiring

- [ ] 3.1 Add YoureInScreen to the screen router in `page.tsx` so it renders when `store.screen === 'youre-in'`
- [ ] 3.2 Confirm BottomNav is not rendered when screen is 'youre-in' (should already be handled by core-components conditional logic; add to exclusion list if needed)

## 4. Verification

- [ ] 4.1 Run the app and confirm the You're In screen renders inside PhoneFrame with check icon, heading, and two buttons centered
- [ ] 4.2 Tap "Fund Account & Trade" and confirm navigation to 'deposit' screen
- [ ] 4.3 Tap "Explore Markets" and confirm navigation to 'home' screen
- [ ] 4.4 Confirm check icon spring animation and staggered button animations play on mount
