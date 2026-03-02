## Why

After onboarding, users land on the Home screen — the primary engagement surface of the app. It must let users discover markets (trending, watchlist, top movers), see their balance at a glance, and tap into any market to trade. Without this screen the core loop has no entry point.

## What Changes

- Create `MarketRow` component (`src/components/MarketRow.tsx`) — reusable row showing pair name, price, 24h change %, and ChevronRight, tappable to navigate to 'trade' with that pair selected
- Create `HomeScreen` component (`src/components/screens/HomeScreen.tsx`) — full scrollable home layout with header, Trending section, Watchlist section, Top Movers horizontal scroll
- Header row: hamburger Menu icon (left), "MF Perps" text-lg font-bold (center), "$648.50" balance text-sm font-semibold (right, tappable → 'portfolio')
- "🔥 Trending" section: text-xs uppercase section header, 3 MarketRows for top 3 markets by 24h change %
- "Your Watchlist" section: header, MarketRows for BTC/USD and ETH/USD, "+ Add market" accent row
- "Top Movers" section: horizontal scrollable row of small cards (w-24, surface bg, rounded-xl, p-3) showing pair + change %
- Wire HomeScreen into the screen router in `page.tsx` for `screen === 'home'`
- BottomNav visible with Home as active tab

## Capabilities

### New Capabilities
- `market-row`: MarketRow component displaying pair, price, change %, and navigation to trade screen
- `home-screen`: HomeScreen layout with header, trending markets, watchlist, top movers, and balance navigation

### Modified Capabilities

## Impact

- Adds 2 new files under `src/components/` and `src/components/screens/`
- Updates `page.tsx` screen router to render HomeScreen for the 'home' screen state
- Depends on: PhoneFrame, StatusBar, BottomNav, Card, Zustand store, mock-data (from core-components change)
