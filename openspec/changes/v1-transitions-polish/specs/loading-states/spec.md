## ADDED Requirements

### Requirement: KYC screen CTA shows loading spinner during verification
The KYC screen "Start verification" button SHALL show a Loader2 icon (from lucide-react) with `animate-spin` class when tapped, replacing or accompanying the button text during the simulated loading period.

#### Scenario: User taps Start verification
- **WHEN** the user taps the "Start verification" button on the KYC screen
- **THEN** the button text changes to show a spinning Loader2 icon and the button is disabled until the simulated action completes

#### Scenario: Loading completes and navigates
- **WHEN** the simulated verification completes (after ~1s)
- **THEN** the spinner stops and the app navigates to the next screen

### Requirement: Deposit amount CTA shows loading spinner during funding
The DepositAmountScreen "Fund $X.XX" button SHALL show a Loader2 icon with `animate-spin` class when tapped, replacing or accompanying the button text during the simulated deposit processing.

#### Scenario: User taps Fund CTA
- **WHEN** the user taps the "Fund $100.00" button on the deposit amount screen
- **THEN** the button shows a spinning Loader2 icon and is disabled during the simulated processing (~1s)

#### Scenario: Funding completes with toast
- **WHEN** the simulated deposit processing completes
- **THEN** the spinner stops, the app navigates to 'home', and a success toast appears (e.g., "Account funded: +$100.00")
