## ADDED Requirements

### Requirement: Bottom sheet slides up from bottom with spring animation
The ClosePosition overlay SHALL render as a bottom sheet that animates from `y: "100%"` to `y: 0` using Framer Motion spring animation (type: "spring", damping: ~25, stiffness: ~300). The sheet SHALL have surface background, `rounded-t-3xl`, `px-6 py-8`.

#### Scenario: Sheet animates in when overlay is active
- **WHEN** `store.overlay` is set to `'close-position'`
- **THEN** the bottom sheet slides up from the bottom of the phone frame with spring animation, surface background, rounded-t-3xl corners, and px-6 py-8 padding

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

### Requirement: Heading displays "Close {pair} {direction}?" centered
The sheet SHALL render a heading "Close BTC Long?" (or matching the position's pair and direction) in text-xl font-bold, centered.

#### Scenario: Long position heading
- **WHEN** the closing position is BTC/USD Long
- **THEN** "Close BTC Long?" appears in text-xl font-bold, centered

#### Scenario: Short position heading
- **WHEN** the closing position is ETH/USD Short
- **THEN** "Close ETH Short?" appears in text-xl font-bold, centered

### Requirement: Summary section displays P&L and receive amount
A summary section SHALL render below the heading (mt-4) with two rows in text-sm. The first row SHALL show "Your P&L" (text-secondary) on the left and the P&L value (font-semibold) on the right, colored green (#00D68F) for positive and red (#FF4757) for negative. The second row SHALL show "You'll receive" (text-secondary) on the left and the receive amount (text-primary, font-semibold) on the right.

#### Scenario: Positive P&L summary
- **WHEN** the closing position has pnl=+12.80 and currentValue=512.80
- **THEN** "Your P&L" shows "+$12.80" in green font-semibold and "You'll receive" shows "$512.80" in text-primary font-semibold

#### Scenario: Negative P&L summary
- **WHEN** the closing position has pnl=-25.00 and currentValue=475.00
- **THEN** "Your P&L" shows "-$25.00" in red font-semibold and "You'll receive" shows "$475.00" in text-primary font-semibold

### Requirement: "Close Full Position" primary button triggers close flow
A primary button labeled "Close Full Position" SHALL render full width with mt-6 and accent background. Tapping it SHALL dismiss the overlay, remove the position from the store's positions array, and show a success toast.

#### Scenario: User taps Close Full Position
- **WHEN** the user taps "Close Full Position"
- **THEN** `store.dismissOverlay()` is called, the position is removed from the store's open positions, and a toast "Position closed — $512.80 received" appears

#### Scenario: Position animates out of portfolio list
- **WHEN** the position is removed from the store after tapping "Close Full Position"
- **THEN** the corresponding PositionCard in the portfolio list animates out (exit animation via AnimatePresence)

### Requirement: Success toast displays after position close
A toast notification SHALL appear at the top of the phone frame displaying "Position closed — ${amount} received" after a position is closed. The toast SHALL auto-dismiss after 2.5 seconds (consistent with the toast notification spec in transitions-polish).

#### Scenario: Toast appears and auto-dismisses
- **WHEN** the user confirms closing a position with currentValue=512.80
- **THEN** a toast reading "Position closed — $512.80 received" appears at the top of the phone frame and disappears after 2.5 seconds

### Requirement: "Close Partial ▼" expands a slider (stretch feature)
A ghost text link labeled "Close Partial ▼" SHALL render centered below the primary button (mt-3, text-sm, text-secondary). Tapping it SHALL toggle an AnimatePresence section containing a range slider (0–100%) with a percentage label. The slider is visual only and does not affect the close amount or store state.

#### Scenario: User taps Close Partial to expand slider
- **WHEN** the user taps "Close Partial ▼"
- **THEN** a slider section animates in below the link via AnimatePresence, showing a range input from 0% to 100% with a percentage label

#### Scenario: User taps Close Partial again to collapse slider
- **WHEN** the slider section is visible and the user taps "Close Partial ▼" again
- **THEN** the slider section animates out via AnimatePresence

#### Scenario: Slider does not affect close amount
- **WHEN** the user moves the partial close slider to 50%
- **THEN** the displayed percentage updates but the "Close Full Position" button behavior and summary values do not change

### Requirement: "Cancel" ghost link dismisses overlay
A ghost text link labeled "Cancel" SHALL render centered below the Close Partial link (mt-3, text-sm, text-muted). Tapping it SHALL call `store.dismissOverlay()`.

#### Scenario: User taps Cancel
- **WHEN** the user taps "Cancel"
- **THEN** `store.dismissOverlay()` is called and the sheet closes

### Requirement: Overlay renders only when store.overlay equals 'close-position'
The ClosePosition component SHALL only render when `store.overlay === 'close-position'`. When the overlay value is null or any other string, the component SHALL not be in the DOM.

#### Scenario: Overlay renders when triggered
- **WHEN** `store.overlay` is `'close-position'`
- **THEN** the ClosePosition bottom sheet renders with backdrop

#### Scenario: Overlay does not render otherwise
- **WHEN** `store.overlay` is `null`
- **THEN** the ClosePosition component is not in the DOM

### Requirement: Store exposes closingPosition and toast state
The Zustand store SHALL expose a `closingPosition` field (set when a PositionCard close button is tapped) containing the position's pair, direction, pnl, and currentValue. The store SHALL also expose a `toast` field (string | null) with a `showToast(msg)` action that sets the toast and auto-clears it after ~3 seconds.

#### Scenario: PositionCard close sets closingPosition
- **WHEN** the user taps "Close" on a PositionCard for BTC/USD Long with pnl=+12.80, currentValue=512.80
- **THEN** `store.closingPosition` is set to `{ pair: 'BTC/USD', direction: 'Long', pnl: 12.80, currentValue: 512.80 }`

#### Scenario: showToast sets and auto-clears toast
- **WHEN** `showToast('Position closed — $512.80 received')` is called
- **THEN** `store.toast` is `'Position closed — $512.80 received'` and after 2.5 seconds `store.toast` becomes `null`

### Requirement: Share card trigger on profitable close
When the user closes a position with positive P&L, the close flow SHALL trigger the share-card overlay after the position is removed. Specifically, after calling `store.dismissOverlay()` and `store.showToast(...)`, a setTimeout of ~500ms SHALL call `store.showOverlay('share-card')` to let the user celebrate and share their profit.

#### Scenario: Profitable close triggers share card
- **WHEN** the user taps "Close Full Position" on a position with positive P&L (pnl > 0)
- **THEN** the overlay dismisses, a toast appears, and after ~500ms the share-card overlay is shown

#### Scenario: Loss close does not trigger share card
- **WHEN** the user taps "Close Full Position" on a position with negative P&L (pnl < 0)
- **THEN** the overlay dismisses and a toast appears, but the share-card overlay is NOT shown
