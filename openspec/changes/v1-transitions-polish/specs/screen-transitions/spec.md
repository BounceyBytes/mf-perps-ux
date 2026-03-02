## ADDED Requirements

### Requirement: AnimatePresence wraps screen router with mode="wait"
The screen router in `page.tsx` SHALL be wrapped in a Framer Motion AnimatePresence with `mode="wait"`. Each screen SHALL be wrapped in a `motion.div` keyed by the current screen name.

#### Scenario: Screen change triggers exit then enter animation
- **WHEN** the store.screen value changes from one screen to another
- **THEN** the current screen animates out fully before the new screen animates in

### Requirement: Onboarding screens use slide-from-right transition
The screens 'welcome', 'kyc', and 'youre-in' SHALL use a slide-from-right transition: initial `{ x: 30, opacity: 0 }`, animate `{ x: 0, opacity: 1 }`, exit `{ x: -30, opacity: 0 }`, with a duration of 300ms. The 'referral' screen is deferred to V3 — see [plan-v3-referral-program.md](../../../../plan-v3-referral-program.md).

#### Scenario: Welcome to KYC transition
- **WHEN** the user navigates from 'welcome' to 'kyc'
- **THEN** the welcome screen slides out to the left (x: -30, opacity: 0) and the KYC screen slides in from the right (x: 30→0, opacity: 0→1) over 300ms

#### Scenario: KYC to youre-in transition
- **WHEN** the user navigates from 'kyc' to 'youre-in'
- **THEN** the KYC screen exits left and the youre-in screen enters from the right over 300ms

### Requirement: Tab screens use crossfade transition
The screens 'home', 'trade', and 'portfolio' SHALL use a crossfade transition: initial `{ opacity: 0 }`, animate `{ opacity: 1 }`, exit `{ opacity: 0 }`, with a duration of 200ms. No horizontal or vertical slide.

#### Scenario: Home to portfolio tab switch
- **WHEN** the user taps the Portfolio tab in BottomNav
- **THEN** the home screen fades out (opacity 1→0) and the portfolio screen fades in (opacity 0→1) over 200ms

#### Scenario: Portfolio to trade tab switch
- **WHEN** the user taps the Trade tab in BottomNav
- **THEN** the portfolio screen fades out and the trade screen fades in over 200ms

### Requirement: Modal screens use slide-up transition
The screens 'deposit', 'deposit-amount', and 'withdraw' SHALL use a slide-up-from-bottom transition: initial `{ y: 50, opacity: 0 }`, animate `{ y: 0, opacity: 1 }`, exit `{ y: 50, opacity: 0 }`, with a duration of 300ms.

#### Scenario: Navigate to deposit screen
- **WHEN** the user navigates to 'deposit'
- **THEN** the deposit screen slides up from the bottom (y: 50→0, opacity: 0→1) over 300ms

#### Scenario: Exit withdraw screen
- **WHEN** the user taps back on the withdraw screen
- **THEN** the withdraw screen slides down (y: 0→50, opacity: 1→0) over 300ms

### Requirement: Transition variant is determined by screen category
A helper function or map SHALL categorize each screen into 'onboarding', 'tabs', or 'modal' and return the corresponding transition variants. Unrecognized screens SHALL default to crossfade.

#### Scenario: Screen maps to correct category
- **WHEN** the screen is 'kyc'
- **THEN** the onboarding (slide-right) transition variants are used

#### Scenario: Unknown screen defaults to crossfade
- **WHEN** the screen is an unrecognized value
- **THEN** the crossfade transition variants are used
