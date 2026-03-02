## Context

All screens, flows, and overlays for the MF Perps V1 prototype are built. The app is functional — users can tap through onboarding, view markets, open trades, manage positions, deposit, and withdraw. But every screen change is an instant cut. Numbers appear statically. Buttons have no tactile response. There is no feedback when actions complete. This final polish pass adds the motion and interaction layer that makes the prototype feel like a real mobile trading app.

## Goals / Non-Goals

**Goals:**
- Smooth, categorized screen transitions (slide, crossfade, slide-up) that match the mental model of each navigation type
- Toast notification system for action confirmations (deposit funded, position closed, etc.)
- Animated number countups on dollar amounts and percentages for a dynamic, live feel
- Micro-interactions on buttons (press scale, hover brightness) for tactile feedback
- Loading spinners on async-simulated actions (KYC verification, deposit confirmation)
- Proper scroll containment so the phone frame doesn't bounce the outer page

**Non-Goals:**
- No new screens or flows — only polish on existing ones
- No gesture-based navigation (swipe between screens)
- No skeleton loading screens or shimmer placeholders
- No sound effects or haptic feedback
- No changes to layout, spacing, or visual design of existing screens

## Decisions

1. **AnimatePresence with mode="wait"** — Ensures the exiting screen fully animates out before the entering screen animates in. Prevents layout flash from two screens rendering simultaneously.
2. **Three transition categories** — Onboarding slides right (progressive flow), tabs crossfade (lateral navigation), modals slide up (temporary overlay from bottom). This matches iOS conventions and user mental models.
3. **Toast at top of phone frame** — Positioned below the status bar, inside PhoneFrame, using fixed positioning with z-50. Top placement avoids conflict with BottomNav and CTA buttons at the bottom.
4. **useSpring for number animations** — Framer Motion's useSpring provides a natural deceleration curve for counting animations. 500ms duration with default spring config. tabular-nums prevents layout shift as digits change.
5. **Zustand for toast state** — showToast(message) sets the toast string and schedules a setTimeout to clear it after 2.5s. Simple, no external toast library needed.
6. **Loading state is local component state** — The Loader2 spinner on KYC and deposit CTAs uses local useState/setTimeout, not Zustand. These are transient UI states that don't need global visibility.
7. **whileTap on all buttons** — Applied at the Button component level so every button in the app gets press feedback automatically. scale(0.97) is subtle enough to feel responsive without being distracting.

## Risks / Trade-offs

- [AnimatePresence may conflict with existing overlay animations] → Overlays already have their own motion.div wrappers. Screen transitions only wrap the screen content, not the overlay layer. Keep them separate.
- [Number animation on every mount may feel repetitive] → Only animate on initial screen mount, not on re-renders within the same screen. Use a key tied to screen state.
- [Toast auto-dismiss timing] → 2.5s is standard for success toasts. If multiple toasts fire in quick succession, the latest one wins (overwrite pattern, not queue).
- [Performance on lower-end devices] → All animations use transform/opacity only (GPU-composited). No layout-triggering properties animated. Framer Motion handles will-change automatically.
