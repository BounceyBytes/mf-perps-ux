## ADDED Requirements

### Requirement: Page renders PhoneFrame with screen router
The `page.tsx` SHALL render a PhoneFrame containing a StatusBar at top, a content area that renders the current screen based on `store.screen`, and a BottomNav at the bottom (when applicable).

#### Scenario: App loads with welcome screen
- **WHEN** the app loads at the root URL
- **THEN** the PhoneFrame renders with StatusBar and the Welcome screen content, without BottomNav

### Requirement: Overlay renders on top of screen content
When `store.overlay` is set, the corresponding overlay component SHALL render on top of the current screen content within the PhoneFrame.

#### Scenario: Trade confirmation overlay appears
- **WHEN** `store.overlay` is 'trade-confirmation'
- **THEN** the TradeConfirmation component renders on top of the current screen

#### Scenario: No overlay when null
- **WHEN** `store.overlay` is null
- **THEN** no overlay component renders
