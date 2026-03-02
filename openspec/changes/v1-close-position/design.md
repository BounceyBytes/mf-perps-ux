## Context

The portfolio-screen change surfaces open positions with a "Close" button on each PositionCard. Tapping Close calls `store.showOverlay('close-position')`. This change builds the overlay that appears in response — a bottom sheet asking the user to confirm position closure, showing P&L and receive amount before committing. The core-components change provides PhoneFrame, Button, Zustand store, and mock data that this overlay depends on. The trade-confirmation change established the bottom sheet pattern (slide-up spring animation, backdrop, drag handle, swipe-to-dismiss) that this change reuses.

## Goals / Non-Goals

**Goals:**
- A bottom sheet overlay that slides up from the bottom with Framer Motion spring animation, matching the trade-confirmation pattern
- Semi-transparent backdrop (`bg-black/50`) that dismisses the sheet on tap
- Drag handle bar for visual affordance and swipe-down-to-dismiss gesture
- "Close BTC Long?" heading centered at the top (text-xl font-bold)
- Summary section with two rows: "Your P&L" with green value, "You'll receive" with primary-colored value
- "Close Full Position" primary button that dismisses the overlay, removes the position from the portfolio list with exit animation, and shows a success toast
- "Close Partial ▼" ghost link that expands a 0–100% slider via AnimatePresence (stretch feature, visual only)
- "Cancel" ghost link that dismisses the overlay
- Wire into the overlay layer in `page.tsx`

**Non-Goals:**
- No actual blockchain transaction or position management — this is a prototype confirmation
- Partial close slider does not need to be functional — it is a stretch feature for visual polish only
- No haptic feedback or sound effects
- No share functionality in this change
- No confirmation dialog before the close action — the bottom sheet itself is the confirmation step

## Decisions

1. **Same bottom sheet pattern as trade-confirmation** — Reuses the slide-up spring animation, backdrop tap-to-dismiss, drag handle, and swipe-down gesture. Keeps the interaction model consistent across overlays.
2. **"Close BTC Long?" as a question heading** — Framing as a question makes the user pause and consider, reducing accidental closures. Uses text-xl font-bold centered for prominence.
3. **Two-row summary instead of a Card** — The information is minimal (P&L and receive amount), so a lightweight two-row layout with justified text is cleaner than wrapping in a Card component. Each row: label (text-secondary) on the left, value (font-semibold) on the right.
4. **P&L colored green/red based on sign** — Positive P&L renders in green (#00D68F), negative in red (#FF4757). Consistent with PositionCard P&L coloring.
5. **"Close Full Position" as primary CTA** — Full-width accent button at mt-6. This is the main action. On tap: calls `store.dismissOverlay()`, removes the position from the store's positions array, and triggers a success toast.
6. **Position removal animates out** — The PositionCard in the portfolio list should animate out (e.g., opacity 0, height 0, or slideRight) when the position is removed from the store. AnimatePresence on the position list handles this automatically if positions are keyed.
7. **Success toast: "Position closed — $512.80 received"** — Brief, informative. Appears at the bottom of the phone frame, auto-dismisses after ~3 seconds. Simple implementation: a store field `toast` with text and a timeout to clear it.
8. **"Close Partial ▼" is a stretch feature** — Ghost text link (text-sm text-secondary, centered, mt-3). On tap: toggles an AnimatePresence section below it containing a range slider (0–100%) with a percentage label. The slider is visual only — it does not affect the close amount or any store state. The ▼ chevron hints at the expandable behavior.
9. **"Cancel" as muted ghost link** — text-sm text-muted, centered, mt-3. Least prominent action. Calls `store.dismissOverlay()`.
10. **Swipe-down to dismiss with 100px threshold** — Same as trade-confirmation: Framer Motion `drag="y"` with `dragConstraints={{ top: 0 }}`, dismiss if `offset.y > 100`.
11. **Reads position data from store** — The overlay reads the position being closed from a `closingPosition` field in the store (set when the PositionCard close button is tapped). Contains pair, direction, pnl, currentValue.

## Risks / Trade-offs

- [Position data may not be stored when Close is tapped] → The PositionCard close handler should set `store.closingPosition` with the position data before calling `showOverlay('close-position')`. Simple store update.
- [Toast system doesn't exist yet] → Add a minimal `toast` field to the store (string | null) with a `showToast(msg)` action that sets it and a setTimeout to clear after 3s. Render a toast component in the app shell.
- [Partial close slider is non-functional] → Acceptable for prototype. The slider is purely visual to validate the UX pattern. Real partial close logic would come in a future change.
- [Removing position from mock data is destructive] → For the prototype, removing from the store's array is fine. If the user wants to re-test, they refresh the page. Could add a "reset" dev tool later.
- [AnimatePresence on position list requires keyed items] → PositionCards must be rendered with unique keys (e.g., position ID) for exit animations to work. The portfolio-screen change should already handle this.
