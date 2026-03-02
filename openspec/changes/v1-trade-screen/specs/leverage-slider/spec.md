## ADDED Requirements

### Requirement: LeverageSlider renders a range slider from 2x to 100x
The LeverageSlider component SHALL accept `value` and `onChange` props and render a horizontal range slider with minimum 2 and maximum 100. The track SHALL be h-2 with rounded-full styling. A white thumb (w-6 h-6) SHALL indicate the current position. "2x" SHALL appear on the left and "100x" on the right in text-xs text-muted.

#### Scenario: Slider renders at default value
- **WHEN** LeverageSlider renders with value=10
- **THEN** the thumb is positioned at 10 on a 2–100 range, "2x" appears left, "100x" appears right, and a "10x" label appears above the thumb

#### Scenario: User drags slider to 50x
- **WHEN** the user drags the slider thumb to the 50 position
- **THEN** `onChange` is called with 50, the thumb moves to the 50 position, and the label updates to "50x"

### Requirement: Track fill color indicates risk level
The LeverageSlider track fill SHALL be color-coded based on the current value: green (#00D68F) for 2-25x, yellow (#FFD93D — see design tokens) for 25-50x, red (#FF4757) for 50-100x. The unfilled portion of the track SHALL use surface-light (#1E1E2E) background.

#### Scenario: Leverage at 10x shows green fill
- **WHEN** LeverageSlider renders with value=10
- **THEN** the filled portion of the track is green (#00D68F)

#### Scenario: Leverage at 35x shows yellow fill
- **WHEN** LeverageSlider renders with value=35
- **THEN** the filled portion of the track is yellow (#FFD93D)

#### Scenario: Leverage at 75x shows red fill
- **WHEN** LeverageSlider renders with value=75
- **THEN** the filled portion of the track is red (#FF4757)

### Requirement: Dynamic label above thumb matches risk color
The LeverageSlider SHALL display a label above the slider showing the current value (e.g., "10x"). The label text color SHALL match the track fill color for the current risk level.

#### Scenario: Label color matches track at 10x
- **WHEN** LeverageSlider renders with value=10
- **THEN** the label "10x" is displayed in green (#00D68F)

#### Scenario: Label color matches track at 60x
- **WHEN** LeverageSlider renders with value=60
- **THEN** the label "60x" is displayed in red (#FF4757)

### Requirement: Warning text appears when leverage exceeds 25x
The LeverageSlider SHALL display a warning message below the slider when the value exceeds 25. The warning text SHALL use text-xs styling and match the current risk color. The warning text SHALL read "High leverage increases liquidation risk" for values 26-50, and "Extreme leverage — high liquidation risk" for values above 50.

#### Scenario: No warning at 20x
- **WHEN** LeverageSlider renders with value=20
- **THEN** no warning text is displayed below the slider

#### Scenario: Yellow warning at 30x
- **WHEN** LeverageSlider renders with value=30
- **THEN** "High leverage increases liquidation risk" appears below the slider in yellow (#FFD93D) text-xs

#### Scenario: Red warning at 75x
- **WHEN** LeverageSlider renders with value=75
- **THEN** "Extreme leverage — high liquidation risk" appears below the slider in red (#FF4757) text-xs
