## ADDED Requirements

### Requirement: YoureInScreen renders check icon and heading
The YoureInScreen SHALL display a CheckCircle2 icon (from Lucide) in accent color (#7B61FF) at 64px size, centered horizontally. Below the icon, the screen SHALL display "You're all set" in text-2xl font-bold with mt-4, centered.

#### Scenario: Screen loads with confirmation content
- **WHEN** the YoureInScreen renders
- **THEN** a 64px CheckCircle2 icon in accent color is displayed centered, followed by "You're all set" heading in text-2xl font-bold

### Requirement: Two action buttons are displayed
The YoureInScreen SHALL render two full-width buttons with mt-8 and gap-3, inside a px-6 container: "Fund Account & Trade" (primary button with accent background) and "Explore Markets" (secondary button with surface-light background).

#### Scenario: Buttons are visible on mount
- **WHEN** the YoureInScreen renders
- **THEN** two full-width buttons are displayed: "Fund Account & Trade" (accent bg) and "Explore Markets" (surface-light bg)

### Requirement: Fund Account & Trade button navigates to deposit screen
The "Fund Account & Trade" button SHALL call `store.navigate('deposit')` when tapped.

#### Scenario: User taps Fund Account & Trade
- **WHEN** the user taps "Fund Account & Trade"
- **THEN** the app navigates to the 'deposit' screen

### Requirement: Explore Markets button navigates to home screen
The "Explore Markets" button SHALL call `store.navigate('home')` when tapped.

#### Scenario: User taps Explore Markets
- **WHEN** the user taps "Explore Markets"
- **THEN** the app navigates to the 'home' screen

### Requirement: Check icon has spring entrance animation
The CheckCircle2 icon SHALL animate from scale 0 to scale 1 on mount using a Framer Motion spring animation with type: "spring" and stiffness: 200.

#### Scenario: Check icon pops in on mount
- **WHEN** the YoureInScreen mounts
- **THEN** the CheckCircle2 icon animates from scale 0 to scale 1 with a spring animation (stiffness: 200)

### Requirement: Buttons stagger in from below after delay
The two action buttons SHALL animate in from below (y:20→0, opacity 0→1) with a stagger effect, starting after a 300ms delay from mount.

#### Scenario: Buttons animate in after check icon
- **WHEN** the YoureInScreen mounts
- **THEN** the two buttons animate from y:20 to y:0 with opacity 0→1, staggered, after a 300ms delay

### Requirement: Content is centered on both axes
The YoureInScreen layout SHALL center its content both vertically and horizontally within the screen area, with px-6 horizontal padding.

#### Scenario: Content is centered
- **WHEN** the YoureInScreen renders
- **THEN** the check icon, heading, and buttons are centered vertically and horizontally with px-6 padding

### Requirement: No BottomNav on You're In screen
The BottomNav component SHALL NOT render when the current screen is 'youre-in'.

#### Scenario: BottomNav is hidden
- **WHEN** the current screen is 'youre-in'
- **THEN** the BottomNav is not visible
