## 1. LeverageSlider Component

- [ ] 1.1 Create `src/components/LeverageSlider.tsx` accepting `value` (number) and `onChange` (callback) props
- [ ] 1.2 Render range input with min=2, max=100, h-2 rounded-full track, and w-6 h-6 white thumb
- [ ] 1.3 Color-code the track fill: green (#00D68F) for 2-25x, yellow (#F7B731) for 25-50x, red (#FF4757) for 50-100x
- [ ] 1.4 Display dynamic label above the slider showing value + "x" (e.g., "10x") in the matching risk color
- [ ] 1.5 Show "2x" left and "100x" right labels in text-xs text-muted
- [ ] 1.6 Display warning text below slider when value > 25: "High leverage increases liquidation risk" (26-50x, yellow) or "Extreme leverage — high liquidation risk" (>50x, red)

## 2. TradeScreen Header & Chart

- [ ] 2.1 Create `src/components/screens/TradeScreen.tsx` with scrollable container (pt-2 pb-24)
- [ ] 2.2 Add header row: back arrow (ArrowLeft icon, tappable → navigate('home')), pair name centered (text-lg font-semibold), current price right (text-sm tabular-nums) — read selectedPair and look up price from mock data
- [ ] 2.3 Add chart placeholder Card (mt-2, mx-4, h-48) with simple SVG wavy upward line in accent color (#7B61FF)
- [ ] 2.4 Add timeframe pills below chart: "1H", "4H", "1D" (active by default), "1W" as rounded-full buttons with local state for active pill — active: accent bg + white text, inactive: surface-light bg + text-muted

## 3. Long/Short Toggle

- [ ] 3.1 Add Long/Short toggle (mt-4, mx-4): two equal-width rounded-xl h-12 buttons with local state defaulting to 'long'
- [ ] 3.2 Style Long selected: green bg (#00D68F), white text, "(up)" subtext; Short unselected: surface-light bg, text-muted
- [ ] 3.3 Style Short selected: red bg (#FF4757), white text, "(down)" subtext; Long unselected: surface-light bg, text-muted

## 4. Amount Input & Chips

- [ ] 4.1 Add amount section (mt-4, mx-4): "Amount" label in text-xs text-secondary
- [ ] 4.2 Add input with surface-light bg, "$" prefix, text-right, text-lg, default value "50.00" as local state
- [ ] 4.3 Add quick-select chips below input: "$25", "$50", "$100" as rounded-full pills in a flex row with gap-2
- [ ] 4.4 Wire chip tap to set amount value; active chip (matching current amount) gets accent border (#7B61FF)

## 5. Leverage Integration

- [ ] 5.1 Add LeverageSlider (mt-4, mx-4) with local state defaulting to 10
- [ ] 5.2 Wire onChange to update leverage state, which feeds into summary calculations

## 6. Summary Section

- [ ] 6.1 Add summary section (mt-4, mx-4) with three text-sm rows using flex justify-between
- [ ] 6.2 "Position size" row: compute amount × leverage, format as currency
- [ ] 6.3 "Liquidation price" row: compute entry price − (entry price / leverage) for Long, entry price + (entry price / leverage) for Short, format as currency
- [ ] 6.4 "Fee" row: compute 0.05% of position size, format as currency
- [ ] 6.5 Wrap all computed values in Framer Motion animated number transitions (200-300ms)

## 7. CTA Button

- [ ] 7.1 Add CTA button (mt-4, mx-4, h-14, rounded-xl, full-width): green bg for Long, red bg for Short
- [ ] 7.2 Dynamic two-line text: "Open Long/Short $[positionSize] [pair] at $[price]"
- [ ] 7.3 Disable button (opacity-50, pointer-events-none) when amount is 0 or empty
- [ ] 7.4 Wire tap to call `store.showOverlay('trade-confirmation')`

## 8. App Shell Wiring

- [ ] 8.1 Add TradeScreen to the screen router in `page.tsx` so it renders when `store.screen === 'trade'`
- [ ] 8.2 Confirm BottomNav renders with Trade as active tab when on this screen

## 9. Verification

- [ ] 9.1 Run the app and confirm TradeScreen renders inside PhoneFrame with header, chart, toggle, amount, leverage, summary, CTA, and BottomNav
- [ ] 9.2 Toggle Long/Short and confirm CTA color, text, summary, and liquidation price update correctly
- [ ] 9.3 Change amount via chips and manual input; confirm summary and CTA recalculate
- [ ] 9.4 Drag leverage slider across the full range; confirm color transitions, warnings, and summary updates
- [ ] 9.5 Tap CTA and confirm trade-confirmation overlay is triggered
- [ ] 9.6 Tap back arrow and confirm navigation to home screen
