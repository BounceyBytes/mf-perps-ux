## 1. NumPad Component

- [ ] 1.1 Create `src/components/NumPad.tsx` accepting `onDigit` (string callback), `onDecimal` (callback), and `onBackspace` (callback) props
- [ ] 1.2 Render a 4×3 grid layout: Row 1 (1, 2, 3), Row 2 (4, 5, 6), Row 3 (7, 8, 9), Row 4 (".", 0, ⌫)
- [ ] 1.3 Style each button as w-16 h-16 rounded-full surface-light (#1E1E2E) bg with text-xl white text, centered in a grid with consistent gap spacing
- [ ] 1.4 Wire digit buttons (0-9) to call `onDigit` with the digit string, "." to call `onDecimal`, and ⌫ to call `onBackspace`
- [ ] 1.5 Add Framer Motion `whileTap={{ scale: 0.9 }}` to all NumPad buttons
- [ ] 1.6 Center the NumPad grid horizontally with mt-4 top margin

## 2. DepositScreen Component

- [ ] 2.1 Create `src/components/screens/DepositScreen.tsx` with px-6 pt-4 layout
- [ ] 2.2 Add header: ArrowLeft icon (tappable → `store.navigate('home')`) + "Fund Account" centered in text-lg font-semibold
- [ ] 2.3 Add "Transfer Crypto" method card (mt-6): Wallet icon (Lucide) left, "Transfer Crypto" name + "From another wallet" timing center, ChevronRight right — tappable → open bottom sheet (fiat on-ramps Debit Card and Apple Pay are deferred to V5)
- [ ] 2.4 Implement bottom sheet overlay for Transfer Crypto: QR code placeholder (gray rounded square), mock wallet address (e.g., "0x1a2B...9fEd"), dismiss on tap outside or close button
- [ ] 2.5 Wrap method cards in Framer Motion stagger: each card animates from opacity 0, y:20 to opacity 1, y:0 with stagger delay

## 3. DepositAmountScreen Component

- [ ] 3.1 Create `src/components/screens/DepositAmountScreen.tsx` with px-6 flex column layout
- [ ] 3.2 Add header: ArrowLeft icon (tappable → `store.navigate('deposit')`) + "Fund Account" centered in text-lg font-semibold
- [ ] 3.3 Add amount display: "$" in text-2xl text-secondary + amount value in text-5xl font-bold tabular-nums, centered, initial value "0"
- [ ] 3.4 Add Framer Motion scale-in animation on amount display: scale 1.0→1.05→1.0 on each digit entry
- [ ] 3.5 Add quick-select chips (mt-4, centered, gap-2): "$50", "$100", "$500" as rounded-full pills — active chip (matching current amount) gets accent border (#7B61FF), tapping sets the amount
- [ ] 3.6 Add NumPad component (mt-4) and wire callbacks: `onDigit` appends digit, `onDecimal` adds ".", `onBackspace` removes last character — enforce max 2 decimal places and prevent multiple decimals
- [ ] 3.7 Add fee breakdown section (mt-4): "Fee" row showing 1% of amount, "Buying power after fee" row showing amount minus fee, both in text-sm with flex justify-between
- [ ] 3.8 Add CTA button (full-width, primary): dynamic text "Fund $X.XX", disabled with opacity-50 when amount is 0
- [ ] 3.9 Wire CTA tap: show loading spinner on button for 1 second, then call `store.navigate('home')` and trigger success toast "Account funded: +$X.XX"

## 4. App Shell Wiring

- [ ] 4.1 Add DepositScreen to the screen router in `page.tsx` so it renders when `store.screen === 'deposit'`
- [ ] 4.2 Add DepositAmountScreen to the screen router in `page.tsx` so it renders when `store.screen === 'deposit-amount'`
- [ ] 4.3 Confirm BottomNav is not rendered when screen is 'deposit' or 'deposit-amount'

## 5. Verification

- [ ] 5.1 Run the app and confirm DepositScreen renders inside PhoneFrame with header and method card(s) staggering in
- [ ] 5.2 Tap "Transfer Crypto" and confirm bottom sheet appears with QR placeholder and mock address
- [ ] 5.3 On DepositAmountScreen, tap NumPad digits and confirm amount display updates with scale animation
- [ ] 5.4 Tap quick-select chips ($50, $100, $500) and confirm amount and active chip update correctly
- [ ] 5.5 Confirm max 2 decimal places and no multiple decimals enforced
- [ ] 5.6 Confirm fee breakdown updates dynamically (1% fee, buying power = amount - fee)
- [ ] 5.7 Confirm CTA shows "Fund $0.00" disabled at $0, and "Fund $150.00" enabled at $150
- [ ] 5.8 Tap CTA and confirm 1s loading → navigate to home → success toast appears
- [ ] 5.9 Tap back arrows and confirm correct navigation (deposit-amount → deposit, deposit → home)
