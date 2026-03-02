## ADDED Requirements

### Requirement: Store manages screen navigation
The Zustand store SHALL expose a `screen` state (union of all screen names: 'welcome', 'kyc', 'youre-in', 'home', 'deposit', 'deposit-amount', 'trade', 'portfolio', 'withdraw') defaulting to 'welcome', and a `navigate(screen)` function to change it. The 'referral' screen is deferred to V3 — see [plan-v3-referral-program.md](../../plan-v3-referral-program.md).

#### Scenario: Navigate from welcome to kyc
- **WHEN** `navigate('kyc')` is called
- **THEN** `store.screen` becomes 'kyc'

### Requirement: Store manages overlay state
The Zustand store SHALL expose an `overlay` state (null | 'trade-confirmation' | 'close-position' | 'share-card') defaulting to null, with `showOverlay(overlay)` and `dismissOverlay()` functions.

#### Scenario: Show trade confirmation overlay
- **WHEN** `showOverlay('trade-confirmation')` is called
- **THEN** `store.overlay` becomes 'trade-confirmation'

#### Scenario: Dismiss overlay
- **WHEN** `dismissOverlay()` is called
- **THEN** `store.overlay` becomes null

### Requirement: Store tracks selected trading pair
The Zustand store SHALL expose a `selectedPair` state defaulting to 'BTC/USD' and a way to update it when selecting a market.

#### Scenario: Select ETH/USD pair
- **WHEN** user selects ETH/USD from a market list
- **THEN** `store.selectedPair` becomes 'ETH/USD'

### Requirement: Mock data provides markets, positions, and user
The `mock-data.ts` file SHALL export `markets` (array of 7 pairs with price and 24h change), `openPositions` (2 positions with P&L, leverage, health), and `user` (name, balance, available, referral code, referral count, referral earnings).

#### Scenario: Import markets mock data
- **WHEN** a component imports `markets` from `src/lib/mock-data`
- **THEN** an array of 7 market objects is available with pair, price, and change24h fields
