## Why

After closing positions or accumulating funds, users need a way to withdraw money from their account. Without a withdraw screen, the prototype's portfolio flow is incomplete — users can deposit and trade but never extract value. The withdraw screen closes the loop on the funds lifecycle and validates the withdrawal UX pattern (amount selection, destination entry, confirmation) before integrating real blockchain transactions or fiat off-ramps.

## What Changes

- Create `WithdrawScreen` component (`src/components/screens/WithdrawScreen.tsx`) — a single-screen withdrawal flow rendered inside PhoneFrame with:
  - Header: back arrow navigating to 'portfolio' + "Withdraw" centered in text-lg font-semibold
  - Available balance display (mt-2, centered): "Available: $512.80" in text-sm text-secondary
  - Large amount display (mt-4, centered): "$512.80" in text-4xl font-bold text-primary, pre-filled with the max available balance
  - Quick-select chips (mt-3, centered): "25%", "50%", "Max" as rounded-full pills — "Max" active by default with accent border, tapping recalculates the amount based on the percentage of available balance
  - "Withdraw to:" label (mt-6): text-xs uppercase tracking-wider text-muted
  - Single destination card (mt-2): Wallet icon left + "External Wallet" name + "Paste or select wallet address" text-xs text-secondary + "Instant" text-xs text-muted — accent border with checkmark on the right
  - Tapping the wallet card expands an input section with AnimatePresence: a text field for wallet address with a paste button + "Confirm Withdraw" primary button
  - Confirm tap: 1.5s loading spinner on button → navigate to 'portfolio' + success toast "Withdrawal initiated — $512.80"
  - No BottomNav on this screen
  - V1 supports external wallet only — no fiat off-ramps
- Wire the screen into the screen router in `page.tsx` for `screen === 'withdraw'`

## Capabilities

### New Capabilities
- `withdraw-screen`: WithdrawScreen component with balance display, quick-select percentage chips, wallet destination card with expandable address input, and confirmation flow with loading state and success toast

### Modified Capabilities

## Impact

- Adds 1 new file: `src/components/screens/WithdrawScreen.tsx`
- Updates `page.tsx` screen router to render WithdrawScreen for 'withdraw'
- Depends on: PhoneFrame, StatusBar, Card, Button, Zustand store (from core-components change)
- Connects from: portfolio screen (via withdraw action)
- Connects to: portfolio screen (after successful withdrawal with toast)
