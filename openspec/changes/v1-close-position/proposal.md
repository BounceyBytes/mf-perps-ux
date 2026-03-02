## Why

When a user taps "Close" on a PositionCard in the Portfolio screen, there is no confirmation step or feedback before the position is removed. Without a close-position overlay, users could accidentally close positions with no way to review the P&L outcome first. The close-position bottom sheet provides a deliberate confirmation moment — showing the user what they'll receive before committing — and handles the removal animation and success toast for a satisfying close flow.

## What Changes

- Create `ClosePosition` component (`src/components/overlays/ClosePosition.tsx`) — a Framer Motion bottom sheet overlay that slides up from the bottom of the phone frame with spring animation, rendered when `store.overlay === 'close-position'`
- Backdrop: fixed overlay `bg-black/50`, tapping backdrop dismisses the sheet via `store.dismissOverlay()`
- Sheet container: surface background, `rounded-t-3xl`, `px-6 py-8`, with a drag handle bar (`w-10 h-1 rounded-full bg-[#2A2A3A]`) centered at the top
- Content:
  - "Close BTC Long?" heading (text-xl font-bold, centered)
  - Summary section (mt-4) with two rows in text-sm: "Your P&L" → "+$12.80" (green, font-semibold), "You'll receive" → "$512.80" (text-primary, font-semibold)
  - "Close Full Position" — Primary Button, full width, mt-6, accent background. On tap: dismiss overlay, remove position from portfolio list (animate out), show success toast "Position closed — $512.80 received"
  - "Close Partial ▼" — ghost text link, centered, mt-3, text-sm text-secondary. On tap: expand a slider (0–100%) with AnimatePresence. Stretch feature — animation + basic slider UI, does not need to be functional.
  - "Cancel" — ghost text link, centered, mt-3, text-sm text-muted. On tap: dismiss overlay
- Swipe-down to dismiss: Framer Motion drag on y-axis, if drag exceeds 100px the sheet dismisses
- Wire overlay into the overlay layer in `page.tsx` so it renders when `store.overlay === 'close-position'`

## Capabilities

### New Capabilities
- `close-position`: Bottom sheet overlay with P&L summary, close confirmation, partial close stretch feature, and success toast on position removal

### Modified Capabilities

## Impact

- Adds 1 new file under `src/components/overlays/`
- Updates `page.tsx` overlay layer to render ClosePosition when `store.overlay === 'close-position'`
- Depends on: PhoneFrame, Button, Zustand store (from core-components change)
- Depends on: PositionCard triggering `showOverlay('close-position')` (from portfolio-screen change)
- On close confirmation: removes position from `openPositions` in store (or mock data), animates the PositionCard out of the portfolio list, and shows a toast notification
- **Share card trigger**: When the closed position has positive P&L (profit), the close flow triggers the share-card overlay after dismissal so the user can celebrate and share their win
