## ADDED Requirements

### Requirement: Header displays back arrow, pair name, and current price
The TradeScreen SHALL render a header row with a back arrow (ChevronLeft or ArrowLeft icon) on the left, the selected pair name (e.g., "BTC / USD") in text-lg font-semibold centered, and the current price (e.g., "$67,156") in text-sm tabular-nums on the right.

#### Scenario: Header renders with selected pair
- **WHEN** the TradeScreen renders with store.selectedPair = 'BTC/USD'
- **THEN** a back arrow appears on the left, "BTC / USD" appears centered in text-lg font-semibold, and "$67,156" appears on the right in text-sm tabular-nums

#### Scenario: Back arrow navigates to home
- **WHEN** the user taps the back arrow
- **THEN** the app navigates to the 'home' screen

### Requirement: Chart placeholder renders with timeframe pills
The TradeScreen SHALL render a Card (mt-2, mx-4) with h-48 containing a simple SVG line chart — a wavy upward line in accent color (#7B61FF). Below the chart, four rounded-full timeframe pill buttons SHALL render: "1H", "4H", "1D", "1W". The "1D" pill SHALL be active by default with accent background and white text. Inactive pills SHALL use surface-light background and text-muted.

#### Scenario: Chart placeholder renders
- **WHEN** the TradeScreen renders
- **THEN** a Card with h-48 appears containing an SVG line in accent color

#### Scenario: 1D timeframe is active by default
- **WHEN** the TradeScreen renders
- **THEN** the "1D" pill has accent background (#7B61FF) and white text, while "1H", "4H", "1W" have surface-light background and text-muted

#### Scenario: User taps a timeframe pill
- **WHEN** the user taps the "1H" pill
- **THEN** "1H" becomes active (accent bg, white text) and "1D" becomes inactive (surface-light bg, text-muted)

### Requirement: Long/Short toggle switches direction
The TradeScreen SHALL render two equal-width toggle buttons (mt-4, mx-4, rounded-xl, h-12). "Long" shows "(up)" subtext and "Short" shows "(down)" subtext. When Long is selected, its background SHALL be green (#00D68F) with white text and Short SHALL use surface-light (#1E1E2E) with text-muted. When Short is selected, its background SHALL be red (#FF4757) with white text and Long SHALL use surface-light with text-muted. Default selection SHALL be Long.

#### Scenario: Default state is Long selected
- **WHEN** the TradeScreen renders
- **THEN** "Long (up)" has green background with white text, and "Short (down)" has surface-light background with text-muted

#### Scenario: User selects Short
- **WHEN** the user taps the "Short" toggle button
- **THEN** "Short (down)" gets red background with white text, "Long (up)" gets surface-light background with text-muted, and the CTA and summary update accordingly

### Requirement: Amount input with quick-select chips
The TradeScreen SHALL render an amount section (mt-4, mx-4) with an "Amount" label in text-xs text-secondary. The input SHALL have surface-light background, a "$" prefix, text-right alignment, text-lg font size, and default value "50.00". Below the input, three quick-select chips ("$25", "$50", "$100") SHALL render as rounded-full pills. The active chip (matching the current amount) SHALL have an accent border (#7B61FF). Tapping a chip SHALL set the amount to that value.

#### Scenario: Default amount is $50
- **WHEN** the TradeScreen renders
- **THEN** the amount input shows "50.00" and the "$50" chip has accent border

#### Scenario: User taps $100 chip
- **WHEN** the user taps the "$100" quick-select chip
- **THEN** the input value changes to "100.00", the "$100" chip gets accent border, and the "$50" chip loses its accent border

#### Scenario: User types a custom amount
- **WHEN** the user types "75" in the amount input
- **THEN** the input shows "75", no quick-select chip has accent border, and the summary updates

### Requirement: LeverageSlider renders with default 10x
The TradeScreen SHALL render a LeverageSlider component (mt-4, mx-4) with a default value of 10x. The slider SHALL allow values from 2x to 100x. Changing the leverage SHALL update the summary section dynamically.

#### Scenario: Default leverage is 10x
- **WHEN** the TradeScreen renders
- **THEN** the LeverageSlider shows 10x with green track fill

#### Scenario: User adjusts leverage to 50x
- **WHEN** the user drags the slider to 50x
- **THEN** the leverage label shows "50x" in red, a warning appears, and the summary updates with the new position size and liquidation price

### Requirement: Summary section displays computed values
The TradeScreen SHALL render a summary section (mt-4, mx-4) with three rows in text-sm: "Position size" showing amount × leverage (e.g., "$500.00"), "Liquidation price" showing a mock calculation, and "Fee" showing 0.05% of position size. For Long positions, liquidation price SHALL be entry price − (entry price / leverage). For Short positions, liquidation price SHALL be entry price + (entry price / leverage). All values SHALL update dynamically when amount, leverage, or direction changes.

#### Scenario: Default summary with Long $50 at 10x
- **WHEN** the TradeScreen renders with default values (Long, $50, 10x, BTC at $67,156)
- **THEN** "Position size" shows "$500.00", "Liquidation price" shows "$60,440.40", and "Fee" shows "$0.25"

#### Scenario: Summary updates when leverage changes
- **WHEN** the user changes leverage from 10x to 20x
- **THEN** "Position size" updates to "$1,000.00", "Liquidation price" updates, and "Fee" updates to "$0.50"

#### Scenario: Summary updates when direction is Short
- **WHEN** the user selects Short direction
- **THEN** "Liquidation price" recalculates using entry price + (entry price / leverage) instead of minus

### Requirement: CTA button shows dynamic order description
The TradeScreen SHALL render a full-width CTA button (mt-4, mx-4, h-14, rounded-xl) with dynamic text on two lines: "Open Long $500 BTC at $67,156" (or Short equivalent). The background SHALL be green (#00D68F) for Long and red (#FF4757) for Short. The text SHALL update when amount, leverage, pair, or direction changes. The button SHALL be disabled (opacity-50) when the amount is 0 or empty.

#### Scenario: Default CTA for Long
- **WHEN** the TradeScreen renders with default values (Long, $50, 10x, BTC/USD)
- **THEN** the CTA shows "Open Long $500 BTC at $67,156" on green background

#### Scenario: CTA updates for Short at $100 and 20x
- **WHEN** direction is Short, amount is $100, leverage is 20x
- **THEN** the CTA shows "Open Short $2,000 BTC at $67,156" on red background

#### Scenario: CTA disabled when amount is 0
- **WHEN** the user clears the amount input
- **THEN** the CTA button has opacity-50 and is not tappable

### Requirement: Tapping CTA opens trade confirmation overlay
Tapping the CTA button SHALL call `store.showOverlay('trade-confirmation')`.

#### Scenario: User taps CTA
- **WHEN** the user taps the CTA button with a valid amount
- **THEN** `store.showOverlay('trade-confirmation')` is called and the trade-confirmation overlay appears

### Requirement: Number values animate with Framer Motion
All dynamic number values (position size, liquidation price, fee, leverage label, CTA text amounts) SHALL animate transitions using Framer Motion when they change. Animations SHALL be 200-300ms duration.

#### Scenario: Position size animates on leverage change
- **WHEN** the user changes leverage from 10x to 20x
- **THEN** the position size value transitions smoothly from "$500.00" to "$1,000.00"

### Requirement: BottomNav shows Trade as active tab
When the TradeScreen is displayed, the BottomNav SHALL render with Trade as the active tab (accent color).

#### Scenario: Trade tab is active
- **WHEN** the current screen is 'trade'
- **THEN** the Trade tab in BottomNav uses accent color and other tabs use text-muted

### Requirement: TradeScreen is scrollable with bottom nav clearance
The TradeScreen layout SHALL be scrollable with px-0 (sections use mx-4 individually), pt-2, and pb-24 to provide clearance for the fixed BottomNav.

#### Scenario: Content scrolls behind bottom nav
- **WHEN** the TradeScreen content exceeds the viewport height
- **THEN** the user can scroll and the bottom padding prevents content from being hidden behind BottomNav
