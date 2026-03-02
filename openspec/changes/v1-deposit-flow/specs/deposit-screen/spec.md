## ADDED Requirements

### Requirement: Header displays back arrow and centered title
The DepositScreen SHALL render a header with a back arrow (ArrowLeft icon) on the left and "Fund Account" centered in text-lg font-semibold. The back arrow SHALL navigate to 'home' when tapped.

#### Scenario: Header renders with title
- **WHEN** the DepositScreen renders
- **THEN** a back arrow appears on the left and "Fund Account" appears centered in text-lg font-semibold

#### Scenario: Back arrow navigates to home
- **WHEN** the user taps the back arrow
- **THEN** the app navigates to the 'home' screen

### Requirement: Method cards are displayed
The DepositScreen SHALL render a method card in a vertical stack (mt-6, gap-3) within px-6 pt-4 padding. Each card SHALL be a Card component with a horizontal layout containing: a left icon, center text with method name and timing description, and a ChevronRight icon on the right. V1 supports Transfer Crypto only — fiat on-ramps (Debit Card, Apple Pay) are deferred to V5.

#### Scenario: Transfer Crypto method renders
- **WHEN** the DepositScreen renders
- **THEN** the card shows a Wallet icon (Lucide) on the left, "Transfer Crypto" as the name, "From another wallet" as the timing, and a ChevronRight on the right

### Requirement: Transfer Crypto opens bottom sheet
Tapping the "Transfer Crypto" card SHALL open a bottom sheet overlay containing a QR code placeholder and a mock wallet address for the user to copy.

#### Scenario: User taps Transfer Crypto
- **WHEN** the user taps the "Transfer Crypto" card
- **THEN** a bottom sheet appears with a QR code placeholder (gray rounded square) and a mock wallet address (e.g., "0x1a2B...9fEd") with a copy indicator

#### Scenario: User dismisses bottom sheet
- **WHEN** the user taps outside the bottom sheet or taps a close button
- **THEN** the bottom sheet closes and the DepositScreen is fully visible

### Requirement: Cards stagger in on mount
The method cards SHALL animate in on mount using Framer Motion stagger. Each card SHALL animate from opacity 0, y: 20 to opacity 1, y: 0, with a stagger delay between each card.

#### Scenario: Cards animate on mount
- **WHEN** the DepositScreen mounts
- **THEN** the method card(s) stagger in from below (opacity 0→1, y:20→0) with a delay between each card

### Requirement: No BottomNav on DepositScreen
The BottomNav component SHALL NOT render when the current screen is 'deposit'.

#### Scenario: BottomNav is hidden
- **WHEN** the current screen is 'deposit'
- **THEN** the BottomNav is not visible
