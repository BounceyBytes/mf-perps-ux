## Context

The deposit flow and portfolio screen are already implemented. Users can fund their accounts and view open positions with P&L. The withdraw screen (Screen 12) completes the funds lifecycle by letting users pull money out. In the real product, withdrawals would go through blockchain transactions or fiat off-ramps with compliance checks. For the V1 prototype, external wallet is the only destination — a single card with an expandable address input and a confirm button. No real transactions occur; the flow simulates processing with a loading state and navigates back to portfolio with a success toast.

## Goals / Non-Goals

**Goals:**
- Single-screen withdraw flow with pre-filled max amount
- Available balance displayed prominently
- Quick-select percentage chips (25%, 50%, Max) for fast amount selection
- "Max" chip active by default, pre-filling the full available balance
- Single destination option: External Wallet card with accent border and checkmark
- Tapping the wallet card expands an address input with a paste button and "Confirm Withdraw" CTA
- No separate bottom CTA — the confirm button lives inside the expanded wallet card section
- Loading state (1.5s) on confirm → navigate to portfolio with success toast
- No BottomNav on this screen

**Non-Goals:**
- No fiat off-ramps (bank transfer, debit card cashout) — V1 is external wallet only
- No real blockchain transaction submission
- No wallet address validation or ENS resolution
- No minimum/maximum withdrawal limits
- No withdrawal fee calculation
- No withdrawal history or pending status tracking
- No multi-step approval or 2FA confirmation

## Decisions

1. **Single screen instead of multi-step flow** — Unlike deposits which have method selection then amount entry, withdrawals have only one destination (external wallet in V1). Combining amount selection and destination into one screen reduces friction.
2. **Pre-filled max amount** — Users withdrawing usually want the full balance. Starting at max with "Max" chip active saves a tap for the most common case. Users can select 25% or 50% if they want a partial withdrawal.
3. **Percentage chips instead of dollar amounts** — Unlike deposit chips ($50, $100, $500) which are absolute, withdrawal chips are relative to the current balance. Percentages (25%, 50%, Max) make more sense because the available balance varies.
4. **Single destination card with expand-to-input pattern** — Instead of navigating to a separate screen for address entry, tapping the wallet card expands it inline to reveal the input field and confirm button. This keeps the user on one screen and makes the flow feel fast.
5. **No separate bottom CTA** — The "Confirm Withdraw" button appears only after the wallet card is expanded. This prevents users from trying to confirm without entering an address. The button is contextually placed next to the input.
6. **1.5s loading instead of 1s** — Withdrawals feel like a more consequential action than deposits. The slightly longer loading time (1.5s vs 1s for deposits) communicates that something important is happening.
7. **Back navigates to portfolio, not home** — Users access withdraw from the portfolio screen, so back returns there. This maintains the navigation mental model.
8. **V1 external wallet only** — Fiat off-ramps require payment provider integration and compliance work. The prototype validates the withdrawal UX pattern with the simplest case (crypto to external wallet). Additional methods can be added later as separate cards, similar to how the deposit screen has multiple method cards.
9. **Accent border and checkmark on wallet card** — Since there's only one destination option in V1, the card is always "selected." The accent border and checkmark reinforce this state and maintain visual consistency with the selection patterns used elsewhere in the app.
10. **AnimatePresence for expand/collapse** — The address input section animates in/out when the wallet card is tapped. This avoids a jarring layout shift and keeps the single-screen flow feeling smooth.

## Risks / Trade-offs

- [Only one destination option looks sparse] → Acceptable for V1. The "Withdraw to:" label and card pattern establish the UI framework for adding fiat off-ramp cards later. The single card with accent border and checkmark looks intentional, not empty.
- [No wallet address validation means users can type anything] → Acceptable for prototype. The input field is visual only. In production, validation would check for valid blockchain addresses and possibly ENS resolution.
- [Pre-filling max could lead to accidental full withdrawals] → Mitigated by the two-step interaction: user must tap the wallet card to expand, then tap "Confirm Withdraw." Two deliberate taps reduce accidental full withdrawals.
- [No withdrawal fees shown] → In V1, the prototype doesn't model fees. When real transactions are integrated, a fee breakdown similar to the deposit flow's fee section should be added.
- [Toast message shows static amount] → The toast displays the amount at confirmation time. If the balance changes between screen load and confirmation (not possible in prototype, but possible in production), the amount shown could be stale. Acceptable for prototype.
