## Context

The core-components change established the app shell (PhoneFrame, StatusBar, BottomNav, Zustand store, Button, Card). The onboarding flow (welcome → KYC → you're-in) brings users to the point of having an account. The referral screen is deferred to V3 — see [plan-v3-referral-program.md](../../plan-v3-referral-program.md). The deposit flow is the next step — before users can trade, they need funds. Screen 06 (Deposit Method Selection) and Screen 07 (Deposit Amount Entry) form a two-step funding flow that bridges onboarding to the trading experience. This is a clickable prototype — no real payment processing or blockchain transactions occur.

## Goals / Non-Goals

**Goals:**
- A two-screen deposit flow: method selection → amount entry
- One funding method for V1: Transfer Crypto (from external wallet)
- Fiat on-ramps (Debit Card, Apple Pay) are deferred to V5 — see [plan-v5-fiat-integrations.md](../../plan-v5-fiat-integrations.md)
- Custom NumPad component for precise amount entry without native keyboard
- Quick-select chips for common deposit amounts ($50, $100, $500)
- Fee transparency: show 1% fee and resulting buying power before confirming
- Dynamic CTA that reflects the exact deposit amount
- Loading state on CTA → navigate to home with success toast
- Smooth entrance animations and press feedback via Framer Motion
- No BottomNav on either deposit screen

**Non-Goals:**
- No real payment processing (Stripe, Apple Pay SDK, etc.) — fiat on-ramps (Debit Card, Apple Pay) are deferred to V5
- No real crypto deposit address or QR code scanning
- No KYC re-verification for high amounts
- No minimum/maximum deposit validation
- No currency selection (USD only)
- No deposit history or transaction tracking

**Stablecoin context:** The platform supports three stablecoins: **mantraUSD** (our default stablecoin), **USDC**, and **USDT**. In the V1 prototype, all amounts are displayed in USD. Stablecoin conversion is handled behind the scenes — users deposit in any supported stablecoin and see their balance in USD equivalent. The deposit screen does not expose stablecoin selection in V1; this is a future enhancement.

## Decisions

1. **Two-screen flow instead of single screen** — Method selection and amount entry are distinct steps. Keeps each screen focused. Method selection is a quick routing decision; amount entry requires concentration with the NumPad.
2. **Custom NumPad instead of native keyboard** — Native keyboards are inconsistent across devices and don't match the dark UI aesthetic. A custom NumPad gives full control over styling, layout, and animation. It also prevents the viewport shift that native keyboards cause.
3. **NumPad as a separate reusable component** — Extracted to `src/components/NumPad.tsx` so it can be reused in withdraw flows or anywhere else that needs numeric input. Accepts `onDigit`, `onDecimal`, `onBackspace` callbacks.
4. **1% fee model** — Simple, transparent fee structure. Fee = 1% of amount. Buying power = amount − fee. Displayed before confirming so users aren't surprised.
5. **Quick-select chips for speed** — $50, $100, $500 cover common deposit amounts. One tap sets the amount. Active chip gets accent border. Tapping a chip also updates the NumPad display.
6. **Back arrow context-dependent** — On DepositScreen, back goes to 'home' (if user came from home) or 'youre-in' (if user came from onboarding). In the prototype, we default to navigating to 'home' since the store tracks the previous screen. On DepositAmountScreen, back always goes to 'deposit'.
7. **Transfer Crypto opens a bottom sheet, not a new screen** — A simple sheet with a QR placeholder and mock address is sufficient. No need for a full screen since there's no interactive flow — user just copies the address and deposits externally.
8. **CTA loading simulates processing** — 1-second loading spinner on button tap simulates payment processing, then navigates to 'home' and shows a success toast. Gives the feel of a real transaction without backend integration.
10. **Scale-in animation on amount display** — Subtle scale pulse on each digit entry gives tactile feedback that the input registered. Keeps the large amount display feeling responsive.

## Risks / Trade-offs

- [Back arrow on DepositScreen depends on navigation history] → For the prototype, default to navigating to 'home'. If the store already tracks previous screen, use that. Otherwise, hardcode 'home' and revisit when flow branching is needed.
- [No real payment processing means the deposit demo is purely visual] → Acceptable for UX prototype. Validates the flow and interaction patterns before integrating real payment rails.
- [1% fee is a placeholder] → Real fee structure will depend on payment provider and regulatory requirements. The UX pattern (showing fee + buying power) is what matters for validation.
- [Custom NumPad may not handle edge cases (e.g., leading zeros, multiple decimals)] → Enforce max 2 decimal places, prevent multiple decimal points, and strip leading zeros in the handler logic.
