## ADDED Requirements

### Requirement: Toast component renders as a pill at the top of the phone frame
The Toast component SHALL render as a fixed-position pill at the top of the PhoneFrame, below the status bar, horizontally centered, with z-50. It SHALL have rounded-full corners, surface-light background, px-4 py-2 padding, and text-sm white text.

#### Scenario: Toast is visible when store.toast has a message
- **WHEN** store.toast is set to "Account funded: +$100.00"
- **THEN** a pill-shaped toast appears at the top of the phone frame displaying "Account funded: +$100.00"

#### Scenario: Toast is hidden when store.toast is null
- **WHEN** store.toast is null
- **THEN** no toast is rendered

### Requirement: Toast slides in from top with entrance animation
The Toast SHALL animate in from above: initial `{ y: -20, opacity: 0 }`, animate `{ y: 0, opacity: 1 }`, exit `{ y: -20, opacity: 0 }`, wrapped in AnimatePresence.

#### Scenario: Toast entrance animation
- **WHEN** a toast message is shown
- **THEN** the toast slides down from y: -20 to y: 0 with opacity fading in

#### Scenario: Toast exit animation
- **WHEN** the toast auto-dismisses
- **THEN** the toast slides up to y: -20 with opacity fading out

### Requirement: Toast has green left accent for success
The Toast pill SHALL have a green (#00D68F) left border or left accent bar to indicate success.

#### Scenario: Success accent renders
- **WHEN** a toast is visible
- **THEN** a green accent appears on the left side of the pill (e.g., border-l-2 border-green or a small green bar)

### Requirement: Toast auto-dismisses after 2.5 seconds
The `showToast(message)` action in the Zustand store SHALL set `store.toast` to the message string and schedule a setTimeout that clears `store.toast` to null after 2500ms.

#### Scenario: Toast auto-clears
- **WHEN** showToast("Position closed") is called
- **THEN** store.toast is set to "Position closed" and after 2500ms store.toast is set back to null

#### Scenario: Rapid successive toasts overwrite
- **WHEN** showToast("First") is called and then showToast("Second") is called 500ms later
- **THEN** the toast displays "Second" and auto-clears 2500ms after the second call
