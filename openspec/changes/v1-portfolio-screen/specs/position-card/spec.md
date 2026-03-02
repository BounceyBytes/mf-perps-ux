## ADDED Requirements

### Requirement: PositionCard displays pair, direction, and leverage
The PositionCard SHALL render a top row showing "{pair} {direction} {leverage}x" where direction is colored green (#00D68F) for Long and red (#FF4757) for Short.

#### Scenario: Long position header
- **WHEN** PositionCard renders with pair="BTC/USD", direction="Long", leverage=10
- **THEN** "BTC/USD Long 10x" appears with "Long" in green

#### Scenario: Short position header
- **WHEN** PositionCard renders with pair="ETH/USD", direction="Short", leverage=5
- **THEN** "ETH/USD Short 5x" appears with "Short" in red

### Requirement: PositionCard displays P&L with color coding
The PositionCard SHALL display P&L in text-lg font-bold, formatted as "+$12.80 (+2.56%)" with green color for positive and red for negative values.

#### Scenario: Positive P&L display
- **WHEN** a position has pnl=+12.80 and pnlPercent=+2.56
- **THEN** "+$12.80 (+2.56%)" renders in text-lg font-bold green

#### Scenario: Negative P&L display
- **WHEN** a position has pnl=-8.50 and pnlPercent=-1.70
- **THEN** "-$8.50 (-1.70%)" renders in text-lg font-bold red

### Requirement: PositionCard displays value progression
The PositionCard SHALL display the position value progression in text-sm text-secondary, formatted as "$500 → $512.80" showing entry value to current value.

#### Scenario: Value progression renders
- **WHEN** a position has entryValue=500 and currentValue=512.80
- **THEN** "$500 → $512.80" appears in text-sm text-secondary

### Requirement: PositionCard displays health bar with liquidation distance
The PositionCard SHALL render a HealthBar with a track (h-1.5, rounded), a fill whose width equals the health percentage, and a label showing "{N}% to liq". The fill and label color SHALL be green (#00D68F) when health > 60%, yellow (#FFD93D — see design tokens) when 30-60%, and red (#FF4757) when < 30%.

#### Scenario: Healthy position (above 60%)
- **WHEN** a position has health=75
- **THEN** the health bar fill is 75% wide in green and label reads "75% to liq" in green

#### Scenario: Caution position (30-60%)
- **WHEN** a position has health=45
- **THEN** the health bar fill is 45% wide in yellow (#FFD93D) and label reads "45% to liq" in yellow

#### Scenario: Danger position (below 30%)
- **WHEN** a position has health=20
- **THEN** the health bar fill is 20% wide in red and label reads "20% to liq" in red

### Requirement: PositionCard has a close button
The PositionCard SHALL render a right-aligned "Close" button with surface-light background and rounded-lg styling. Tapping it SHALL call `showOverlay('close-position')`.

#### Scenario: User taps Close button
- **WHEN** the user taps "Close" on a PositionCard
- **THEN** `showOverlay('close-position')` is called

### Requirement: PositionCard has a colored left border
The PositionCard SHALL have a 3px left border: green (#00D68F) for Long positions and red (#FF4757) for Short positions.

#### Scenario: Long position border
- **WHEN** a PositionCard renders for a Long position
- **THEN** a 3px green left border is visible

#### Scenario: Short position border
- **WHEN** a PositionCard renders for a Short position
- **THEN** a 3px red left border is visible
