## Context

The onboarding flow is: Welcome → KYC → You're In. The KYC screen collects identity verification; once complete, the user lands on this confirmation screen. It renders inside the PhoneFrame at `store.screen === 'youre-in'`. This is the last step before the user enters the main app — they can proceed to deposit funds or explore markets. This is a clickable prototype; no real account state is involved.

## Goals / Non-Goals

**Goals:**
- A celebratory confirmation screen that renders inside PhoneFrame with a check icon, heading, and two CTAs
- "Fund Account & Trade" routes to the deposit flow; "Explore Markets" routes to the home screen
- Smooth entrance animations — spring-animated check icon and staggered buttons
- No BottomNav visible on this screen

**Non-Goals:**
- No real account or KYC state validation (prototype only — screen is statically rendered)
- No dark/light theme toggle (dark mode only)
- No loading states or conditional rendering based on KYC completion
- No confetti or particle effects (keep it clean and performant)

## Decisions

1. **Single YoureInScreen component** — All layout, icon, heading, buttons, and animations in one file. No sub-components needed for a simple confirmation screen.
2. **CheckCircle2 from Lucide** — Consistent with the icon library already used across the project. No custom SVG needed.
3. **Spring animation for check icon** — A spring with stiffness: 200 gives a natural "pop-in" feel that communicates success. Scale 0→1 is more celebratory than a simple fade.
4. **Two distinct button styles** — Primary (accent bg) for the high-intent action (fund account), secondary (surface-light bg) for the exploratory action (markets). Clear visual hierarchy.
5. **300ms delay before buttons appear** — Lets the check icon land first, then reveals the CTAs. Keeps the animation sequence legible.

## Risks / Trade-offs

- [Spring animation stiffness is hardcoded] → Acceptable for prototype. Tokenizing animation configs is overkill at this stage.
- [No back navigation from this screen] → Intentional. Onboarding is a one-way funnel; going back to KYC doesn't make sense.
- [No conditional rendering based on KYC completion] → Out of scope for prototype. In production, this screen would gate on verified KYC status.
