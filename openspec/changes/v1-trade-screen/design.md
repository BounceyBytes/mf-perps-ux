## Context

The core-components change provides PhoneFrame, BottomNav, base components, Zustand store, and mock data. The home-screen change provides the market discovery surface where users select a pair and navigate to 'trade'. This screen is the destination — where the user commits capital and opens a position. It must feel fast, clear, and confident. Everything happens on one screen with no intermediate review step before the overlay.

## Goals / Non-Goals

**Goals:**
- A single-screen trade interface that renders inside PhoneFrame with BottomNav (Trade active)
- Chart placeholder with timeframe pills to feel like a real trading app
- Long/Short toggle that changes CTA color/text and summary dynamically
- Amount input with quick-select chips for fast entry
- Custom LeverageSlider with color-coded risk feedback (green/yellow/red)
- Summary section computing position size, liquidation price, and fee from current inputs
- CTA button that shows the full order description and triggers the trade-confirmation overlay
- Framer Motion number transitions on all dynamic values

**Non-Goals:**
- No real charting library or live price data (SVG placeholder only)
- No order types (limit, stop-loss) — market orders only in v1
- No separate review/confirmation screen — CTA goes straight to overlay
- No actual position creation logic — this is a clickable prototype
- No pair selector or search on this screen — pair comes from store.selectedPair

## Decisions

1. **Single-screen layout, no review step** — Reduces friction. Tapping CTA opens the confirmation overlay directly. Users see all details on-screen before tapping.
2. **LeverageSlider as a separate component** — Complex enough to warrant extraction. Color-coded track, dynamic label, and warning text make it reusable and testable in isolation.
3. **Color-coded leverage risk** — Green (2-25x) = safe, yellow (25-50x) = caution, red (50-100x) = danger. Matches mental model of risk escalation. Warning text appears above 25x.
4. **Long = green, Short = red** — Universal trading convention. Green (#00D68F) for bullish/long, red (#FF4757) for bearish/short. CTA color matches selected direction.
5. **Amount quick-select chips** — $25, $50, $100 provide fast one-tap entry. Active chip has accent border. Tapping a chip sets the amount input value.
6. **Default values: Long, $50, 10x** — Safe defaults that produce a $500 position. Reasonable starting point that demonstrates the UI without being reckless.
7. **Summary computed from inputs** — Position size = amount × leverage. Fee = 0.05% of position size. Liquidation price = mock calculation (entry price ± entry price / leverage, depending on direction). All update dynamically.
8. **CTA text is descriptive** — "Open Long $500 BTC at $67,156" tells the user exactly what they're doing. Two lines of text in the button. Disabled when amount is 0.
9. **Chart is decorative** — Simple SVG wavy line in accent color inside a Card. Timeframe pills (1H, 4H, 1D, 1W) are tappable but only switch active state visually. No data changes.
10. **pb-24 for BottomNav clearance** — Same pattern as HomeScreen to prevent content from being hidden behind the fixed BottomNav.

## Risks / Trade-offs

- [Mock liquidation price is not accurate] → Acceptable for prototype. Uses simplified formula (entry ± entry/leverage). Real implementation would use proper margin calculations.
- [No real chart data] → SVG placeholder is sufficient for UX validation. Real charting comes with live data integration.
- [LeverageSlider uses native range input] → Styled with CSS. May look slightly different across browsers. Acceptable for prototype since the real app will be React Native.
- [All numbers animate on every change] → Could feel janky if overdone. Keep animations short (200-300ms) and only on final values, not during active slider dragging.
