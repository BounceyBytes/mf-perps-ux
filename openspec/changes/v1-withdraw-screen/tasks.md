## 1. WithdrawScreen Component — Layout & Header

- [ ] 1.1 Create `src/components/screens/WithdrawScreen.tsx` with px-6 pt-4 layout
- [ ] 1.2 Add header: ArrowLeft icon (tappable → `store.navigate('portfolio')`) + "Withdraw" centered in text-lg font-semibold
- [ ] 1.3 Add available balance display (mt-2, centered): "Available: $512.80" in text-sm text-secondary

## 2. WithdrawScreen Component — Amount & Chips

- [ ] 2.1 Add large amount display (mt-4, centered): "$512.80" in text-4xl font-bold text-primary, initialized to max available balance
- [ ] 2.2 Add quick-select chips (mt-3, centered, gap-2): "25%", "50%", "Max" as rounded-full pills — "Max" active by default with accent border (#7B61FF)
- [ ] 2.3 Wire chip tap handlers: 25% sets amount to $128.20, 50% sets amount to $256.40, Max sets amount to $512.80 — active chip gets accent border, others reset to default style
- [ ] 2.4 Ensure large amount display updates dynamically when chips are tapped

## 3. WithdrawScreen Component — Destination Card & Address Input

- [ ] 3.1 Add "Withdraw to:" label (mt-6): text-xs uppercase tracking-wider text-muted
- [ ] 3.2 Add External Wallet destination card (mt-2): Wallet icon (Lucide) left, "External Wallet" name + "Paste or select wallet address" text-xs text-secondary + "Instant" text-xs text-muted, accent border (#7B61FF), checkmark icon (Check from Lucide) on the right
- [ ] 3.3 Wire wallet card tap to toggle expanded state for address input section
- [ ] 3.4 Implement expanded section with AnimatePresence: text input field (placeholder "Enter wallet address") + paste button alongside the input + "Confirm Withdraw" primary button below — section animates from height 0 / opacity 0 to full height / opacity 1
- [ ] 3.5 Wire paste button to populate input with mock address "0x1a2B3c4D5e6F7a8B9c0D1e2F3a4B5c6D7e8F9a"

## 4. WithdrawScreen Component — Confirm Flow

- [ ] 4.1 Wire "Confirm Withdraw" button tap: show loading spinner on button for 1.5 seconds
- [ ] 4.2 After loading completes: call `store.navigate('portfolio')` and trigger success toast "Withdrawal initiated — $X.XX" with the current withdraw amount
- [ ] 4.3 Ensure toast auto-dismisses after ~3 seconds (using existing store toast mechanism)

## 5. App Shell Wiring

- [ ] 5.1 Add WithdrawScreen to the screen router in `page.tsx` so it renders when `store.screen === 'withdraw'`
- [ ] 5.2 Confirm BottomNav is not rendered when screen is 'withdraw'

## 6. Verification

- [ ] 6.1 Run the app and confirm WithdrawScreen renders inside PhoneFrame with header, balance, amount display, chips, and wallet card
- [ ] 6.2 Confirm "Max" chip is active by default and amount shows "$512.80"
- [ ] 6.3 Tap "25%" chip and confirm amount updates to "$128.20" with accent border on 25% chip
- [ ] 6.4 Tap "50%" chip and confirm amount updates to "$256.40" with accent border on 50% chip
- [ ] 6.5 Tap "Max" chip and confirm amount returns to "$512.80" with accent border on Max chip
- [ ] 6.6 Tap External Wallet card and confirm address input section expands with AnimatePresence animation
- [ ] 6.7 Tap paste button and confirm mock address populates the input field
- [ ] 6.8 Tap "Confirm Withdraw" and confirm 1.5s loading spinner → navigate to portfolio → success toast "Withdrawal initiated — $512.80" appears
- [ ] 6.9 Tap back arrow and confirm navigation to portfolio screen
- [ ] 6.10 Confirm BottomNav is not visible on the withdraw screen
