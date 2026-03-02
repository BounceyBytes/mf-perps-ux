## ADDED Requirements

### Requirement: ReferralScreen renders heading
The ReferralScreen SHALL display "Got an invite code?" as a heading in text-2xl font-bold with pt-16.

#### Scenario: Screen loads with heading
- **WHEN** the ReferralScreen renders
- **THEN** the heading "Got an invite code?" is displayed at text-2xl font-bold with pt-16

### Requirement: Back arrow navigates to KYC screen
The ReferralScreen SHALL display a ChevronLeft icon (Lucide) in the top-left area. Tapping the back arrow SHALL call `store.navigate('kyc')`.

#### Scenario: User taps back arrow
- **WHEN** the user taps the ChevronLeft back arrow
- **THEN** the app navigates to the 'kyc' screen

### Requirement: Code input field is displayed with code-entry styling
The ReferralScreen SHALL render an Input component with mt-8, text-center, text-xl, tracking-widest, placeholder "Enter code", autoCapitalize, and maxLength 12. The input SHALL use the base Input component with className overrides for centered code-entry styling.

#### Scenario: Input renders with code-entry styling
- **WHEN** the ReferralScreen renders
- **THEN** a text input is displayed with centered text, large font, wide letter spacing, and placeholder "Enter code"

#### Scenario: Input enforces maxLength
- **WHEN** the user types more than 12 characters
- **THEN** the input stops accepting additional characters at 12

### Requirement: Incentive text is displayed below the input
The ReferralScreen SHALL display "You'll both earn trading rewards" in text-sm text-secondary, centered, with mt-4 below the input field.

#### Scenario: Incentive text is visible
- **WHEN** the ReferralScreen renders
- **THEN** the text "You'll both earn trading rewards" is displayed below the input in text-sm text-secondary, centered

### Requirement: Continue button is displayed full width
The ReferralScreen SHALL render a primary Button with text "Continue" at full width in the CTA area, pushed to the bottom with mt-auto.

#### Scenario: Continue button is visible
- **WHEN** the ReferralScreen renders
- **THEN** a full-width primary button with text "Continue" is visible near the bottom of the screen

### Requirement: Skip link is displayed below Continue button
The ReferralScreen SHALL display a "Skip" text link below the Continue button with mt-3, styled as text-secondary with underline, centered. Tapping Skip SHALL navigate to 'youre-in'.

#### Scenario: Skip link is visible and styled
- **WHEN** the ReferralScreen renders
- **THEN** a "Skip" link is displayed below the Continue button, centered, in text-secondary with underline

#### Scenario: User taps Skip
- **WHEN** the user taps "Skip"
- **THEN** the app navigates to the 'youre-in' screen

### Requirement: Continue with code shows green checkmark then navigates
When the user taps "Continue" and the input contains text, the ReferralScreen SHALL display a green Check icon (Lucide) next to the input field, animated from scale 0 to scale 1 using Framer Motion. After a 500ms delay, the app SHALL navigate to 'youre-in'.

#### Scenario: User taps Continue with a code entered
- **WHEN** the user has entered text in the input and taps "Continue"
- **THEN** a green checkmark animates in (scale 0→1) next to the input

#### Scenario: Navigation occurs after checkmark animation
- **WHEN** the green checkmark has been displayed for 500ms
- **THEN** the app navigates to the 'youre-in' screen

### Requirement: Continue with empty input navigates directly
When the user taps "Continue" and the input is empty, the app SHALL navigate directly to the 'youre-in' screen without showing the checkmark animation.

#### Scenario: User taps Continue with empty input
- **WHEN** the user taps "Continue" with no text in the input
- **THEN** the app navigates directly to the 'youre-in' screen without a checkmark animation

### Requirement: Entrance animation slides in from the right
The ReferralScreen content SHALL animate in from the right on mount — x: 30 → 0 with opacity: 0 → 1 — using Framer Motion.

#### Scenario: Screen slides in from right on mount
- **WHEN** the ReferralScreen mounts
- **THEN** the content animates from x: 30, opacity: 0 to x: 0, opacity: 1

### Requirement: No BottomNav on Referral screen
The BottomNav component SHALL NOT render when the current screen is 'referral'.

#### Scenario: BottomNav is hidden
- **WHEN** the current screen is 'referral'
- **THEN** the BottomNav is not visible
