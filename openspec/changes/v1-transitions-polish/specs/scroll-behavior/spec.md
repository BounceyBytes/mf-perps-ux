## ADDED Requirements

### Requirement: PhoneFrame has overscroll-behavior contain
The PhoneFrame component's scrollable container SHALL have `overscroll-behavior: contain` to prevent scroll chaining from the phone frame to the outer browser page.

#### Scenario: User scrolls past content boundary
- **WHEN** the user scrolls past the top or bottom of the phone frame content
- **THEN** the scroll does not propagate to the outer browser page

### Requirement: PhoneFrame has webkit overflow scrolling touch
The PhoneFrame component's scrollable container SHALL have `-webkit-overflow-scrolling: touch` for momentum-based scrolling on iOS Safari.

#### Scenario: User flick-scrolls on iOS
- **WHEN** the user performs a flick scroll gesture inside the phone frame on an iOS device
- **THEN** the content scrolls with momentum (inertia) rather than stopping immediately
