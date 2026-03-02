## ADDED Requirements

### Requirement: MarketRow displays pair, price, and change percentage
The MarketRow component SHALL accept `pair`, `price`, and `change24h` props and render them in a horizontal layout: pair name (text-sm font-semibold) on the left, price (text-sm tabular-nums) right-aligned, change percentage (text-sm) with green color (#00D68F) for positive values and red color (#FF4757) for negative values, and a ChevronRight icon in text-muted on the far right. Positive change values SHALL display a "+" prefix.

#### Scenario: Positive change market
- **WHEN** MarketRow renders with pair="SOL/USD", price="$142.80", change24h=8.4
- **THEN** "SOL/USD" appears left in text-sm font-semibold, "$142.80" right-aligned in tabular-nums, "+8.4%" in green, and a ChevronRight icon

#### Scenario: Negative change market
- **WHEN** MarketRow renders with pair="DOGE/USD", price="$0.142", change24h=-3.2
- **THEN** the change text shows "-3.2%" in red (#FF4757)

### Requirement: MarketRow has a bottom border
The MarketRow SHALL render a subtle bottom border separating it from the next row.

#### Scenario: Border between rows
- **WHEN** multiple MarketRows render in a list
- **THEN** each row has a bottom border in the border color (#2A2A3A)

### Requirement: Tapping MarketRow navigates to trade screen
Tapping a MarketRow SHALL set `store.selectedPair` to the row's pair value and call `store.navigate('trade')`.

#### Scenario: User taps BTC/USD row
- **WHEN** the user taps the BTC/USD MarketRow
- **THEN** `store.selectedPair` becomes 'BTC/USD' and the app navigates to the 'trade' screen
