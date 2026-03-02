## ADDED Requirements

### Requirement: KycScreen renders heading and subtext
The KycScreen SHALL display "Verify your identity" as a heading in text-2xl font-bold with pt-16. Below the heading, it SHALL display "Usually takes ~30 seconds. Verification helps keep the venue trusted." in text-sm text-secondary.

#### Scenario: Screen loads with heading and subtext
- **WHEN** the KycScreen renders
- **THEN** the heading "Verify your identity" is displayed at text-2xl font-bold with pt-16, and the subtext is displayed below in text-sm text-secondary

### Requirement: Back arrow navigates to welcome screen
The KycScreen SHALL display a ChevronLeft icon (Lucide) in the top-left area. Tapping the back arrow SHALL call `store.navigate('welcome')`.

#### Scenario: User taps back arrow
- **WHEN** the user taps the ChevronLeft back arrow
- **THEN** the app navigates to the 'welcome' screen

### Requirement: Two verification step cards are displayed
The KycScreen SHALL render two horizontal step cards in a vertical stack with mt-8 and gap-3. Each card SHALL have a horizontal layout with an icon in accent color, a title, a description in text-xs text-secondary, and a ChevronRight icon.

#### Scenario: Scan ID step card is visible
- **WHEN** the KycScreen renders
- **THEN** a card is displayed with a FileText icon in accent, title "Scan your ID", description "Government-issued ID" in text-xs text-secondary, and a ChevronRight icon

#### Scenario: Take a selfie step card is visible
- **WHEN** the KycScreen renders
- **THEN** a card is displayed with a Camera icon in accent, title "Take a selfie", description "Quick face match" in text-xs text-secondary, and a ChevronRight icon

### Requirement: Trust badge is displayed near the bottom
The KycScreen SHALL display a trust badge with a Lock icon and text "Bank-grade encryption. Your data is never shared." in text-xs text-muted. The trust badge SHALL be pushed toward the bottom using mt-auto with pb-8.

#### Scenario: Trust badge is visible
- **WHEN** the KycScreen renders
- **THEN** a trust badge with Lock icon and encryption text is visible near the bottom of the screen

### Requirement: CTA button is displayed full width
The KycScreen SHALL render a primary Button with text "Start verification" at full width near the bottom of the screen.

#### Scenario: CTA button is visible
- **WHEN** the KycScreen renders
- **THEN** a full-width primary button with text "Start verification" is visible near the bottom

### Requirement: CTA shows loading spinner then navigates to referral
When the user taps the "Start verification" button, the button SHALL display a Loader2 spinning icon for 1.5 seconds. After the 1.5s delay, the app SHALL navigate to the 'referral' screen via `store.navigate('referral')`. The button SHALL be disabled while loading.

#### Scenario: User taps Start verification
- **WHEN** the user taps "Start verification"
- **THEN** the button shows a Loader2 spinning icon and is disabled

#### Scenario: Loading completes after 1.5 seconds
- **WHEN** 1.5 seconds have elapsed since the user tapped "Start verification"
- **THEN** the app navigates to the 'referral' screen

### Requirement: Entrance animation slides in from the right
The KycScreen content SHALL animate in from the right on mount — x: 30 → 0 with opacity: 0 → 1 — using Framer Motion.

#### Scenario: Screen slides in from right on mount
- **WHEN** the KycScreen mounts
- **THEN** the content animates from x: 30, opacity: 0 to x: 0, opacity: 1

### Requirement: No BottomNav on KYC screen
The BottomNav component SHALL NOT render when the current screen is 'kyc'.

#### Scenario: BottomNav is hidden
- **WHEN** the current screen is 'kyc'
- **THEN** the BottomNav is not visible
