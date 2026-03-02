## ADDED Requirements

### Requirement: Header displays back arrow and centered title
The WithdrawScreen SHALL render a header with a back arrow (ArrowLeft icon) on the left and "Withdraw" centered in text-lg font-semibold. The screen SHALL use px-6 pt-4 padding.

#### Scenario: Header renders with title
- **WHEN** the WithdrawScreen renders
- **THEN** a back arrow appears on the left and "Withdraw" appears centered in text-lg font-semibold

#### Scenario: Back arrow navigates to portfolio
- **WHEN** the user taps the back arrow
- **THEN** the app navigates to the 'portfolio' screen

### Requirement: Available balance is displayed centered below header
The WithdrawScreen SHALL render the available balance as "Available: $512.80" in text-sm text-secondary, centered, with mt-2 margin.

#### Scenario: Available balance renders
- **WHEN** the WithdrawScreen renders
- **THEN** "Available: $512.80" appears centered below the header in text-sm text-secondary

### Requirement: Large amount display shows current withdraw amount
The WithdrawScreen SHALL render the current withdraw amount in text-4xl font-bold text-primary, centered, with mt-4 margin. The amount SHALL be pre-filled with the max available balance ($512.80) on initial render.

#### Scenario: Amount display renders pre-filled with max
- **WHEN** the WithdrawScreen mounts
- **THEN** "$512.80" appears centered in text-4xl font-bold text-primary

#### Scenario: Amount updates when chip is selected
- **WHEN** the user taps a quick-select chip
- **THEN** the large amount display updates to reflect the calculated value

### Requirement: Quick-select percentage chips with Max active by default
The WithdrawScreen SHALL render three quick-select chips ("25%", "50%", "Max") as rounded-full pills, centered with mt-3 margin and gap between chips. "Max" SHALL be active by default with an accent border (#7B61FF). Tapping a chip SHALL recalculate the amount as a percentage of the available balance.

#### Scenario: Chips render with Max active
- **WHEN** the WithdrawScreen renders
- **THEN** three chips ("25%", "50%", "Max") appear centered, with "Max" having an accent border and the others having a default/muted style

#### Scenario: User taps 25% chip
- **WHEN** the user taps the "25%" chip
- **THEN** the amount updates to "$128.20" (25% of $512.80), the "25%" chip gets the accent border, and the other chips lose the accent border

#### Scenario: User taps 50% chip
- **WHEN** the user taps the "50%" chip
- **THEN** the amount updates to "$256.40" (50% of $512.80), the "50%" chip gets the accent border, and the other chips lose the accent border

#### Scenario: User taps Max chip
- **WHEN** the user taps the "Max" chip
- **THEN** the amount updates to "$512.80" (100% of available balance), the "Max" chip gets the accent border, and the other chips lose the accent border

### Requirement: "Withdraw to:" label renders above destination card
The WithdrawScreen SHALL render a label "Withdraw to:" in text-xs uppercase tracking-wider text-muted with mt-6 margin.

#### Scenario: Label renders
- **WHEN** the WithdrawScreen renders
- **THEN** "WITHDRAW TO:" appears in text-xs uppercase tracking-wider text-muted above the destination card

### Requirement: External Wallet destination card renders with accent border and checkmark
The WithdrawScreen SHALL render a single destination card with mt-2 margin containing: a Wallet icon on the left, "External Wallet" as the name, "Paste or select wallet address" in text-xs text-secondary below the name, "Instant" in text-xs text-muted, and a checkmark icon on the right. The card SHALL have an accent border (#7B61FF).

#### Scenario: Wallet card renders
- **WHEN** the WithdrawScreen renders
- **THEN** a card appears with Wallet icon, "External Wallet" title, "Paste or select wallet address" subtitle, "Instant" label, accent border, and a checkmark on the right

### Requirement: Tapping wallet card expands address input section
Tapping the External Wallet card SHALL toggle an expanded section with AnimatePresence containing: a text input field for wallet address with a paste button, and a "Confirm Withdraw" primary button below the input. The section SHALL animate in from collapsed (height 0, opacity 0) to expanded.

#### Scenario: User taps wallet card to expand
- **WHEN** the user taps the External Wallet card
- **THEN** an address input section animates in below the card with a text field (placeholder: "Enter wallet address"), a paste button, and a "Confirm Withdraw" primary button

#### Scenario: User taps wallet card again to collapse
- **WHEN** the address input section is visible and the user taps the wallet card
- **THEN** the address input section animates out via AnimatePresence

#### Scenario: No separate bottom CTA exists
- **WHEN** the WithdrawScreen renders
- **THEN** there is no fixed bottom CTA button — the "Confirm Withdraw" button only appears inside the expanded wallet card section

### Requirement: Paste button populates address field
The paste button next to the address input SHALL simulate pasting a wallet address into the text field. In the prototype, tapping paste SHALL populate the field with a mock address (e.g., "0x1a2B...9fEd").

#### Scenario: User taps paste button
- **WHEN** the user taps the paste button next to the address input
- **THEN** the text field is populated with a mock wallet address such as "0x1a2B3c4D5e6F7a8B9c0D1e2F3a4B5c6D7e8F9a"

### Requirement: Confirm Withdraw triggers loading and navigation with toast
Tapping "Confirm Withdraw" SHALL show a loading spinner on the button for 1.5 seconds, then navigate to the 'portfolio' screen and display a success toast "Withdrawal initiated — $X.XX" where $X.XX is the current withdraw amount.

#### Scenario: User taps Confirm Withdraw
- **WHEN** the user taps "Confirm Withdraw" with amount $512.80
- **THEN** the button shows a loading spinner for 1.5 seconds, then the app navigates to 'portfolio' and a toast "Withdrawal initiated — $512.80" appears

#### Scenario: User taps Confirm Withdraw with partial amount
- **WHEN** the user selected 25% chip and taps "Confirm Withdraw" with amount $128.20
- **THEN** the button shows a loading spinner for 1.5 seconds, then the app navigates to 'portfolio' and a toast "Withdrawal initiated — $128.20" appears

### Requirement: No BottomNav on WithdrawScreen
The BottomNav component SHALL NOT render when the current screen is 'withdraw'.

#### Scenario: BottomNav is hidden
- **WHEN** the current screen is 'withdraw'
- **THEN** the BottomNav is not visible
