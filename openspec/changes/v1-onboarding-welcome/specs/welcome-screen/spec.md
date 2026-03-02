## ADDED Requirements

### Requirement: WelcomeScreen renders brand logo and tagline
The WelcomeScreen SHALL display the MF Perps logo with "MF" in accent color (#7B61FF) and "Perps" in white, rendered at text-3xl font-bold, centered horizontally with pt-24. Below the logo, the screen SHALL display "Trade BTC, ETH & more" in text-lg and "Up to 100x leverage" in text-sm text-secondary.

#### Scenario: Screen loads with brand identity
- **WHEN** the WelcomeScreen renders
- **THEN** the logo shows "MF" in accent and "Perps" in white at text-3xl, centered with top padding, followed by tagline text

### Requirement: Three auth buttons are displayed
The WelcomeScreen SHALL render three vertically stacked buttons with gap-3 and px-6: "Continue with Apple" (white background, black text, Apple icon), "Continue with Google" (surface-light background, white text, Google icon), and "Use email or phone" (ghost variant, Mail icon).

#### Scenario: Auth buttons are visible
- **WHEN** the WelcomeScreen renders
- **THEN** three auth buttons are displayed in a vertical stack: Apple (white bg), Google (surface-light bg), and email/phone (ghost)

### Requirement: All auth actions navigate to KYC screen
Every auth button and the "Sign in" link SHALL call `store.navigate('kyc')` when tapped.

#### Scenario: User taps Continue with Apple
- **WHEN** the user taps "Continue with Apple"
- **THEN** the app navigates to the 'kyc' screen

#### Scenario: User taps Continue with Google
- **WHEN** the user taps "Continue with Google"
- **THEN** the app navigates to the 'kyc' screen

#### Scenario: User taps Use email or phone
- **WHEN** the user taps "Use email or phone"
- **THEN** the app navigates to the 'kyc' screen

#### Scenario: User taps Sign in link
- **WHEN** the user taps "Sign in" in the bottom link
- **THEN** the app navigates to the 'kyc' screen

### Requirement: Sign-in link is displayed at the bottom
The WelcomeScreen SHALL display "Already have an account? Sign in" at the bottom of the screen, with "Sign in" styled in the accent color as a tappable link.

#### Scenario: Sign-in link is visible
- **WHEN** the WelcomeScreen renders
- **THEN** text "Already have an account? Sign in" appears at the bottom with "Sign in" in accent color

### Requirement: Entrance animations play on mount
The WelcomeScreen SHALL fade in on mount (opacity 0→1 over 500ms). The auth buttons SHALL stagger in from below (y:20→0) with 100ms stagger delay between each button.

#### Scenario: Screen fades in on mount
- **WHEN** the WelcomeScreen mounts
- **THEN** the container animates from opacity 0 to 1 over 500ms

#### Scenario: Buttons stagger in from below
- **WHEN** the WelcomeScreen mounts
- **THEN** the three auth buttons animate from y:20 to y:0 with opacity 0→1, each staggered by 100ms

### Requirement: Buttons have press feedback
All auth buttons SHALL animate to scale 0.97 on press (whileTap).

#### Scenario: User presses and holds a button
- **WHEN** the user presses and holds any auth button
- **THEN** the button scales to 0.97 while pressed

### Requirement: No BottomNav on Welcome screen
The BottomNav component SHALL NOT render when the current screen is 'welcome'.

#### Scenario: BottomNav is hidden
- **WHEN** the current screen is 'welcome'
- **THEN** the BottomNav is not visible
