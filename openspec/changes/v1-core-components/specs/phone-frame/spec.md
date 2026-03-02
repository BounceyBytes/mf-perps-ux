## ADDED Requirements

### Requirement: PhoneFrame renders a centered device frame
The PhoneFrame component SHALL render a centered container with max-width 390px, height 844px, rounded corners (40px radius), subtle border (`#2A2A3A`), background matching app bg (`#0A0A0F`), and overflow-y auto with hidden scrollbar. The outer page background SHALL be `#1a1a1a`.

#### Scenario: Phone frame renders at correct dimensions
- **WHEN** the PhoneFrame component mounts
- **THEN** a 390×844px container is centered on the page with rounded corners and a dark border

### Requirement: StatusBar renders a fake iOS status bar
The StatusBar component SHALL render at the top of the PhoneFrame with time "9:41" on the left, and signal + wifi + battery icons on the right, in white text with small font, absolutely positioned with top padding.

#### Scenario: Status bar displays time and icons
- **WHEN** the PhoneFrame renders
- **THEN** a status bar showing "9:41" and system icons appears at the top of the frame
