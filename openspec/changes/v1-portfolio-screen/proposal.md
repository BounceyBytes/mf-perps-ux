## Why

After users open positions from the Trade screen, they need a central place to monitor their portfolio — total value, P&L, open positions with health indicators, and closed position history. The Portfolio screen is the "account dashboard" of the app. Without it, users have no visibility into their capital allocation, no way to close positions, and no path to the deposit or withdraw flows. It also surfaces the yield teaser — the first touchpoint in the RWA trojan horse strategy.

## What Changes

- Create `PortfolioScreen` component (`src/components/screens/PortfolioScreen.tsx`) — full scrollable portfolio layout rendered inside PhoneFrame with:
  - Header row: "Portfolio" (text-lg font-bold left), total "$648.50" (text-2xl font-bold right) with P&L "+$12.30" (text-sm green) beneath
  - Portfolio value area chart (~140px tall) with green fill when P&L positive, red when negative, dashed break-even line, and time-range pills (1D, 1W, 1M default, 3M, ALL). Touch scrub updates header values.
  - "Open Positions (2)" section header (text-xs uppercase tracking-wider text-muted)
  - PositionCard components (stacked, gap-3) showing pair/direction/leverage, P&L, value progression, health bar with liquidation distance, close button, and 3px colored left border
  - Available balance "$48.50" with "Fund Account" accent link navigating to 'deposit'
  - Yield teaser card with gradient border (accent→green), target APY, TrendingUp icon, "Learn More →" accent link, and disclaimer caption
  - "History" section with two closed position rows showing pair, result, P&L color, and relative timestamp
- Create `PositionCard` component (`src/components/PositionCard.tsx`) — reusable card for open positions with direction coloring, P&L display, health bar, and close action
- P&L numbers animate (count up) on mount with Framer Motion
- Wire PortfolioScreen into the screen router in `page.tsx` for `screen === 'portfolio'`
- BottomNav visible with Portfolio tab active

## Capabilities

### New Capabilities
- `portfolio-screen`: PortfolioScreen layout with value chart, open positions, available balance, yield teaser, and history
- `position-card`: PositionCard component displaying direction, P&L, value, health bar, and close action

### Modified Capabilities

## Impact

- Adds 2 new files under `src/components/` and `src/components/screens/`
- Updates `page.tsx` screen router to render PortfolioScreen for the 'portfolio' screen state
- Depends on: PhoneFrame, StatusBar, BottomNav, Card, Zustand store, mock-data (from core-components change)
- Connects to close-position overlay (separate change) and deposit flow (separate change)
