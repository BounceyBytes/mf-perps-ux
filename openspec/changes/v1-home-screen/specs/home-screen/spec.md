## ADDED Requirements

### Requirement: Header displays hamburger icon, brand name, and balance
The HomeScreen SHALL render a header row with a hamburger Menu icon on the left, "MF Perps" in text-lg font-bold centered, and the user balance "$648.50" in text-sm font-semibold on the right. The balance SHALL be tappable.

#### Scenario: Header renders correctly
- **WHEN** the HomeScreen renders
- **THEN** a Menu icon appears left, "MF Perps" appears centered in text-lg font-bold, and "$648.50" appears on the right in text-sm font-semibold

### Requirement: Tapping balance navigates to portfolio
Tapping the balance text in the header SHALL call `store.navigate('portfolio')`.

#### Scenario: User taps balance
- **WHEN** the user taps "$648.50" in the header
- **THEN** the app navigates to the 'portfolio' screen

### Requirement: Trending section shows top 3 markets by change percentage
The HomeScreen SHALL render a "🔥 Trending" section with a text-xs uppercase tracking-wider text-muted header, followed by 3 MarketRow components displaying the top 3 markets sorted by absolute 24h change percentage (descending).

#### Scenario: Trending section renders top 3
- **WHEN** the HomeScreen renders
- **THEN** a "🔥 Trending" header appears with 3 MarketRows showing the markets with the highest absolute change percentages from mock data

### Requirement: Watchlist section shows BTC and ETH with add row
The HomeScreen SHALL render a "Your Watchlist" section with a text-xs uppercase tracking-wider text-muted header, MarketRows for BTC/USD and ETH/USD, and a "+ Add market" row styled with a Plus icon in accent color (#7B61FF) and text-sm text-accent.

#### Scenario: Watchlist renders BTC and ETH
- **WHEN** the HomeScreen renders
- **THEN** "Your Watchlist" header appears followed by MarketRow for BTC/USD, MarketRow for ETH/USD, and a "+ Add market" row in accent color

#### Scenario: Add market row is decorative
- **WHEN** the user taps "+ Add market"
- **THEN** nothing happens (no functionality in v1)

### Requirement: Top Movers section shows horizontal scrollable cards
The HomeScreen SHALL render a "Top Movers" section with a text-xs uppercase tracking-wider text-muted header, followed by a horizontal scrollable row of small cards (w-24, surface background, rounded-xl, p-3). Each card SHALL display the pair name in text-xs font-semibold and the change percentage in text-sm with green/red coloring.

#### Scenario: Top Movers cards scroll horizontally
- **WHEN** the HomeScreen renders
- **THEN** a horizontally scrollable row of market cards appears, each w-24 with surface bg, showing pair name and colored change percentage

#### Scenario: Top Movers card taps navigate to trade
- **WHEN** the user taps a Top Movers card
- **THEN** `store.selectedPair` is set to that card's pair and the app navigates to 'trade'

### Requirement: HomeScreen is scrollable with bottom nav clearance
The HomeScreen layout SHALL be scrollable with px-4, pt-2, and pb-24 to provide clearance for the fixed BottomNav.

#### Scenario: Content scrolls behind bottom nav
- **WHEN** the HomeScreen content exceeds the viewport height
- **THEN** the user can scroll and the bottom padding prevents content from being hidden behind BottomNav

### Requirement: BottomNav shows Home as active tab
When the HomeScreen is displayed, the BottomNav SHALL render with Home as the active tab (accent color).

#### Scenario: Home tab is active
- **WHEN** the current screen is 'home'
- **THEN** the Home tab in BottomNav uses accent color and other tabs use text-muted

### Requirement: Sections use consistent header styling
All section headers ("🔥 Trending", "Your Watchlist", "Top Movers") SHALL use text-xs uppercase tracking-wider text-muted styling with mt-4 spacing above.

#### Scenario: Section headers are styled consistently
- **WHEN** the HomeScreen renders
- **THEN** all three section headers appear in text-xs uppercase tracking-wider text-muted with mt-4 top margin
