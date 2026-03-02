## Why

After a user taps the CTA on the Trade screen, there is no feedback confirming the position was opened. Without a confirmation overlay, users have no visual closure for their trade action and no clear path to view their position, trade again, or set risk management. The trade-confirmation bottom sheet provides that feedback loop — a satisfying moment that validates the action and offers clear next steps.

## What Changes

- Create `TradeConfirmation` component (`src/components/overlays/TradeConfirmation.tsx`) — a Framer Motion bottom sheet overlay that slides up from the bottom of the phone frame with spring animation, rendered when `store.overlay === 'trade-confirmation'`
- Backdrop: fixed overlay `bg-black/50`, tapping backdrop dismisses the sheet via `store.dismissOverlay()`
- Sheet container: surface background, `rounded-t-3xl`, `px-6 py-8`, max height 50% of phone frame, with a drag handle bar (`w-10 h-1 rounded-full bg-[#2A2A3A]`) centered at the top
- Content: large green CheckCircle2 icon (48px, scales in with spring), "Position Opened" heading (text-xl font-bold, fades in), summary Card showing trade parameters (e.g., "BTC Long $500 @ 10x", "Entry: $67,156"), and three action buttons:
  1. "View Position" — Primary Button → `navigate('portfolio')` + `dismissOverlay()`
  2. "Trade Again" — Secondary Button → `dismissOverlay()` (stay on trade screen)
  3. "Set TP/SL" — Secondary Button → placeholder (no-op for v1)
- Swipe-down to dismiss: Framer Motion drag on y-axis, if drag exceeds 100px the sheet dismisses
- Wire overlay into the overlay layer in `page.tsx` so it renders when `store.overlay === 'trade-confirmation'`

## Capabilities

### New Capabilities
- `trade-confirmation`: Bottom sheet overlay with success feedback, trade summary, and action buttons for post-trade navigation

### Modified Capabilities

## Impact

- Adds 1 new file under `src/components/overlays/`
- Updates `page.tsx` overlay layer to render TradeConfirmation when `store.overlay === 'trade-confirmation'`
- Depends on: PhoneFrame, Button, Card, Zustand store (from core-components change)
- Depends on: TradeScreen triggering `showOverlay('trade-confirmation')` (from trade-screen change)
- Reads trade parameters (pair, direction, amount, leverage, entry price) from store or props
