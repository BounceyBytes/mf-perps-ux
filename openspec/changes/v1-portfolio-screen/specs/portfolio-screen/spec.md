## ADDED Requirements

### Requirement: Header displays portfolio title, total value, and P&L
The PortfolioScreen SHALL render a header with "Portfolio" in text-lg font-bold on the left, and the total portfolio value "$648.50" in text-2xl font-bold on the right with P&L "+$12.30" in text-sm green (#00D68F) beneath the value.

#### Scenario: Header renders with positive P&L
- **WHEN** the PortfolioScreen renders with positive total P&L
- **THEN** "Portfolio" appears left in text-lg font-bold, "$648.50" appears right in text-2xl font-bold, and "+$12.30" appears below it in text-sm green

#### Scenario: Header renders with negative P&L
- **WHEN** the total P&L is negative
- **THEN** the P&L value displays in red (#FF4757) with a "-" prefix

### Requirement: Portfolio value area chart renders with dynamic fill color
The PortfolioScreen SHALL render an area chart component approximately 140px tall. The chart fill SHALL be green (#00D68F) when total P&L is positive and red (#FF4757) when negative. A dashed horizontal line SHALL indicate the break-even level.

#### Scenario: Chart renders green for positive P&L
- **WHEN** the portfolio has positive total P&L
- **THEN** the area chart renders with green fill and a dashed break-even line

#### Scenario: Chart renders red for negative P&L
- **WHEN** the portfolio has negative total P&L
- **THEN** the area chart renders with red fill and a dashed break-even line

### Requirement: Time-range pills filter chart display
The chart SHALL display time-range pills: 1D, 1W, 1M, 3M, ALL. The 1M pill SHALL be active by default. Tapping a pill SHALL update the active state visually.

#### Scenario: Default time range is 1M
- **WHEN** the PortfolioScreen renders
- **THEN** the 1M pill is visually active (accent background or border)

#### Scenario: User switches time range
- **WHEN** the user taps the 1W pill
- **THEN** the 1W pill becomes active and the previously active pill becomes inactive

### Requirement: Touch scrub updates header values
When the user drags across the chart area, the header total value and P&L SHALL update to reflect the scrubbed position's values.

#### Scenario: User scrubs chart
- **WHEN** the user touches and drags across the chart
- **THEN** the header total and P&L values update dynamically to reflect the point being scrubbed

### Requirement: Open Positions section header displays count
The PortfolioScreen SHALL render an "Open Positions (2)" section header in text-xs uppercase tracking-wider text-muted below the chart.

#### Scenario: Open positions header renders
- **WHEN** the PortfolioScreen renders with 2 open positions
- **THEN** "Open Positions (2)" appears as a section header in text-xs uppercase tracking-wider text-muted

### Requirement: PositionCards render in a stacked list
The PortfolioScreen SHALL render PositionCard components for each open position, stacked vertically with gap-3 spacing.

#### Scenario: Two position cards render
- **WHEN** mock data contains 2 open positions
- **THEN** 2 PositionCard components render stacked with gap-3

### Requirement: Available balance displays with Fund Account link
The PortfolioScreen SHALL display the available balance "$48.50" with a "Fund Account" link in accent color (#7B61FF). Tapping "Fund Account" SHALL call `store.navigate('deposit')`.

#### Scenario: Available balance renders
- **WHEN** the PortfolioScreen renders
- **THEN** "Available" label and "$48.50" value are displayed with a "Fund Account" accent link

#### Scenario: User taps Fund Account link
- **WHEN** the user taps "Fund Account"
- **THEN** the app navigates to the 'deposit' screen

### Requirement: Yield teaser card renders with gradient border
The PortfolioScreen SHALL render a yield teaser card with a gradient border (accent #7B61FF → green #00D68F). The card SHALL display "Earn up to 8.2% target APY (variable)..." with a TrendingUp icon in green, a "Learn More →" link in accent color, and "Not guaranteed." in text-xs text-muted as a disclaimer.

#### Scenario: Yield teaser renders
- **WHEN** the PortfolioScreen renders
- **THEN** a card with gradient border appears containing the APY text, TrendingUp icon in green, "Learn More →" in accent, and "Not guaranteed." disclaimer

### Requirement: History section shows closed positions
The PortfolioScreen SHALL render a "History" section with closed position rows. Each row SHALL display the pair, direction, "Closed" label, P&L value (green for profit, red for loss), and a relative timestamp.

#### Scenario: Closed positions render in history
- **WHEN** the PortfolioScreen renders
- **THEN** the History section shows "SOL Long — Closed" with "+$45.00" in green and "2 hours ago", and "DOGE Short — Closed" with "-$12.00" in red and "Yesterday"

### Requirement: P&L numbers animate on mount
All P&L dollar and percentage values on the PortfolioScreen SHALL animate from 0 to their final value on mount using Framer Motion count-up animation.

#### Scenario: P&L values count up on mount
- **WHEN** the PortfolioScreen mounts
- **THEN** the header P&L, position card P&L values, and history P&L values animate from 0 to their final numbers

### Requirement: PortfolioScreen is scrollable with bottom nav clearance
The PortfolioScreen layout SHALL be scrollable with px-4, pt-2, and pb-24 to provide clearance for the fixed BottomNav.

#### Scenario: Content scrolls behind bottom nav
- **WHEN** the PortfolioScreen content exceeds the viewport height
- **THEN** the user can scroll and the bottom padding prevents content from being hidden behind BottomNav

### Requirement: BottomNav shows Portfolio as active tab
When the PortfolioScreen is displayed, the BottomNav SHALL render with Portfolio as the active tab (accent color).

#### Scenario: Portfolio tab is active
- **WHEN** the current screen is 'portfolio'
- **THEN** the Portfolio tab in BottomNav uses accent color and other tabs use text-muted
