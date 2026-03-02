# MF Perps V1 MVP — OpenSpec Build Plan

> Maps every feature in [plan-v1-mvp.md](plan-v1-mvp.md) into sequenced OpenSpec changes. Each change is a self-contained unit of work that can be proposed (`/opsx:propose`) and implemented (`/opsx:apply`) independently.

## Build Order & Dependencies

Changes are listed in dependency order. Later changes assume earlier ones are complete.

---

## Phase 1: Foundations

### Change 1: `v1-project-setup`
**What:** Initialize Next.js 14 project with all dependencies, design tokens, globals, Tailwind config, and base file structure.

**Covers (from plan):**
- Prompt 0 steps 1–4: project init, tokens, Tailwind theme, globals.css, Inter font
- Design tokens from build-v1-mvp.md (colors, typography, spacing, radius)

**Key deliverables:**
- Initialized Next.js project with TypeScript, Tailwind, Framer Motion, Lucide, Zustand
- `src/lib/tokens.ts` — design tokens as exported constants
- `src/app/globals.css` — Tailwind imports, Inter font, dark background, scrollbar hiding
- Tailwind config extended with custom theme (background, surface, surface-light, border, text-primary, text-secondary, text-muted, accent, green, red, yellow, orange)

**Dependencies:** None

---

### Change 2: `v1-core-components`
**What:** Build PhoneFrame, StatusBar, BottomNav, and base reusable components (Button, Card, Input).

**Covers (from plan):**
- Prompt 0 steps 7–11: Button (primary/secondary/ghost), Card, Input, PhoneFrame, StatusBar, BottomNav
- Zustand store with navigation state (`src/lib/store.ts`)
- Mock data (`src/lib/mock-data.ts`)
- App shell wiring in `src/app/page.tsx` (screen router, overlay layer, conditional BottomNav)

**Key deliverables:**
- `src/components/PhoneFrame.tsx` — 390×844 phone frame, centered, rounded corners, overflow scroll
- `src/components/StatusBar.tsx` — fake iOS status bar (9:41, signal, wifi, battery)
- `src/components/BottomNav.tsx` — Home/Trade/Portfolio tabs, active state, navigate on tap
- `src/components/Button.tsx` — primary (accent), secondary (surface-light), ghost variants with press animation
- `src/components/Card.tsx` — surface bg, rounded-2xl, p-4, border
- `src/components/Input.tsx` — surface-light bg, rounded-xl, accent focus ring
- `src/lib/store.ts` — Zustand store (screen, overlay, selectedPair, navigate, showOverlay, dismissOverlay)
- `src/lib/mock-data.ts` — markets, openPositions, user data
- `src/app/page.tsx` — PhoneFrame + screen router + overlay layer

**Dependencies:** `v1-project-setup`

---

## Phase 2: Onboarding

### Change 3: `v1-onboarding-welcome`
**What:** Build the Welcome/Sign Up screen (Screen 01).

**Covers (from plan):**
- Prompt 1: MF Perps logo, tagline, 3 auth buttons (Apple, Google, email/phone), sign-in link
- Framer Motion fade-in + staggered button entrance
- All auth buttons navigate to KYC screen

**Dependencies:** `v1-core-components`

---

### Change 4: `v1-onboarding-kyc`
**What:** Build the KYC identity verification screen (Screen 02).

**Covers (from plan):**
- Prompt 2: "Verify your identity" heading, two-step checklist (Scan ID, Take selfie), trust badge, "Start verification" CTA
- Loading spinner state (1.5s) then navigate to You're In screen
- Slide-in animation from right

**Dependencies:** `v1-core-components`

---

### Change 5: `v1-onboarding-youre-in`
**What:** Build the "You're all set" confirmation screen (Screen 03).

**Covers (from plan):**
- Prompt 3: Checkmark icon, "You're all set" heading, "Deposit & Trade" (→ deposit) and "Explore Markets" (→ home) CTAs
- Spring scale animation on checkmark, staggered button entrance

**Dependencies:** `v1-core-components`

---

## Phase 3: Core Loop

### Change 6: `v1-home-screen`
**What:** Build the Home / Markets discovery screen (Screen 05).

**Covers (from plan):**
- Prompt 5: MarketRow component, header with balance, Trending section, Watchlist, Top Movers horizontal scroll
- Tapping any market → trade screen with that pair selected
- Tapping balance → portfolio

**Key deliverables:**
- `src/components/MarketRow.tsx` — pair, price, 24h change, tap-to-trade
- `src/screens/05-Home.tsx` — full home screen layout

**Dependencies:** `v1-core-components`

---

### Change 7: `v1-trade-screen`
**What:** Build the Trade screen (Screen 08) — the most important screen in the app.

**Covers (from plan):**
- Prompt 8: Header with pair + price, chart placeholder with timeframe pills, Long/Short toggle, dollar amount input with chips, leverage slider, summary section (position size, liquidation, fee), dynamic CTA
- All values update reactively as user adjusts inputs
- CTA opens trade confirmation overlay

**Key deliverables:**
- `src/components/LeverageSlider.tsx` — custom slider with color zones (green/yellow/red)
- `src/screens/08-Trade.tsx` — full trade screen layout

**Dependencies:** `v1-core-components`

---

### Change 8: `v1-trade-confirmation`
**What:** Build the Trade Confirmation bottom sheet (Screen 09).

**Covers (from plan):**
- Prompt 9: Bottom sheet with spring animation, checkmark + "Position Opened", summary card, View Position / Trade Again / Set TP/SL buttons
- Swipe-down-to-dismiss, backdrop tap dismiss

**Dependencies:** `v1-trade-screen`

---

### Change 9: `v1-portfolio-screen`
**What:** Build the Portfolio screen (Screen 09).

**Covers (from plan):**
- Prompt 9: Portfolio header with total value + P&L, portfolio value chart (area chart with time-range pills and scrub), PositionCard components with health bars, available balance + deposit link, trade history
- P&L numbers animate on mount

**Key deliverables:**
- `src/components/PositionCard.tsx` — position with P&L, health bar, close button
- `src/components/HealthBar.tsx` — liquidation distance bar (green→yellow→red)
- `src/screens/10-Portfolio.tsx` — full portfolio layout

**Dependencies:** `v1-core-components`

---

### Change 10: `v1-close-position`
**What:** Build the Close Position bottom sheet (Screen 10).

**Covers (from plan):**
- Prompt 11: "Close BTC Long?" confirmation, P&L + receive amount, Close Full / Close Partial / Cancel
- Closing animates position out of portfolio, shows success toast

**Dependencies:** `v1-portfolio-screen`

---

## Phase 4: Money Flow

### Change 11: `v1-deposit-flow`
**What:** Build both Deposit screens — method selection (Screen 05) and amount entry (Screen 06).

**Covers (from plan):**
- Prompt 5: "Fund Account" heading, Transfer Crypto method card (fiat on-ramps deferred to V5), crypto transfer shows QR + address
- Prompt 6: NumPad component, large amount display, quick-select chips ($50/$100/$500), dynamic fee breakdown, "Fund $X" CTA with loading state, success toast

**Key deliverables:**
- `src/components/NumPad.tsx` — 4×3 number pad with press animations
- `src/screens/06-Deposit.tsx` — method selection
- `src/screens/07-DepositAmount.tsx` — amount entry with numpad

**Dependencies:** `v1-core-components`

---

### Change 12: `v1-withdraw-screen`
**What:** Build the Withdraw screen (Screen 11).

**Covers (from plan):**
- Prompt 11: "Withdraw" heading, available balance, large amount display, percentage chips (25%/50%/Max), external wallet destination card, expandable address input, confirm withdrawal with loading + success toast

**Dependencies:** `v1-core-components`

---

## Phase 5: Social

### Change 13: `v1-share-card`
**What:** Build the Share Card overlay (Screen 12).

**Covers (from plan):**
- Prompt 12: Full-screen overlay, branded position card with gradient, position P&L hero number, user info, branding area, Share / Save Image / Done buttons
- Card enters with scale + opacity animation

**Dependencies:** `v1-portfolio-screen`

---

## Phase 6: Polish

### Change 14: `v1-transitions-polish`
**What:** Add screen transitions, toast system, number animations, and micro-interactions across the entire prototype.

**Covers (from plan):**
- Prompt 14: AnimatePresence screen transitions (slide-right for onboarding, crossfade for tabs, slide-up for modals)
- Toast notification component (slide from top, auto-dismiss, green accent)
- Number count-up animations on dollar amounts and percentages
- Button micro-interactions (whileTap scale, hover brightness)
- Loading states on CTA buttons (spinner icon swap)
- PhoneFrame scroll behavior (overscroll-behavior, smooth scrolling)
- Demo flow starts at welcome, flows seamlessly through onboarding

**Key deliverables:**
- `src/components/Toast.tsx` — pill toast with auto-dismiss
- Toast state in Zustand store
- AnimatePresence wrappers in page.tsx
- Scroll and interaction polish across all screens

**Dependencies:** All previous changes

---

## Summary Table

| # | Change Name | Phase | Depends On | Screens/Components |
|---|---|---|---|---|
| 1 | `v1-project-setup` | Foundations | — | Project init, tokens, Tailwind, globals |
| 2 | `v1-core-components` | Foundations | 1 | PhoneFrame, StatusBar, BottomNav, Button, Card, Input, store, mock data, page.tsx |
| 3 | `v1-onboarding-welcome` | Onboarding | 2 | Screen 01 |
| 4 | `v1-onboarding-kyc` | Onboarding | 2 | Screen 02 |
| 5 | `v1-onboarding-youre-in` | Onboarding | 2 | Screen 03 |
| 6 | `v1-home-screen` | Core Loop | 2 | Screen 04, MarketRow |
| 7 | `v1-trade-screen` | Core Loop | 2 | Screen 07, LeverageSlider |
| 8 | `v1-trade-confirmation` | Core Loop | 7 | Screen 08 |
| 9 | `v1-portfolio-screen` | Core Loop | 2 | Screen 09, PositionCard, HealthBar |
| 10 | `v1-close-position` | Core Loop | 9 | Screen 10 |
| 11 | `v1-deposit-flow` | Money Flow | 2 | Screen 05, Screen 06, NumPad |
| 12 | `v1-withdraw-screen` | Money Flow | 2 | Screen 11 |
| 13 | `v1-share-card` | Social | 9 | Screen 12 |
| 14 | `v1-transitions-polish` | Polish | All | Toast, transitions, animations |

## Parallelism

Within each phase, changes that share the same dependency can be built in parallel:

- **Onboarding (3–5):** All depend only on `v1-core-components` → can be built in parallel
- **Core Loop:** `v1-home-screen` (6), `v1-trade-screen` (7), `v1-portfolio-screen` (9) can be built in parallel; then `v1-trade-confirmation` (8) and `v1-close-position` (10) follow
- **Money Flow (11–12):** Both depend only on `v1-core-components` → can be built in parallel with Core Loop
- **Social (13):** depends on `v1-portfolio-screen` → after change 9

## How to Execute

For each change, run:
```
/opsx:propose <change-name>
```
Then implement with:
```
/opsx:apply <change-name>
```

Start with `v1-project-setup`, then `v1-core-components`, then fan out into the parallel tracks.
