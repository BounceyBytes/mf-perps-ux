## ADDED Requirements

### Requirement: Overlay renders only when store.overlay equals 'share-card'
The ShareCard component SHALL only render when `store.overlay === 'share-card'`. When the overlay value is null or any other string, the component SHALL not be in the DOM.

#### Scenario: Overlay renders when triggered
- **WHEN** `store.overlay` is set to `'share-card'`
- **THEN** the ShareCard full-screen overlay renders with backdrop and centered card

#### Scenario: Overlay does not render otherwise
- **WHEN** `store.overlay` is `null` or any value other than `'share-card'`
- **THEN** the ShareCard component is not in the DOM

### Requirement: Full-screen backdrop with bg-black/80
The overlay SHALL render a full-screen backdrop within the phone frame using `bg-black/80`. The card content SHALL be centered within the backdrop.

#### Scenario: Backdrop covers phone frame
- **WHEN** the share-card overlay is open
- **THEN** a semi-transparent dark overlay (`bg-black/80`) covers the full phone frame area with content centered vertically and horizontally

### Requirement: Share card container with gradient background
The share card SHALL have `max-w-[320px]`, `rounded-2xl`, and `overflow-hidden`. The background SHALL be a linear gradient from surface (#14141F) to purple-tinted dark (#1a1530).

#### Scenario: Card container renders with correct styling
- **WHEN** the share-card overlay is open
- **THEN** a card renders with max-width 320px, rounded-2xl corners, overflow-hidden, and a gradient background from #14141F to #1a1530

### Requirement: Top accent bar renders as green gradient
A 4px tall bar SHALL render at the top of the share card with a green gradient, spanning the full width of the card. This indicates a winning/long position.

#### Scenario: Green accent bar is visible
- **WHEN** the share-card overlay is open
- **THEN** a 4px tall green gradient bar appears at the top of the card spanning its full width

### Requirement: Position direction and pair display
The card SHALL display the position direction emoji and pair name (e.g., "🟢 BTC Long") in `text-lg font-bold` with green color, inside `p-6` padding.

#### Scenario: Position info renders
- **WHEN** the share-card overlay shows a BTC Long position
- **THEN** "🟢 BTC Long" is displayed in text-lg font-bold green text within the card's padded content area

### Requirement: Hero PnL percentage display
The card SHALL display the PnL percentage (e.g., "+47.2%") in `text-4xl font-bold text-green` as the primary visual element of the card.

#### Scenario: PnL percentage is prominently displayed
- **WHEN** the share-card overlay is open with a +47.2% gain
- **THEN** "+47.2%" renders in text-4xl font-bold green as the largest text element on the card

### Requirement: Dollar breakdown display
The card SHALL display the dollar breakdown (e.g., "$500 → $735.00") in `text-sm` with secondary text color below the PnL percentage.

#### Scenario: Dollar amounts render below PnL
- **WHEN** the position started at $500 and is now worth $735.00
- **THEN** "$500 → $735.00" renders in text-sm text-secondary below the hero percentage

### Requirement: User info section with avatar and name
The card SHALL display a user info section (mt-4) with a 24px circular avatar and the user's name in text-xs.

#### Scenario: User info renders
- **WHEN** the share-card overlay is open
- **THEN** a 24px circular avatar and the user name "Jake" appear in a horizontal row below the dollar breakdown

### Requirement: Divider separates position info from referral area
A horizontal divider (`border-t border-[#2A2A3A]`, mt-4) SHALL separate the position/user info from the referral area below.

#### Scenario: Divider is visible
- **WHEN** the share-card overlay is open
- **THEN** a horizontal line (border-t border-[#2A2A3A]) appears between the user info and referral area

### Requirement: Referral area with CTA text, link, and QR placeholder
The referral area (mt-4) SHALL display "Trade on MF Perps" in `text-sm font-semibold`, the referral link "mfperps.app/join/JAKE2026" in `text-xs text-accent`, and a 64×64 QR placeholder box with `rounded-lg` and surface-light background.

#### Scenario: Referral area renders completely
- **WHEN** the share-card overlay is open
- **THEN** "Trade on MF Perps" appears in text-sm font-semibold, "mfperps.app/join/JAKE2026" appears in text-xs text-accent, and a 64×64 rounded-lg surface-light placeholder box represents the QR code

### Requirement: Card entrance animation with scale and opacity
The share card SHALL animate in using Framer Motion with `initial={{ scale: 0.8, opacity: 0 }}` and `animate={{ scale: 1, opacity: 1 }}` using a spring transition.

#### Scenario: Card pops in on open
- **WHEN** `store.overlay` changes to `'share-card'`
- **THEN** the card animates from scale 0.8 and opacity 0 to scale 1 and opacity 1 with a spring transition

#### Scenario: Card animates out on dismiss
- **WHEN** the overlay is dismissed
- **THEN** the card animates back to scale 0.8 and opacity 0 before being removed from the DOM

### Requirement: Share button renders as primary with Share2 icon
A "Share" button SHALL render below the card (mt-6, within px-6) as a Primary Button variant with a Share2 icon from Lucide. Tapping it SHALL display a toast "Shared!".

#### Scenario: Share button renders correctly
- **WHEN** the share-card overlay is open
- **THEN** a primary "Share" button with Share2 icon renders below the card

#### Scenario: Tapping Share shows toast
- **WHEN** the user taps the "Share" button
- **THEN** a toast message "Shared!" is displayed

### Requirement: Save Image button renders as secondary with Download icon
A "Save Image" button SHALL render below the Share button (gap-3) as a Secondary Button variant with a Download icon from Lucide. Tapping it SHALL display a toast "Saved!".

#### Scenario: Save Image button renders correctly
- **WHEN** the share-card overlay is open
- **THEN** a secondary "Save Image" button with Download icon renders below the Share button

#### Scenario: Tapping Save Image shows toast
- **WHEN** the user taps the "Save Image" button
- **THEN** a toast message "Saved!" is displayed

### Requirement: Done link dismisses the overlay
A "Done" text link SHALL render centered below the buttons in `text-sm text-muted`. Tapping it SHALL call `store.dismissOverlay()` to close the share-card overlay.

#### Scenario: Done link is visible
- **WHEN** the share-card overlay is open
- **THEN** a "Done" text link appears centered below the action buttons in text-sm text-muted

#### Scenario: Tapping Done dismisses overlay
- **WHEN** the user taps "Done"
- **THEN** `store.dismissOverlay()` is called and the overlay closes

### Requirement: Overlay wired into page.tsx overlay layer
The ShareCard component SHALL be imported and rendered in `page.tsx` within the overlay layer, wrapped in `AnimatePresence`, conditionally when `store.overlay === 'share-card'`.

#### Scenario: ShareCard renders in overlay layer
- **WHEN** `store.overlay` equals `'share-card'`
- **THEN** the ShareCard component is rendered within the AnimatePresence wrapper in page.tsx's overlay layer
