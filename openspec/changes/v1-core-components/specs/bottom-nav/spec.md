## ADDED Requirements

### Requirement: BottomNav displays three tabs
The BottomNav component SHALL render three tabs: Home (House icon), Trade (TrendingUp icon), Portfolio (Wallet icon), with labels below icons in text-xs. It SHALL use surface bg with a top border, fixed at the bottom of the phone frame.

#### Scenario: Three tabs visible
- **WHEN** BottomNav renders
- **THEN** Home, Trade, and Portfolio tabs are visible with icons and labels

### Requirement: Active tab is highlighted
The BottomNav SHALL highlight the active tab using the accent color (`#7B61FF`). Inactive tabs use text-muted color.

#### Scenario: Trade tab is active
- **WHEN** the current screen is 'trade'
- **THEN** the Trade tab icon and label use accent color, others use text-muted

### Requirement: Tab tap navigates to screen
Tapping a BottomNav tab SHALL call the store's `navigate()` function with the corresponding screen: Home → 'home', Trade → 'trade', Portfolio → 'portfolio'.

#### Scenario: User taps Portfolio tab
- **WHEN** user taps the Portfolio tab
- **THEN** `navigate('portfolio')` is called and the Portfolio screen renders

### Requirement: BottomNav only shows on main screens
The BottomNav SHALL only render when the current screen is 'home', 'trade', or 'portfolio'. It SHALL be hidden during onboarding and modal screens.

#### Scenario: BottomNav hidden during onboarding
- **WHEN** the current screen is 'welcome', 'kyc', 'referral', or 'youre-in'
- **THEN** the BottomNav is not rendered
