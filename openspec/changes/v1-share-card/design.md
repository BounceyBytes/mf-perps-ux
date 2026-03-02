## Context

The portfolio-screen and trade-confirmation changes provide the context where a user has an open (and potentially winning) position. The share-card overlay gives users a way to celebrate a win and share it socially with a branded card that includes their PnL, a referral link, and a QR code. The core-components change provides PhoneFrame, Button, Zustand store, and mock data that this overlay depends on.

## Goals / Non-Goals

**Goals:**
- A full-screen overlay with `bg-black/80` backdrop covering the phone frame, dismissable via "Done" link
- A centered, polished share card (max-w-[320px], rounded-2xl) with gradient background and a green top accent bar
- Position data displayed prominently: emoji + pair/direction, hero PnL percentage, dollar breakdown
- User info section with avatar circle and name
- Referral area with CTA text, referral link, and QR code placeholder
- "Share" primary button and "Save Image" secondary button below the card
- "Done" text link centered below buttons to dismiss the overlay
- Card entrance animation via Framer Motion (scale + opacity)
- Prototype-only share/save — just show toasts

**Non-Goals:**
- No actual image generation or canvas rendering — prototype only
- No real share sheet integration (Web Share API) — prototype toast only
- No dynamic QR code generation — static placeholder box
- No red/loss variant styling in this change — green/winning only for v1
- No swipe or drag-to-dismiss gesture — "Done" link and backdrop are sufficient

## Decisions

1. **Full-screen overlay, not bottom sheet** — A share card is a moment of pride; it deserves the full screen. The dark backdrop (`bg-black/80`) creates a dramatic reveal and focuses attention entirely on the card.
2. **Gradient background on card** — Linear gradient from surface (#14141F) to purple-tinted dark (#1a1530) adds depth and premium feel without being distracting. Keeps the dark theme while adding visual interest.
3. **Top accent bar (4px, green gradient)** — Quick visual signal of a winning position. Uses green accent gradient matching the app's success color. Width spans the full card; sits above the rounded content area inside overflow-hidden.
4. **Hero PnL at text-4xl** — The percentage gain is the emotional core of the card. Making it the largest element ensures it reads immediately in screenshots and social shares.
5. **Dollar breakdown below PnL** — "$500 → $735.00" grounds the abstract percentage in real dollar terms. Secondary size (text-sm text-secondary) keeps hierarchy clear.
6. **User info section** — 24px avatar circle (bg-accent, initials or placeholder) + user name (text-xs). Creates personal ownership of the result. Kept small to not compete with PnL.
7. **Divider before referral** — `border-t border-[#2A2A3A]` with mt-4 separates the personal result from the referral CTA. Standard pattern for "above the fold" vs. "call to action" separation.
8. **Referral area with QR placeholder** — "Trade on MF Perps" (text-sm font-semibold) + referral link (text-xs text-accent) + 64×64 QR placeholder box. The QR placeholder is a rounded-lg surface-light box — real QR generation is out of scope for the prototype.
9. **Scale + opacity entrance** — Card animates from scale 0.8 + opacity 0 to scale 1 + opacity 1 with spring transition. Creates a satisfying "pop" reveal. Simpler than slide-up and more appropriate for a centered card.
10. **Share and Save show toasts** — Prototype behavior: tapping "Share" shows a toast "Shared!", tapping "Save Image" shows "Saved!". No real functionality. Toasts can use the store's toast mechanism or a simple inline state.
11. **"Done" as text link, not button** — A muted text link (text-sm text-muted) to dismiss keeps visual priority on the Share/Save buttons. Centered below the button group.
12. **Hardcoded winning position data** — For the prototype, the card displays hardcoded values (BTC Long, +47.2%, $500 → $735.00, Jake, JAKE2026). Future changes can wire this to actual position data from the store.

## Risks / Trade-offs

- [No real share/save functionality] → Users tapping Share or Save see only a toast. Acceptable for prototype — validates layout and flow.
- [Hardcoded data only] → Card always shows the same BTC Long +47.2% result regardless of actual positions. Acceptable for prototype — the visual design is what's being validated.
- [No loss variant] → If user has a losing position, the card still shows green. A future change could add red styling for negative PnL.
- [QR code is a placeholder box] → No actual scannable QR code. Acceptable for prototype — demonstrates the intended layout.
- [No backdrop tap dismiss] → Only "Done" link dismisses. Could add backdrop tap dismiss later, but "Done" is sufficient and more intentional for a share flow (prevents accidental dismissal while admiring the card).
