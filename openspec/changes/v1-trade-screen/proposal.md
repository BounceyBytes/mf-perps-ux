## Why

The trade screen is the most important screen in the app — the core revenue-generating surface where users actually open positions. Without it, the entire funnel (onboarding → home → trade) has no destination. Users tapping a market from the Home screen need to land on a clear, single-screen trading interface that lets them pick direction, set amount and leverage, see a position summary, and execute — all without navigating to a separate review page.

## What Changes

- Create `LeverageSlider` component (`src/components/LeverageSlider.tsx`) — custom slider with color-coded track (green 2-25x, yellow 25-50x, red 50-100x), white thumb, dynamic label, and high-leverage warning text
- Create `TradeScreen` component (`src/components/screens/TradeScreen.tsx`) — full single-screen trading layout rendered inside PhoneFrame with:
  - Header: back arrow navigating to 'home', centered pair name "BTC / USD" (text-lg font-semibold), current price "$67,156" (text-sm tabular-nums right)
  - Chart placeholder: Card with h-48 SVG line chart (wavy upward line in accent color) and timeframe pills (1H, 4H, 1D active, 1W)
  - Long/Short toggle: two equal-width buttons — Long (green #00D68F) / Short (red #FF4757), default Long selected
  - Amount input: "$" prefix, text-right, text-lg, default "50.00", quick-select chips ($25/$50/$100)
  - LeverageSlider: default 10x, range 2-100x
  - Summary section: position size, liquidation price, fee (0.05%)
  - CTA button: full-width, dynamic text "Open Long/Short $X PAIR at $PRICE", green/red bg matching direction
- Wire TradeScreen into the screen router in `page.tsx` for `screen === 'trade'`
- Tapping CTA calls `showOverlay('trade-confirmation')`
- BottomNav visible with Trade tab active
- All number values animate with Framer Motion

## Capabilities

### New Capabilities
- `leverage-slider`: Custom slider component with color-coded track, dynamic label, and high-leverage warning
- `trade-screen`: TradeScreen layout with chart, direction toggle, amount input, leverage, summary, and CTA

### Modified Capabilities

## Impact

- Adds 2 new files under `src/components/` and `src/components/screens/`
- Updates `page.tsx` screen router to render TradeScreen for the 'trade' screen state
- Depends on: PhoneFrame, StatusBar, BottomNav, Card, Button, Zustand store, mock-data (from core-components change)
- Connects to trade-confirmation overlay (separate change)
