## 1. WelcomeScreen Component

- [ ] 1.1 Create `src/components/screens/WelcomeScreen.tsx` with a full-height flex column layout (min-h-full, flex, flex-col, items-center, justify-between)
- [ ] 1.2 Add brand logo block: "MF" in accent (#7B61FF) + "Perps" in white, text-3xl font-bold, centered with pt-24
- [ ] 1.3 Add tagline: "Trade BTC, ETH & more" (text-lg text-primary) and "Up to 100x leverage" (text-sm text-secondary), centered below logo
- [ ] 1.4 Add three auth buttons in a stacked container (gap-3, px-6, w-full): "Continue with Apple" (white bg, black text, inline Apple SVG icon), "Continue with Google" (secondary variant, inline Google SVG icon), "Use email or phone" (ghost variant, Lucide Mail icon)
- [ ] 1.5 Wire all three auth buttons to call `useStore.getState().navigate('kyc')` on click
- [ ] 1.6 Add bottom link: "Already have an account? Sign in" with "Sign in" in accent color, tappable, also navigates to 'kyc'

## 2. Animations

- [ ] 2.1 Wrap the WelcomeScreen root in a `motion.div` with initial={{ opacity: 0 }} animate={{ opacity: 1 }} transition={{ duration: 0.5 }}
- [ ] 2.2 Wrap the auth button group in a `motion.div` with staggerChildren: 0.1 variant, and each button in a `motion.div` with initial={{ opacity: 0, y: 20 }} animate={{ opacity: 1, y: 0 }}
- [ ] 2.3 Ensure all auth buttons have whileTap={{ scale: 0.97 }} (via Button component or direct motion props)

## 3. App Shell Wiring

- [ ] 3.1 Add WelcomeScreen to the screen router in `page.tsx` so it renders when `store.screen === 'welcome'`
- [ ] 3.2 Confirm BottomNav is not rendered when screen is 'welcome' (should already be handled by core-components conditional logic)

## 4. Verification

- [ ] 4.1 Run the app and confirm the Welcome screen renders inside PhoneFrame with logo, tagline, buttons, and sign-in link
- [ ] 4.2 Tap each auth button and confirm navigation to 'kyc' screen
- [ ] 4.3 Confirm fade-in and staggered button animations play on mount
