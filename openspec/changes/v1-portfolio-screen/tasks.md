## 1. PositionCard Component

- [ ] 1.1 Create `src/components/PositionCard.tsx` accepting position props (pair, direction, leverage, pnl, pnlPercent, entryValue, currentValue, health)
- [ ] 1.2 Render top row: "{pair} {direction} {leverage}x" with direction colored green (#00D68F) for Long, red (#FF4757) for Short
- [ ] 1.3 Render P&L line: "+$12.80 (+2.56%)" in text-lg font-bold, green if positive, red if negative
- [ ] 1.4 Render value progression: "$500 → $512.80" in text-sm text-secondary
- [ ] 1.5 Render HealthBar: h-1.5 rounded track with fill width = health%, color green >60%, yellow (#FFD93D) 30-60%, red <30%. Label "{N}% to liq" in matching color
- [ ] 1.6 Render right-aligned "Close" button (surface-light bg, rounded-lg, text-sm) wired to `store.showOverlay('close-position')`
- [ ] 1.7 Apply 3px left border: green for Long, red for Short. Use surface bg, rounded-xl, p-4 for the card.

## 2. Portfolio Value Chart

- [ ] 2.1 Create portfolio area chart section (~140px tall) with SVG or canvas mock — upward curve with area fill
- [ ] 2.2 Set fill color to green (#00D68F) when total P&L is positive, red (#FF4757) when negative
- [ ] 2.3 Render dashed horizontal break-even line across the chart
- [ ] 2.4 Add time-range pills row: 1D, 1W, 1M (default active), 3M, ALL — tappable with active state styling (accent bg/border)
- [ ] 2.5 Implement touch scrub gesture that updates header total and P&L values on drag (stretch goal)

## 3. PortfolioScreen Header

- [ ] 3.1 Create `src/components/screens/PortfolioScreen.tsx` with scrollable container (px-4 pt-2 pb-24 overflow-y-auto)
- [ ] 3.2 Render header row: "Portfolio" (text-lg font-bold left), "$648.50" total (text-2xl font-bold right) with "+$12.30" P&L (text-sm green) beneath

## 4. Open Positions Section

- [ ] 4.1 Add "Open Positions (2)" section header (text-xs uppercase tracking-wider text-muted)
- [ ] 4.2 Render PositionCard for each open position from mock data, stacked with gap-3

## 5. Available Balance & Deposit Link

- [ ] 5.1 Render available balance row: "Available" label with "$48.50" value
- [ ] 5.2 Add "Fund Account" accent link (#7B61FF) wired to `store.navigate('deposit')`

## 6. Yield Teaser Card

- [ ] 6.1 Create yield teaser card with gradient border effect (accent #7B61FF → green #00D68F) using wrapper div with gradient bg and inner surface div
- [ ] 6.2 Add content: "Earn up to 8.2% target APY (variable)..." text, TrendingUp icon in green, "Learn More →" in accent color
- [ ] 6.3 Add "Not guaranteed." disclaimer in text-xs text-muted

## 7. History Section

- [ ] 7.1 Add "History" section header (text-xs uppercase tracking-wider text-muted)
- [ ] 7.2 Render closed position row: "SOL Long — Closed" with "+$45.00" in green and "2 hours ago"
- [ ] 7.3 Render closed position row: "DOGE Short — Closed" with "-$12.00" in red and "Yesterday"

## 8. Animations

- [ ] 8.1 Add Framer Motion count-up animation on header P&L value (animate from 0 to final on mount)
- [ ] 8.2 Add Framer Motion count-up animation on each PositionCard P&L value
- [ ] 8.3 Add Framer Motion count-up animation on history P&L values

## 9. App Shell Wiring

- [ ] 9.1 Add PortfolioScreen to the screen router in `page.tsx` so it renders when `store.screen === 'portfolio'`
- [ ] 9.2 Confirm BottomNav renders with Portfolio as active tab when on this screen

## 10. Verification

- [ ] 10.1 Run the app and confirm the Portfolio screen renders inside PhoneFrame with header, chart, positions, and BottomNav
- [ ] 10.2 Confirm PositionCards display correct direction coloring, P&L, health bars, and left borders
- [ ] 10.3 Tap "Close" on a PositionCard and confirm `showOverlay('close-position')` is called
- [ ] 10.4 Tap "Fund Account" and confirm navigation to 'deposit'
- [ ] 10.5 Confirm P&L count-up animations fire on mount
- [ ] 10.6 Confirm time-range pills toggle active state and chart area renders correctly
