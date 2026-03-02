## Why

After onboarding, users need to fund their account before they can trade. The deposit flow is the critical conversion step between "signed up" and "active trader." Without a clear, fast funding experience, users drop off before ever opening a position. V1 supports crypto transfer from an external wallet. Fiat on-ramps (debit card, Apple Pay) are deferred to V5. The flow is presented in a frictionless mobile-native interface with a custom NumPad for precise amount entry.

## What Changes

- Create `DepositScreen` component (`src/components/screens/DepositScreen.tsx`) — method selection screen rendered inside PhoneFrame with:
  - Header: back arrow navigating to 'home' or 'youre-in' (depending on flow) + "Fund Account" centered
  - Transfer Crypto method card (mt-6, gap-3): "Transfer Crypto" (Wallet icon, "From another wallet") — fiat on-ramps (Debit Card, Apple Pay) deferred to V5
  - Transfer Crypto card opens a bottom sheet with QR code placeholder and mock wallet address
  - Cards stagger in on mount with Framer Motion
  - No BottomNav on this screen
- Create `DepositAmountScreen` component (`src/components/screens/DepositAmountScreen.tsx`) — amount entry screen rendered inside PhoneFrame with:
  - Header: back arrow navigating to 'deposit' + "Fund Account" centered
  - Large amount display: "$" prefix in text-2xl text-secondary + amount in text-5xl font-bold tabular-nums, starts at "$0", scale-in animation on digit entry
  - Quick-select chips (mt-4, centered, gap-2): "$50", "$100", "$500" as rounded-full pills with accent border on active
  - NumPad component (mt-4): 4×3 grid, w-16 h-16 rounded-full surface-light buttons, digits 1-9, ".", 0, ⌫, whileTap scale 0.9, max 2 decimal places
  - Fee breakdown (mt-4): "Fee" showing 1% of amount, "Buying power after fee" showing amount minus fee
  - CTA: Primary Button "Fund $X.XX" — dynamic text, disabled at $0 (opacity-50), tap triggers 1s loading then navigates to 'home' with success toast "Account funded: +$X.XX"
  - No BottomNav on this screen
- Create `NumPad` component (`src/components/NumPad.tsx`) — reusable 4×3 numeric keypad with digit, decimal, and backspace buttons
- Wire both screens into the screen router in `page.tsx` for `screen === 'deposit'` and `screen === 'deposit-amount'`

**Stablecoin note:** The platform supports mantraUSD (default), USDC, and USDT. In V1, all amounts display in USD and stablecoin conversion is handled behind the scenes. Stablecoin selection is deferred to a future version.

## Capabilities

### New Capabilities
- `deposit-screen`: DepositScreen component with method selection cards, crypto transfer bottom sheet, and entrance animations
- `deposit-amount-screen`: DepositAmountScreen component with amount display, quick-select chips, fee breakdown, and CTA
- `num-pad`: Reusable NumPad component with 4×3 grid, decimal support, backspace, and press animations

### Modified Capabilities

## Impact

- Adds 3 new files: `src/components/screens/DepositScreen.tsx`, `src/components/screens/DepositAmountScreen.tsx`, `src/components/NumPad.tsx`
- Updates `page.tsx` screen router to render DepositScreen for 'deposit' and DepositAmountScreen for 'deposit-amount'
- Depends on: PhoneFrame, StatusBar, Card, Button, Zustand store (from core-components change)
- Connects from: onboarding-youre-in (via 'youre-in' → 'deposit') and home screen (via deposit action)
- Connects to: home screen (after successful deposit)
