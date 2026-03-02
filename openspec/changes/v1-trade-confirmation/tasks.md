## 1. TradeConfirmation Component Setup

- [ ] 1.1 Create `src/components/overlays/TradeConfirmation.tsx` as a client component
- [ ] 1.2 Read overlay state from Zustand store, only render when `store.overlay === 'trade-confirmation'`
- [ ] 1.3 Render fixed backdrop with `bg-black/50` covering the phone frame area; wire `onClick` to `store.dismissOverlay()`

## 2. Bottom Sheet Container & Animation

- [ ] 2.1 Render a Framer Motion `motion.div` for the sheet with `initial={{ y: "100%" }}`, `animate={{ y: 0 }}`, `exit={{ y: "100%" }}`, spring transition (damping ~25, stiffness ~300)
- [ ] 2.2 Style sheet: surface bg, `rounded-t-3xl`, `px-6 py-8`, max-h-[50%], positioned at the bottom of the phone frame
- [ ] 2.3 Add centered drag handle bar at top: `w-10 h-1 rounded-full bg-[#2A2A3A] mx-auto`
- [ ] 2.4 Enable `drag="y"` with `dragConstraints={{ top: 0 }}` and `dragElastic={0.2}`; on drag end, if `offset.y > 100` call `store.dismissOverlay()`

## 3. Success Icon & Heading

- [ ] 3.1 Render CheckCircle2 from Lucide (size 48, color #00D68F), centered, with Framer Motion `scale` spring animation (initial: 0, animate: 1)
- [ ] 3.2 Render "Position Opened" text below icon: `text-xl font-bold text-center mt-4`, with Framer Motion fade-in (opacity 0→1, delay ~200ms)

## 4. Summary Card

- [ ] 4.1 Add a Card component (mt-4) displaying trade params: "{PAIR} {Direction} ${positionSize} @ {leverage}x" on the first line
- [ ] 4.2 Display "Entry: ${entryPrice}" on the second line inside the same Card
- [ ] 4.3 Read trade parameters from Zustand store (selectedPair, direction, amount, leverage, entry price) — store `lastTrade` object on CTA tap if not already available

## 5. Action Buttons

- [ ] 5.1 Add a vertical button group (mt-6, flex flex-col gap-3)
- [ ] 5.2 "View Position" — Primary Button; on tap call `store.navigate('portfolio')` then `store.dismissOverlay()`
- [ ] 5.3 "Trade Again" — Secondary Button; on tap call `store.dismissOverlay()`
- [ ] 5.4 "Set TP/SL" — Secondary Button; on tap do nothing (placeholder for v1)

## 6. App Shell Wiring

- [ ] 6.1 Import TradeConfirmation in `page.tsx` and render it in the overlay layer, conditionally when `store.overlay === 'trade-confirmation'`
- [ ] 6.2 Wrap TradeConfirmation in `AnimatePresence` for exit animations

## 7. Store Updates (if needed)

- [ ] 7.1 Add `lastTrade` field to Zustand store to hold `{ pair, direction, amount, leverage, entryPrice }` set when CTA is tapped on the trade screen
- [ ] 7.2 Update trade screen CTA handler to populate `lastTrade` before calling `showOverlay('trade-confirmation')`

## 8. Verification

- [ ] 8.1 Run the app, navigate to trade screen, tap CTA, and confirm the bottom sheet slides up with backdrop
- [ ] 8.2 Verify checkmark scales in, heading fades in, summary card shows correct trade params
- [ ] 8.3 Tap "View Position" and confirm navigation to portfolio screen with overlay dismissed
- [ ] 8.4 Reopen overlay, tap "Trade Again" and confirm overlay dismisses while staying on trade screen
- [ ] 8.5 Tap "Set TP/SL" and confirm nothing happens
- [ ] 8.6 Tap backdrop and confirm overlay dismisses
- [ ] 8.7 Swipe sheet down > 100px and confirm it dismisses; swipe < 100px and confirm it snaps back
- [ ] 8.8 Verify that on the user's first position, a "Share Your Win 🎉" button appears and triggers the share-card overlay
