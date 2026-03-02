## Context

The trade-screen change provides the trading interface where users pick direction, set amount and leverage, and tap the CTA to open a position. That CTA calls `store.showOverlay('trade-confirmation')`. This change builds the overlay that appears in response — a bottom sheet confirming the position was opened and offering next steps. The core-components change provides PhoneFrame, Button, Card, Zustand store, and mock data that this overlay depends on.

## Goals / Non-Goals

**Goals:**
- A bottom sheet overlay that slides up from the bottom with Framer Motion spring animation
- Semi-transparent backdrop (`bg-black/50`) that dismisses the sheet on tap
- Drag handle bar for visual affordance and swipe-down-to-dismiss gesture
- Green CheckCircle2 icon that scales in with spring animation for satisfying feedback
- "Position Opened" heading that fades in after the icon
- Summary Card reflecting actual trade parameters (pair, direction, amount, leverage, entry price)
- Three clearly prioritized action buttons: View Position (primary), Trade Again (secondary), Set TP/SL (secondary placeholder)
- Wire into the overlay layer in `page.tsx`

**Non-Goals:**
- No actual position creation or persistence — this is a prototype confirmation
- No take-profit / stop-loss functionality behind the "Set TP/SL" button — placeholder only
- No haptic feedback or sound effects
- No share functionality in this change (share-card is a separate change)
- No animation on the summary card content itself — only the icon and heading animate

## Decisions

1. **Bottom sheet, not full-screen modal** — A bottom sheet feels lighter and faster, appropriate for a confirmation moment. Max height 50% keeps the trade screen visible behind the backdrop, reinforcing context.
2. **Spring animation for slide-up** — `y: "100%" → 0` with spring type and damping ~25 creates a natural, satisfying entrance. Matches iOS bottom sheet conventions.
3. **Backdrop tap dismisses** — Standard UX pattern. Users expect tapping outside a sheet to close it.
4. **Swipe-down to dismiss with 100px threshold** — Framer Motion `drag="y"` with `dragConstraints={{ top: 0 }}`. If `dragY > 100` on release, dismiss. Prevents accidental dismissal from small drags.
5. **CheckCircle2 from Lucide, 48px, green** — Large enough to feel celebratory. Green (#00D68F) matches the "success" color used throughout the app. Spring scale-in (0 → 1) with slight overshoot for delight.
6. **Staggered entrance: icon first, then text** — Icon scales in immediately, heading fades in with 200ms delay. Creates a cinematic "reveal" moment without feeling slow.
7. **Summary card uses actual trade params** — Reads from store (selectedPair, direction, amount, leverage) rather than hardcoded values. Shows "BTC Long $500 @ 10x" and "Entry: $67,156" so the user sees exactly what was confirmed.
8. **Three buttons in vertical stack** — View Position is primary (accent bg), Trade Again and Set TP/SL are secondary (surface-light bg). Vertical stack with gap-3 for easy thumb reach on the bottom sheet.
9. **"View Position" navigates to portfolio** — Calls `navigate('portfolio')` then `dismissOverlay()`. Most valuable post-trade action.
10. **"Set TP/SL" is a no-op placeholder** — Shows the button to validate the UX flow. Real implementation comes in a future change.
11. **Drag handle bar** — `w-10 h-1 rounded-full bg-[#2A2A3A]` centered at top of sheet. Visual cue that the sheet is draggable.

## Risks / Trade-offs

- [Trade params may not be in store yet] → If store doesn't hold last trade params, we can pass them as props or store them when CTA is tapped. For the prototype, storing `lastTrade` in the Zustand store on CTA tap is simplest.
- [Swipe-down gesture may conflict with scroll] → Sheet content is short enough (max 50% height) that scrolling shouldn't be needed. If content grows, would need to disable drag when scrolled.
- [Spring animation may feel slow on low-end devices] → Spring with damping 25 and stiffness 300 completes quickly. Acceptable for prototype.
- [Set TP/SL button does nothing] → Users may tap it expecting functionality. Acceptable for prototype — validates button placement and flow.
