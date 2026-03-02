## ADDED Requirements

### Requirement: Bottom sheet slides up from bottom with spring animation
The TradeConfirmation overlay SHALL render as a bottom sheet that animates from `y: "100%"` to `y: 0` using Framer Motion spring animation (type: "spring", damping: ~25, stiffness: ~300). The sheet SHALL have surface background, `rounded-t-3xl`, `px-6 py-8`, and a max height of 50% of the phone frame.

#### Scenario: Sheet animates in when overlay is active
- **WHEN** `store.overlay` is set to `'trade-confirmation'`
- **THEN** the bottom sheet slides up from the bottom of the phone frame with spring animation, surface background, rounded-t-3xl corners, px-6 py-8 padding, and max height 50%

#### Scenario: Sheet animates out on dismiss
- **WHEN** the overlay is dismissed
- **THEN** the sheet animates back to `y: "100%"` and is removed from the DOM

### Requirement: Drag handle bar renders at top of sheet
The sheet SHALL render a centered drag handle bar at the top: `w-10 h-1 rounded-full bg-[#2A2A3A]`.

#### Scenario: Drag handle is visible
- **WHEN** the bottom sheet is open
- **THEN** a centered horizontal bar (w-10 h-1 rounded-full bg-[#2A2A3A]) appears at the top of the sheet

### Requirement: Backdrop renders and dismisses on tap
A fixed overlay backdrop with `bg-black/50` SHALL render behind the sheet. Tapping the backdrop SHALL call `store.dismissOverlay()` to close the sheet.

#### Scenario: Backdrop is visible behind sheet
- **WHEN** the bottom sheet is open
- **THEN** a semi-transparent black overlay (bg-black/50) covers the area behind the sheet

#### Scenario: Tapping backdrop dismisses sheet
- **WHEN** the user taps the backdrop area (outside the sheet)
- **THEN** `store.dismissOverlay()` is called and the sheet closes

### Requirement: Swipe down to dismiss with 100px threshold
The sheet SHALL support Framer Motion `drag="y"` with `dragConstraints={{ top: 0 }}`. When the user releases the drag and the y offset exceeds 100px, the sheet SHALL dismiss via `store.dismissOverlay()`. Drags less than 100px SHALL snap the sheet back to its open position.

#### Scenario: Swipe down beyond threshold dismisses
- **WHEN** the user drags the sheet down more than 100px and releases
- **THEN** `store.dismissOverlay()` is called and the sheet closes

#### Scenario: Small drag snaps back
- **WHEN** the user drags the sheet down less than 100px and releases
- **THEN** the sheet animates back to its fully open position

### Requirement: Green checkmark icon scales in with spring animation
A CheckCircle2 icon from Lucide SHALL render centered at the top of the sheet content, size 48px, in green (#00D68F). The icon SHALL animate in with a spring scale transition from 0 to 1.

#### Scenario: Checkmark appears with scale animation
- **WHEN** the bottom sheet finishes its entrance animation
- **THEN** a green CheckCircle2 icon (48px) is visible, centered, having scaled in from 0 to 1 with spring animation

### Requirement: "Position Opened" heading fades in
A heading "Position Opened" SHALL render in text-xl font-bold, centered, with mt-4 below the checkmark icon. The text SHALL fade in with a slight delay (~200ms) after the icon animation begins.

#### Scenario: Heading appears after icon
- **WHEN** the bottom sheet opens
- **THEN** "Position Opened" appears in text-xl font-bold, centered, fading in after the checkmark icon begins its animation

### Requirement: Summary card displays trade parameters
A Card SHALL render below the heading (mt-4) showing the trade parameters: pair name, direction, amount, leverage (e.g., "BTC Long $500 @ 10x") and entry price (e.g., "Entry: $67,156"). The values SHALL reflect the actual trade parameters from the store.

#### Scenario: Summary card shows trade details
- **WHEN** the user opened a Long position on BTC with $50 amount at 10x leverage and entry price $67,156
- **THEN** the summary card displays "BTC Long $500 @ 10x" and "Entry: $67,156"

#### Scenario: Summary card reflects Short direction
- **WHEN** the user opened a Short position on ETH with $100 amount at 5x leverage and entry price $3,456
- **THEN** the summary card displays "ETH Short $500 @ 5x" and "Entry: $3,456"

### Requirement: Three action buttons render in vertical stack
Three buttons SHALL render below the summary card (mt-6, gap-3) in a vertical stack:
1. "View Position" — Primary variant (accent background)
2. "Trade Again" — Secondary variant (surface-light background)
3. "Set TP/SL" — Secondary variant (surface-light background)

#### Scenario: All three buttons are visible
- **WHEN** the bottom sheet is open
- **THEN** "View Position" renders as a primary button, "Trade Again" renders as a secondary button, and "Set TP/SL" renders as a secondary button, stacked vertically with gap-3

### Requirement: "View Position" navigates to portfolio and dismisses
Tapping the "View Position" button SHALL call `store.navigate('portfolio')` and `store.dismissOverlay()`.

#### Scenario: User taps View Position
- **WHEN** the user taps "View Position"
- **THEN** the app navigates to the 'portfolio' screen and the overlay is dismissed

### Requirement: "Trade Again" dismisses overlay and stays on trade screen
Tapping the "Trade Again" button SHALL call `store.dismissOverlay()` without navigating, leaving the user on the trade screen.

#### Scenario: User taps Trade Again
- **WHEN** the user taps "Trade Again"
- **THEN** the overlay is dismissed and the user remains on the trade screen

### Requirement: "Set TP/SL" is a placeholder button
Tapping the "Set TP/SL" button SHALL be a no-op in v1. The button renders to validate UX placement but does not trigger any action.

#### Scenario: User taps Set TP/SL
- **WHEN** the user taps "Set TP/SL"
- **THEN** nothing happens (no navigation, no state change)

### Requirement: Overlay renders only when store.overlay equals 'trade-confirmation'
The TradeConfirmation component SHALL only render when `store.overlay === 'trade-confirmation'`. When the overlay value is null or any other string, the component SHALL not be in the DOM.

#### Scenario: Overlay renders when triggered
- **WHEN** `store.overlay` is `'trade-confirmation'`
- **THEN** the TradeConfirmation bottom sheet renders with backdrop

#### Scenario: Overlay does not render otherwise
- **WHEN** `store.overlay` is `null`
- **THEN** the TradeConfirmation component is not in the DOM
