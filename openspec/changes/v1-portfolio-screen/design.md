## Context

The core-components change provides PhoneFrame, BottomNav, base components, Zustand store, and mock data (including `openPositions` with P&L, leverage, and health, plus `user` with balance and available). The home-screen change provides a tappable balance in the header that navigates to 'portfolio'. The trade screen lets users open positions — Portfolio is where they monitor and close them. This screen is the account hub: value tracking, position management, deposit/withdraw entry points, and the first RWA yield teaser.

## Goals / Non-Goals

**Goals:**
- A scrollable portfolio screen that renders inside PhoneFrame with BottomNav (Portfolio active)
- A reusable PositionCard component used for open positions (and reusable on future screens)
- Portfolio value area chart with time-range pills and touch scrub that updates header values
- Open positions section with PositionCard components showing full position detail and close action
- Available balance display with "Fund Account" link
- Yield teaser card surfacing the RWA conversion hook
- Closed position history section with P&L coloring
- Framer Motion count-up animation on P&L numbers on mount

**Non-Goals:**
- No real chart data or live price feeds — mock area chart with static data points
- No actual position closing logic — close button triggers the close-position overlay
- No yield product screens or functionality — teaser is informational only
- No withdraw entry point on this screen (withdraw is accessed elsewhere)
- No position detail drill-down — all info is visible on the card itself

## Decisions

1. **PositionCard as a separate component** — Contains enough complexity (direction coloring, health bar, P&L formatting, close action) to warrant extraction. Reusable if positions appear on other screens or overlays.
2. **Area chart is a styled mock** — SVG or canvas rendering of a simple upward/downward curve with fill. No charting library. Green fill when total P&L is positive, red when negative. Dashed horizontal line at break-even.
3. **Time-range pills are visual** — 1D, 1W, 1M (default active), 3M, ALL. Tapping switches the active pill but doesn't change chart data in the prototype. Touch scrub is a stretch goal — updates header P&L value on drag.
4. **Health bar color thresholds** — Green (#00D68F) above 60%, yellow (#FFD93D — see design tokens) between 30-60%, red (#FF4757) below 30%. Label shows "{N}% to liq" in the same color. Uses a thin h-1.5 track with rounded fill.
5. **Direction coloring convention** — Long = green (#00D68F), Short = red (#FF4757). Applied to direction text, 3px left border on PositionCard, and P&L values.
6. **P&L count-up animation** — Framer Motion `useMotionValue` and `useTransform` or `animate` to count dollar and percent values from 0 to final on mount. Keeps the screen feeling alive and data-forward.
7. **Yield teaser gradient border** — Uses a wrapper div with linear-gradient background (accent #7B61FF → green #00D68F) and inner div with surface background to create a 1-2px gradient border effect. TrendingUp icon in green. "Not guaranteed." in text-xs text-muted as legal disclaimer.
8. **History uses simple rows, not cards** — Closed positions are lightweight (no health bar, no close button). Simple rows with pair, direction, result label ("Closed"), P&L value, and relative timestamp.
9. **Close button triggers overlay** — Tapping "Close" on a PositionCard calls `showOverlay('close-position')`. The overlay itself is a separate change.
10. **pb-24 for BottomNav clearance** — Same pattern as HomeScreen and TradeScreen.

## Risks / Trade-offs

- [Mock chart has no real data points] → Acceptable for prototype. The area fill and time pills give the right feel. Real charting comes with live data integration.
- [Touch scrub is complex for a prototype] → Implement as a stretch goal. If too complex, the chart is static and header values don't change on interaction.
- [Health bar percentages are static] → Mock data provides fixed health values. No dynamic calculation based on price movement. Acceptable for UX validation.
- [Yield teaser has no destination] → "Learn More →" could navigate to a future screen or do nothing. For v1, it's informational only — the goal is to plant the RWA seed.
- [P&L animation fires every time screen mounts] → Could feel repetitive on repeated visits. Acceptable for prototype — in production, would only animate on first load or data change.
