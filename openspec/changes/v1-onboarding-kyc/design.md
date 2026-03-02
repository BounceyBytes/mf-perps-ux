## Context

The onboarding-welcome change established the Welcome screen as the first screen in the user journey. After any auth action on the Welcome screen, the user navigates to the KYC screen (`store.screen === 'kyc'`). This is Screen 02 in the onboarding flow. It renders inside PhoneFrame and presents the two verification steps (ID scan and selfie) before letting the user proceed to the "You're In" confirmation screen. This is a clickable prototype — no real KYC/identity verification occurs. The referral code screen is deferred to V3 — see [plan-v3-referral-program.md](../../plan-v3-referral-program.md).

## Goals / Non-Goals

**Goals:**
- A polished KYC screen that renders inside PhoneFrame with back navigation, heading, step cards, trust badge, and CTA
- Back arrow navigates to 'welcome' screen
- "Start verification" button shows a loading spinner for 1.5s then navigates to 'youre-in'
- Slide-in entrance animation from the right using Framer Motion
- Communicate trust and security via copy and visual cues (lock icon, encryption text)
- No BottomNav visible on this screen

**Non-Goals:**
- No real identity verification or document scanning
- No camera access or image capture
- No form validation or error states
- No dark/light theme toggle (dark mode only)
- Step cards are not tappable individually (CTA handles progression)

## Decisions

1. **Single KycScreen component** — All layout, cards, trust badge, and animations in one file. Complexity is low enough that sub-components aren't warranted.
2. **Step cards as styled divs, not interactive** — The two step cards (Scan ID, Take selfie) are informational only. They show what the verification involves but don't navigate anywhere independently. Only the CTA button advances the flow.
3. **Simulated loading state on CTA** — Button shows Loader2 spinning icon for 1.5s via `setTimeout`, then calls `store.navigate('youre-in')`. Uses local React state (`isLoading`) to toggle between button text and spinner.
4. **Lucide icons only** — ChevronLeft (back), FileText (ID step), Camera (selfie step), Lock (trust badge), ChevronRight (card affordance), Loader2 (spinner). No custom SVGs needed.
5. **Slide-in from right** — Content animates `x: 30 → 0` with `opacity: 0 → 1` to convey forward navigation flow. Consistent with the left-to-right onboarding progression.
6. **Trust badge pushed to bottom via mt-auto** — Flex layout with mt-auto on the trust section ensures it sits above the CTA regardless of content height.

## Risks / Trade-offs

- [Step cards are not tappable] → Acceptable for prototype. A real app might deep-link each step to its own sub-flow, but the prototype keeps the flow linear.
- [1.5s hard-coded loading delay] → Simulates real verification latency. Acceptable for demo purposes. A real integration would await an API response.
- [No error or retry state on CTA] → Out of scope for prototype. The button always succeeds after the delay.
- [All Lucide icons imported individually] → Tree-shaking keeps bundle size minimal. No concern for a prototype.
