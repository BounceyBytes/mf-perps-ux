## Context

The core-components change provides the PhoneFrame, BottomNav, base components, Zustand store, and mock data. The onboarding flow (welcome → kyc → referral → youre-in) ends by navigating to the home screen. This is the first screen in the core loop — users discover markets here and tap through to the trade screen.

## Goals / Non-Goals

**Goals:**
- A scrollable home screen that renders inside PhoneFrame with BottomNav (Home active)
- A reusable MarketRow component used by both Trending and Watchlist sections (and reusable on future screens)
- Header with hamburger icon, brand name, and tappable balance
- Three discovery sections: Trending (top 3 by change %), Watchlist (BTC + ETH), Top Movers (horizontal scroll)
- Tapping any market sets selectedPair and navigates to 'trade'
- Tapping balance navigates to 'portfolio'

**Non-Goals:**
- No gamification elements (streak widget, challenge card) — those are v2
- No real market data or live prices
- No hamburger menu functionality (icon is decorative for now)
- No "Add market" functionality beyond the static row

## Decisions

1. **MarketRow as a separate component** — Used in Trending, Watchlist, and potentially the trade screen pair selector. Accepts pair, price, change24h props and handles its own styling and navigation.
2. **Top 3 trending derived from mock data** — Sort markets by absolute change24h descending, take first 3. No separate trending data source.
3. **Watchlist is hardcoded** — BTC/USD and ETH/USD. No user-configurable watchlist in v1.
4. **Top Movers uses all markets** — Horizontal scroll shows all 7 mock markets as small cards. No filtering.
5. **Balance from mock user data** — Header balance reads `user.balance` from mock-data ($648.50). Not computed from positions.
6. **pb-24 for BottomNav clearance** — Scrollable content has bottom padding so the last section isn't hidden behind the fixed BottomNav.

## Risks / Trade-offs

- [Hardcoded watchlist limits realism] → Acceptable for prototype. The "+ Add market" row hints at future functionality.
- [No hamburger menu implementation] → Menu icon is visual only in v1. Tapping it does nothing. Can be wired to a profile/settings screen in a later change.
- [MarketRow renders static prices] → Mock data only. Prices don't update. This is a clickable prototype, not a live trading app.
