## ADDED Requirements

### Requirement: Header displays back arrow and centered title
The DepositAmountScreen SHALL render a header with a back arrow (ArrowLeft icon) on the left and "Fund Account" centered in text-lg font-semibold. The back arrow SHALL navigate to 'deposit' when tapped.

#### Scenario: Header renders with title
- **WHEN** the DepositAmountScreen renders
- **THEN** a back arrow appears on the left and "Fund Account" appears centered in text-lg font-semibold

#### Scenario: Back arrow navigates to deposit
- **WHEN** the user taps the back arrow
- **THEN** the app navigates to the 'deposit' screen

### Requirement: Amount display shows current value
The DepositAmountScreen SHALL render a large amount display centered on screen with a "$" prefix in text-2xl text-secondary and the amount value in text-5xl font-bold tabular-nums. The initial display SHALL show "$0".

#### Scenario: Initial amount display
- **WHEN** the DepositAmountScreen renders
- **THEN** the display shows "$" in text-2xl text-secondary and "0" in text-5xl font-bold tabular-nums

#### Scenario: Amount updates on digit entry
- **WHEN** the user taps digits on the NumPad to enter "150"
- **THEN** the display updates to show "$150" in text-5xl font-bold

#### Scenario: Amount display shows decimals
- **WHEN** the user enters "150.50" via the NumPad
- **THEN** the display shows "$150.50" in text-5xl font-bold tabular-nums

### Requirement: Amount display animates on digit entry
The amount value SHALL perform a subtle scale-in animation each time a digit is entered. The animation SHALL scale from 1.0 to 1.05 and back to 1.0.

#### Scenario: Scale animation on digit tap
- **WHEN** the user taps a digit on the NumPad
- **THEN** the amount text briefly scales to 1.05 and returns to 1.0

### Requirement: Quick-select chips for common amounts
The DepositAmountScreen SHALL render three quick-select chips (mt-4, centered, gap-2): "$50", "$100", "$500" as rounded-full pills. The active chip (matching the current amount) SHALL have an accent border (#7B61FF). Tapping a chip SHALL set the amount to that value.

#### Scenario: No chip active at $0
- **WHEN** the DepositAmountScreen renders with initial amount $0
- **THEN** no quick-select chip has an accent border

#### Scenario: User taps $100 chip
- **WHEN** the user taps the "$100" chip
- **THEN** the amount display updates to "$100", the "$100" chip gets accent border, and any previously active chip loses its accent border

#### Scenario: Chip activates when amount matches via NumPad
- **WHEN** the user types "50" on the NumPad
- **THEN** the "$50" chip gets accent border

### Requirement: Fee breakdown displays computed values
The DepositAmountScreen SHALL render a fee breakdown section (mt-4) with two rows: "Fee" showing 1% of the entered amount, and "Buying power after fee" showing the amount minus the fee. Both values SHALL update dynamically as the amount changes.

#### Scenario: Fee breakdown at $100
- **WHEN** the amount is $100
- **THEN** "Fee" shows "$1.00" and "Buying power after fee" shows "$99.00"

#### Scenario: Fee breakdown at $0
- **WHEN** the amount is $0
- **THEN** "Fee" shows "$0.00" and "Buying power after fee" shows "$0.00"

#### Scenario: Fee breakdown at $500
- **WHEN** the amount is $500
- **THEN** "Fee" shows "$5.00" and "Buying power after fee" shows "$495.00"

### Requirement: CTA button shows dynamic text and is disabled at $0
The DepositAmountScreen SHALL render a full-width primary Button at the bottom with dynamic text "Fund $X.XX" reflecting the current amount. The button SHALL be disabled with opacity-50 when the amount is $0. The button text SHALL update as the amount changes.

#### Scenario: CTA disabled at $0
- **WHEN** the amount is $0
- **THEN** the CTA shows "Fund $0.00" with opacity-50 and is not tappable

#### Scenario: CTA enabled at $150
- **WHEN** the amount is $150
- **THEN** the CTA shows "Fund $150.00" with full opacity and is tappable

#### Scenario: CTA text updates dynamically
- **WHEN** the user changes the amount from $50 to $100
- **THEN** the CTA text updates from "Fund $50.00" to "Fund $100.00"

### Requirement: CTA triggers loading then navigates with toast
Tapping the CTA button SHALL show a loading state on the button for 1 second, then navigate to the 'home' screen and display a success toast "Account funded: +$X.XX" with the deposited amount.

#### Scenario: User taps CTA at $150
- **WHEN** the user taps the CTA with amount $150
- **THEN** the button shows a loading spinner for 1 second, then the app navigates to 'home' and a success toast "Account funded: +$150.00" appears

#### Scenario: User taps CTA at $50
- **WHEN** the user taps the CTA with amount $50
- **THEN** the button shows a loading spinner for 1 second, then the app navigates to 'home' and a success toast "Account funded: +$50.00" appears

### Requirement: Layout uses flex column with no BottomNav
The DepositAmountScreen SHALL use a flex column layout with px-6 padding. The BottomNav component SHALL NOT render when the current screen is 'deposit-amount'.

#### Scenario: Screen layout is flex column
- **WHEN** the DepositAmountScreen renders
- **THEN** the content is arranged in a vertical flex column with px-6 padding

#### Scenario: BottomNav is hidden
- **WHEN** the current screen is 'deposit-amount'
- **THEN** the BottomNav is not visible
