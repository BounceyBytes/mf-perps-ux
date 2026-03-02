## ADDED Requirements

### Requirement: NumPad renders a 4×3 button grid
The NumPad component SHALL render a 4-row, 3-column grid of buttons. Row 1: 1, 2, 3. Row 2: 4, 5, 6. Row 3: 7, 8, 9. Row 4: ".", 0, ⌫ (backspace icon). Each button SHALL be w-16 h-16 rounded-full with surface-light background and text-xl text.

#### Scenario: NumPad grid renders all buttons
- **WHEN** the NumPad component renders
- **THEN** 12 buttons are displayed in a 4×3 grid: digits 1-9, decimal point, 0, and backspace

#### Scenario: Button styling
- **WHEN** the NumPad renders
- **THEN** each button is w-16 h-16 rounded-full with surface-light background (#1E1E2E) and text-xl white text

### Requirement: Digit buttons call onDigit callback
Tapping a digit button (0-9) SHALL call the `onDigit` callback with the tapped digit as a string.

#### Scenario: User taps digit 5
- **WHEN** the user taps the "5" button
- **THEN** `onDigit("5")` is called

#### Scenario: User taps digit 0
- **WHEN** the user taps the "0" button
- **THEN** `onDigit("0")` is called

### Requirement: Decimal button calls onDecimal callback
Tapping the "." button SHALL call the `onDecimal` callback.

#### Scenario: User taps decimal
- **WHEN** the user taps the "." button
- **THEN** `onDecimal()` is called

### Requirement: Backspace button calls onBackspace callback
Tapping the ⌫ button SHALL call the `onBackspace` callback.

#### Scenario: User taps backspace
- **WHEN** the user taps the ⌫ button
- **THEN** `onBackspace()` is called

### Requirement: Buttons have press animation
All NumPad buttons SHALL animate to scale 0.9 on press using Framer Motion whileTap.

#### Scenario: User presses and holds a digit button
- **WHEN** the user presses and holds any NumPad button
- **THEN** the button scales to 0.9 while pressed and returns to 1.0 on release

### Requirement: NumPad enforces max 2 decimal places
The parent component using NumPad SHALL enforce a maximum of 2 decimal places. The NumPad itself SHALL call callbacks for all taps, and the parent SHALL ignore digits that would exceed 2 decimal places.

#### Scenario: User enters third decimal digit
- **WHEN** the current amount is "150.50" and the user taps "5"
- **THEN** the amount remains "150.50" (the parent ignores the digit because 2 decimal places are already present)

### Requirement: NumPad prevents multiple decimal points
The parent component using NumPad SHALL prevent multiple decimal points. If the current value already contains a decimal, tapping "." SHALL have no effect.

#### Scenario: User taps decimal when one already exists
- **WHEN** the current amount is "150.5" and the user taps "."
- **THEN** the amount remains "150.5" (the decimal tap is ignored)

### Requirement: NumPad layout is centered with mt-4
The NumPad grid SHALL be centered horizontally within its container and have mt-4 top margin. The grid SHALL have consistent gap spacing between buttons.

#### Scenario: NumPad is centered
- **WHEN** the NumPad renders within DepositAmountScreen
- **THEN** the 4×3 grid is centered horizontally with mt-4 margin above it
