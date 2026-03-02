## Context

The KYC screen navigates to 'referral' after the verification loading animation completes. The referral screen is Screen 03 in the onboarding flow: Welcome → KYC → Referral → You're In. It renders inside PhoneFrame at `store.screen === 'referral'`. The screen is an optional step — users can skip it entirely — so the design must make the Skip action visually obvious rather than hidden. This is a clickable prototype; no real referral validation occurs.

## Goals / Non-Goals

**Goals:**
- A clean, focused single-input screen that renders inside PhoneFrame with code-entry styling
- Clear incentive copy ("You'll both earn trading rewards") to motivate code entry
- Obvious Skip path — not tucked away or de-emphasized beyond readability
- Green checkmark animation on valid code submission for satisfying feedback
- Smooth slide-in entrance animation consistent with the KYC screen transition
- No BottomNav visible on this screen

**Non-Goals:**
- No real referral code validation or API calls (prototype only — any non-empty string is "valid")
- No error states or invalid-code messaging
- No keyboard handling beyond native HTML input behavior
- No persistence of the entered referral code

## Decisions

1. **Single ReferralScreen component** — All layout, input, animations, and navigation in one file. No sub-components needed for a screen this simple.
2. **Reuse Input component with className override** — The base Input component gets `text-center text-xl tracking-widest` to create the code-entry aesthetic. No new Input variant needed.
3. **Green checkmark via Framer Motion scale animation** — A Check icon (Lucide) in green, animated from scale 0 to scale 1 over ~300ms. Placed adjacent to the input field. After 500ms total, navigate to 'youre-in'.
4. **Skip as styled text link, not a Button** — "Skip" is rendered as a `<button>` with text-secondary, underline, and centered styling below the Continue button. This keeps it visually distinct from the primary CTA while still being obviously tappable.
5. **Empty input + Continue = immediate navigation** — Treated identically to Skip. No error state, no prompt to "enter a code first". The screen is fully optional.
6. **maxLength 12 on input** — Prevents excessively long input. Purely cosmetic constraint for prototype aesthetics.

## Risks / Trade-offs

- [No real validation means any text triggers the checkmark] → Acceptable for prototype. Real validation would happen at the API layer in production.
- [Skip as underline text rather than a secondary button] → Matches the design spec. If users miss it, the Continue button with empty input achieves the same outcome.
- [500ms delay after checkmark before navigation] → Brief enough to feel responsive, long enough to register the animation. Could feel slow if users are impatient, but it's a one-time flow.
