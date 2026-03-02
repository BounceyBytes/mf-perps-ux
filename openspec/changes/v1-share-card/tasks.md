## 1. ShareCard Component Setup

- [ ] 1.1 Create `src/components/overlays/ShareCard.tsx` as a client component
- [ ] 1.2 Read overlay state from Zustand store, only render when `store.overlay === 'share-card'`
- [ ] 1.3 Render fixed full-screen backdrop with `bg-black/80` covering the phone frame area, centered flex layout

## 2. Share Card Design

- [ ] 2.1 Render card container with `max-w-[320px]`, `rounded-2xl`, `overflow-hidden`, gradient background from #14141F to #1a1530
- [ ] 2.2 Add top accent bar: 4px tall, full-width green gradient
- [ ] 2.3 Add inner content area with `p-6`
- [ ] 2.4 Render position line: "🟢 BTC Long" in `text-lg font-bold` green
- [ ] 2.5 Render hero PnL: "+47.2%" in `text-4xl font-bold text-green`
- [ ] 2.6 Render dollar breakdown: "$500 → $735.00" in `text-sm text-secondary`
- [ ] 2.7 Render user info (mt-4): 24px circular avatar + "Jake" in text-xs
- [ ] 2.8 Render divider (mt-4): `border-t border-[#2A2A3A]`
- [ ] 2.9 Render referral area (mt-4): "Trade on MF Perps" text-sm font-semibold, "mfperps.app/join/JAKE2026" text-xs text-accent
- [ ] 2.10 Render QR placeholder: 64×64 `rounded-lg` box with surface-light background

## 3. Card Entrance Animation

- [ ] 3.1 Wrap card in Framer Motion `motion.div` with `initial={{ scale: 0.8, opacity: 0 }}`, `animate={{ scale: 1, opacity: 1 }}`, spring transition
- [ ] 3.2 Add `exit={{ scale: 0.8, opacity: 0 }}` for dismiss animation

## 4. Action Buttons & Done Link

- [ ] 4.1 Add button group below card (mt-6, flex flex-col gap-3, px-6)
- [ ] 4.2 "Share" — Primary Button with Share2 icon from Lucide; on tap show toast "Shared!"
- [ ] 4.3 "Save Image" — Secondary Button with Download icon from Lucide; on tap show toast "Saved!"
- [ ] 4.4 "Done" — text link centered below buttons, `text-sm text-muted`; on tap call `store.dismissOverlay()`

## 5. Toast Mechanism

- [ ] 5.1 Implement simple toast state (local component state or store) that renders a brief "Shared!" or "Saved!" message and auto-dismisses after ~2 seconds
- [ ] 5.2 Style toast: centered, surface-light bg, rounded-lg, text-sm, positioned above Done link or at bottom of card area

## 6. App Shell Wiring

- [ ] 6.1 Import ShareCard in `page.tsx` and render it in the overlay layer, conditionally when `store.overlay === 'share-card'`
- [ ] 6.2 Wrap ShareCard in `AnimatePresence` for exit animations

## 7. Verification

- [ ] 7.1 Run the app and trigger `store.showOverlay('share-card')`, confirm full-screen overlay appears with dark backdrop
- [ ] 7.2 Verify card renders with gradient background, green accent bar, position info, PnL, dollar breakdown, user info, divider, and referral area with QR placeholder
- [ ] 7.3 Verify card animates in with scale 0.8→1 and opacity 0→1
- [ ] 7.4 Tap "Share" and confirm "Shared!" toast appears
- [ ] 7.5 Tap "Save Image" and confirm "Saved!" toast appears
- [ ] 7.6 Tap "Done" and confirm overlay dismisses with exit animation
- [ ] 7.7 Reopen overlay and confirm card re-animates in correctly
