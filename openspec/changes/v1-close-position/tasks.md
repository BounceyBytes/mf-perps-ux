## 1. Store Updates

- [ ] 1.1 Add `closingPosition` field to Zustand store (`{ pair, direction, pnl, currentValue } | null`, default null) and a `setClosingPosition(pos)` action
- [ ] 1.2 Add `toast` field to Zustand store (`string | null`, default null) and a `showToast(msg)` action that sets the toast and auto-clears after 2.5 seconds via setTimeout (consistent with toast-notification spec)
- [ ] 1.3 Add `closePosition(positionId)` action to Zustand store that removes the position from the `openPositions` array
- [ ] 1.4 Update PositionCard close button handler to call `setClosingPosition(position)` before calling `showOverlay('close-position')`

## 2. ClosePosition Component Setup

- [ ] 2.1 Create `src/components/overlays/ClosePosition.tsx` as a client component
- [ ] 2.2 Read overlay state from Zustand store, only render when `store.overlay === 'close-position'`
- [ ] 2.3 Render fixed backdrop with `bg-black/50` covering the phone frame area; wire `onClick` to `store.dismissOverlay()`

## 3. Bottom Sheet Container & Animation

- [ ] 3.1 Render a Framer Motion `motion.div` for the sheet with `initial={{ y: "100%" }}`, `animate={{ y: 0 }}`, `exit={{ y: "100%" }}`, spring transition (damping ~25, stiffness ~300)
- [ ] 3.2 Style sheet: surface bg, `rounded-t-3xl`, `px-6 py-8`, positioned at the bottom of the phone frame
- [ ] 3.3 Add centered drag handle bar at top: `w-10 h-1 rounded-full bg-[#2A2A3A] mx-auto`
- [ ] 3.4 Enable `drag="y"` with `dragConstraints={{ top: 0 }}` and `dragElastic={0.2}`; on drag end, if `offset.y > 100` call `store.dismissOverlay()`

## 4. Heading & Summary

- [ ] 4.1 Render "Close {pair} {direction}?" heading: text-xl font-bold text-center, reading pair and direction from `store.closingPosition`
- [ ] 4.2 Render summary section (mt-4) with two justified rows in text-sm:
  - "Your P&L" (text-secondary) → P&L value (green if positive, red if negative, font-semibold)
  - "You'll receive" (text-secondary) → current value (text-primary, font-semibold)

## 5. Action Buttons & Links

- [ ] 5.1 Render "Close Full Position" — Primary Button, full width, mt-6, accent bg
- [ ] 5.2 On "Close Full Position" tap: call `store.closePosition(id)`, `store.dismissOverlay()`, `store.showToast('Position closed — $X received')`. If the closed position has positive P&L, trigger `store.showOverlay('share-card')` after a short delay (~500ms) to celebrate the profitable close.
- [ ] 5.3 Render "Close Partial ▼" — ghost text link, centered, mt-3, text-sm text-secondary; on tap toggle a local state boolean `showPartial`
- [ ] 5.4 Render AnimatePresence section: when `showPartial` is true, animate in a range slider (0–100%) with a percentage label below the link. Slider is visual only — updates local display percentage but does not affect store or close amount
- [ ] 5.5 Render "Cancel" — ghost text link, centered, mt-3, text-sm text-muted; on tap call `store.dismissOverlay()`

## 6. Toast Component

- [ ] 6.1 Create a Toast component (or add inline in `page.tsx`) that renders at the bottom of the phone frame when `store.toast` is not null
- [ ] 6.2 Style toast: surface-light bg, rounded-lg, px-4 py-3, text-sm text-primary, centered, with Framer Motion fade/slide-up entrance and exit
- [ ] 6.3 Wrap toast in AnimatePresence for smooth enter/exit

## 7. App Shell Wiring

- [ ] 7.1 Import ClosePosition in `page.tsx` and render it in the overlay layer, conditionally when `store.overlay === 'close-position'`
- [ ] 7.2 Wrap ClosePosition in `AnimatePresence` for exit animations
- [ ] 7.3 Render Toast component in the app shell, reading from `store.toast`

## 8. Verification

- [ ] 8.1 Run the app, navigate to portfolio, tap "Close" on a PositionCard, and confirm the close-position bottom sheet slides up with backdrop
- [ ] 8.2 Verify heading shows "Close BTC Long?" with correct pair and direction
- [ ] 8.3 Verify P&L row shows green value for positive P&L, and "You'll receive" row shows correct amount
- [ ] 8.4 Tap "Close Full Position" and confirm: overlay dismisses, position animates out of portfolio list, toast appears "Position closed — $X received"
- [ ] 8.5 Verify toast auto-dismisses after 2.5 seconds
- [ ] 8.6 Reopen overlay on another position, tap "Close Partial ▼" and confirm slider section animates in; tap again to collapse
- [ ] 8.7 Tap "Cancel" and confirm overlay dismisses
- [ ] 8.8 Tap backdrop and confirm overlay dismisses
- [ ] 8.9 Swipe sheet down > 100px and confirm it dismisses; swipe < 100px and confirm it snaps back
- [ ] 8.10 Close a position with positive P&L and verify the share-card overlay appears after ~500ms delay
