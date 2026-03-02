# MF Perps DEX — UX Plan (V1 MVP)

> **Scope:** Core trading loop — onboard, deposit, discover, trade, manage, close, withdraw. No referral program (V3), no RWA yield exposure (V2), no XP, levels, streaks, challenges, leaderboards, badges, or reward drops (V4). See [plan-v2-rwa-yield.md](plan-v2-rwa-yield.md), [plan-v3-referral-program.md](plan-v3-referral-program.md), [plan-v4-gamification.md](plan-v4-gamification.md).

## Design Philosophy

**The best crypto UX is one where you forget you're using crypto.**

DreamCash made the classic DeFi mistake: they tried to *educate* users about crypto concepts (wallets, gas, liquidation, seed phrases) instead of *abstracting them away*. Education is friction. Every tutorial screen is a drop-off point.

Our benchmark isn't other perps DEXs. It's **Robinhood, Cash App, and Revolut.** These apps let people do complex financial things (options trading, international transfers, multi-currency accounts) without ever explaining the plumbing. We do the same — but for perps.

### Core Principles
1. **Zero crypto vocabulary** — Users see "account", not "wallet". "Deposit", not "bridge". "Trade", not "swap". "Balance", not "TVL".
2. **No exposed plumbing** — No transaction hashes, no gas fees, no block confirmations, no signing modals. Everything happens behind the curtain.
3. **Progressive complexity** — The default experience is dead simple. Power features (advanced order types, leverage beyond 10x, detailed liquidation info) are there but tucked away.
4. **Speed is UX** — Optimistic updates everywhere. The UI responds instantly; blockchain confirmation happens in the background. If something fails, we roll back gracefully.
5. **Trust through compliance** — KYC isn't a wall, it's a trust signal. "Stronger venue trust through verified access" is a selling point, not a hurdle.

---

## Journey-by-Journey Redesign

### 1. Onboarding

#### DreamCash Problem
13+ screens. Username, wallet creation, Face ID, import/export wallet, then a parade of education cards (what's leverage, what's liquidation, how to fund). Most users will never finish this.

#### MF Perps Approach: "Explore in 60 seconds"

**Flow: 3 screens to app access**

```
Screen 1: Sign Up
┌─────────────────────────┐
│                         │
│     [MF Perps Logo]     │
│                         │
│  Trade BTC, ETH & more  │
│  Up to 100x leverage    │
│                         │
│  ┌───────────────────┐  │
│  │ Continue with Apple│  │
│  └───────────────────┘  │
│  ┌───────────────────┐  │
│  │ Continue with Google│ │
│  └───────────────────┘  │
│  ┌───────────────────┐  │
│  │ Use email/phone    │  │
│  └───────────────────┘  │
│                         │
│  Already have account?  │
│         Sign in         │
└─────────────────────────┘
```

- **Apple/Google sign-in as primary** — one tap, account created. No username, no password. Auth handled by **Privy SDK**.
- **Privy embedded wallet** created automatically in the background — user never sees it, never manages it, never knows it exists.
- Biometric auth inherited from device — no separate "enable Face ID" step. Privy handles session persistence.

```
Screen 2: Quick KYC
┌─────────────────────────┐
│                         │
│   Verify your identity  │
│                         │
│   Usually takes ~30 sec │
│   and helps keep the    │
│   venue trusted and     │
│   accountable ✓         │
│                         │
│   ┌───────────────────┐ │
│   │  Scan your ID     │ │
│   └───────────────────┘ │
│   ┌───────────────────┐ │
│   │  Take a selfie    │ │
│   └───────────────────┘ │
│                         │
│   🔒 Bank-grade security│
│   Your data is encrypted│
└─────────────────────────┘
```

- Framed as a **trust feature**, not a compliance burden. "Verification helps keep the venue trusted."
- Use a provider like Onfido/Sumsub for fast document + selfie KYC.
- If KYC takes time to approve, let users **explore the app** (view markets, set up watchlist) while waiting.
- Update product promise accordingly: users can explore in ~60 seconds; first live trade requires KYC approval.

```
Screen 3: You're in
┌─────────────────────────┐
│                         │
│   You're all set        │
│                         │
│   ┌───────────────────┐ │
│   │ Deposit & Trade   │ │
│   └───────────────────┘ │
│   ┌───────────────────┐ │
│   │ Explore Markets   │ │
│   └───────────────────┘ │
│                         │
└─────────────────────────┘
```

- No tutorials, no education screens.

**What we killed from DreamCash:**
- ~~Pick a username~~ → Not needed. Display name from Apple/Google.
- ~~Welcome animation~~ → Wastes time.
- ~~Enable Face ID~~ → Inherited from device sign-in. Privy handles session.
- ~~Import/export wallet~~ → No user-facing wallet. Privy embedded wallet created silently.
- ~~Trade with money education~~ → They'll figure it out by... trading with money.
- ~~Share positions education~~ → Discoverable in the trade screen.
- ~~Understand liquidation~~ → Shown contextually when it matters (setting leverage).
- ~~Manage portfolio education~~ → The portfolio screen *is* the education.
- ~~Choose funding education~~ → The deposit flow *is* the education.
- ~~Points system onboarding~~ → Discoverable later (V4 gamification).
- ~~Enter referral code~~ → Deferred to V3 referral program. See [plan-v3-referral-program.md](plan-v3-referral-program.md).

---

### 2. Funding / Deposits

#### DreamCash Problem
Forces users through crypto-native deposit flows: wallet addresses, QR codes, choosing networks, buying crypto through third parties. A web2 user hits a wall here.

#### MF Perps Approach: "Fund your investment account"

```
Deposit Screen
┌─────────────────────────┐
│   Fund Account          │
│                         │
│   ┌───────────────────┐ │
│   │ Transfer Crypto    │ │
│   │    From another    │ │
│   │    wallet          │ │
│   └───────────────────┘ │
│                         │
└─────────────────────────┘
```

**Key decisions:**
- **Crypto transfer is the V1 funding path.** Fiat on-ramps (Debit Card, Apple Pay) are deferred to V5 — see [plan-v5-fiat-integrations.md](plan-v5-fiat-integrations.md).
- Language is "Fund Account" with "Buying Power" context, not "Deposit" or "Fund Wallet".
- User enters a dollar amount. We handle the fiat→stablecoin conversion behind the scenes (we support mantraUSD, USDC, and USDT — mantraUSD is our default stablecoin). They never see "USDC", "bridging", or "network fees".
- For the crypto transfer path, show a simple "receive" screen with address + QR — auto-detect the network. No chain picker dropdown.

**Amount entry:**
```
┌─────────────────────────┐
│                         │
│        $150.00          │
│                         │
│   ┌─────┬─────┬─────┐  │
│   │ $50 │$100 │$500 │  │
│   └─────┴─────┴─────┘  │
│                         │
│   ┌─┬─┬─┐              │
│   │1│2│3│              │
│   ├─┼─┼─┤              │
│   │4│5│6│              │
│   ├─┼─┼─┤              │
│   │7│8│9│              │
│   ├─┼─┼─┤              │
│   │.│0│⌫│              │
│   └─┴─┴─┘              │
│                         │
│   ┌───────────────────┐ │
│   │  Fund $150.00     │ │
│   └───────────────────┘ │
│                         │
│   Fee: $1.50            │
│   Buying power $148.50 │
└─────────────────────────┘
```

- Quick-select chips ($50, $100, $500) for speed.
- Transparent fee shown inline — no surprises.
- Single "Fund $X" CTA. One tap after entering amount.

---

### 3. Markets / Discovery

#### DreamCash Problem
Dumps users into a market list. No guidance on what to trade or why.

#### MF Perps Approach: "The Feed"

The home screen isn't a market list. It's a **trading feed** — part watchlist, part discovery.

```
Home Screen
┌─────────────────────────┐
│ ☰  MF Perps     $148.50│
│                         │
│ 🔥 Trending             │
│ PEPE  +47.2%  24h       │
│ SOL   +12.8%  24h       │
│ BTC    +3.2%  24h       │
│                         │
│ Your Watchlist          │
│ BTC    $67,156      📈  │
│ ETH     $3,842      📉  │
│ + Add market            │
│                         │
│ Top Movers              │
│ ┌──────┐┌──────┐┌─────┐│
│ │ DOGE ││ ARB  ││ OP  ││
│ │+23.1%││-8.4% ││+5.6%││
│ └──────┘└──────┘└─────┘│
│                         │
│ [Home] [Trade] [Portfolio]│
└─────────────────────────┘
```

- **Balance always visible** in the header — users should always know where they stand.
- **Trending section** surfaces momentum — degen traders love this.
- **Watchlist** is personal and editable.
- **Top movers** as horizontal scroll cards for discovery.
- Tapping any market goes straight to the trade screen.

> **V4 addition:** The home screen gains a streak counter, level indicator, and daily challenge card. See [plan-v4-gamification.md](plan-v4-gamification.md).

---

### 4. Opening a Position (Long / Short)

#### DreamCash Problem
Too many steps. Market selection → chart → amount → leverage picker → review → confirmation → sign transaction → wait for blockchain. That's 7-8 screens with multiple cognitive loads (understanding leverage, reading confirmations, signing transactions).

#### MF Perps Approach: "Trade in 2 taps"

```
Trade Screen (e.g. BTC)
┌─────────────────────────┐
│ ← BTC / USD    $67,156  │
│                         │
│ ┌─────────────────────┐ │
│ │                     │ │
│ │    [Price Chart]    │ │
│ │    Interactive       │ │
│ │    1H 4H 1D 1W     │ │
│ │                     │ │
│ └─────────────────────┘ │
│                         │
│  ┌──────┐  ┌──────────┐│
│  │ Long │  │  Short   ││
│  │ (up) │  │  (down)  ││
│  └──────┘  └──────────┘│
│                         │
│  Amount     [$] 50.00   │
│  ┌─────┬──────┬───────┐│
│  │ $25 │ $50  │ $100  ││
│  └─────┴──────┴───────┘│
│                         │
│  Leverage        10x ◆──│
│  ├──┼──┼──┼──┼──┼──┤   │
│  2x          50x  100x │
│                         │
│  Position size   $500   │
│  Liquidation   $63,798  │
│  Fee             $0.25  │
│                         │
│  ┌───────────────────┐  │
│  │  Open Long $500   │  │
│  │  BTC at $67,156   │  │
│  └───────────────────┘  │
│                         │
└─────────────────────────┘
```

**Key design decisions:**

1. **Everything on one screen.** No separate "review" screen. Chart, direction, amount, leverage, and confirmation are all visible at once. The CTA button at the bottom updates in real-time as you adjust inputs.

2. **Long / Short as simple "Up / Down".** The primary labels are "Long" and "Short" (traders expect this), but the subtext "(up)" and "(down)" makes it instantly clear for newcomers. Long = green, Short = red. Universal.

3. **Amount in dollars, always.** Never in token units. "$50", not "0.00074 BTC". Quick-select chips for common amounts.

4. **Leverage slider with smart defaults.** Default is 10x (safe enough, exciting enough). Slider goes to 100x. Above 25x, the slider turns yellow. Above 50x, it turns red. Brief inline text: "Higher leverage = higher risk of losing your deposit."
   - No popup education. No "what is leverage?" modal. The color coding and one line of text is sufficient.
   - First-time users are **capped at 10x** until they've completed one trade. This protects them without lecturing them.

5. **Key numbers shown inline.** Position size, liquidation price, and fee are shown in a clean summary — not on a separate confirmation screen. The user sees the full picture before tapping.

6. **Single CTA.** "Open Long $500 BTC at $67,156". The button text tells you exactly what will happen. One tap to execute.

7. **No transaction signing.** No MetaMask popup, no "confirm transaction", no gas estimation. **Privy embedded wallet + session keys** handle signing silently. The trade executes instantly with an optimistic UI update.

8. **Instant feedback.**
   ```
   ┌─────────────────────────┐
   │                         │
   │   ✓ Position Opened     │
   │                         │
   │   BTC Long $500 @ 10x   │
   │   Entry: $67,156        │
   │                         │
   │   ┌───────────────────┐ │
   │   │  View Position    │ │
   │   └───────────────────┘ │
   │   ┌───────────────────┐ │
   │   │  Trade Again      │ │
   │   └───────────────────┘ │
   │                         │
   └─────────────────────────┘
   ```
   - Toast/bottom sheet confirmation, not a full-screen takeover.
    - Show the key info and actions: View Position, Trade Again, or Set TP/SL.

---

### 5. Watching a Position / Portfolio

#### DreamCash Problem
Functional but clinical. Just numbers. No emotional engagement, no quick actions.

#### MF Perps Approach: "Your positions, alive"

```
Portfolio Screen
┌─────────────────────────┐
│ Portfolio       $648.50  │
│                 +$12.30  │
│                         │
│ ┌─────────────────────┐ │
│ │  📈                 │ │
│ │   ╱╲    ╱╲  ╱──     │ │
│ │  ╱  ╲  ╱  ╲╱       │ │
│ │ ╱    ╲╱            │ │
│ └─────────────────────┘ │
│ [1D] [1W] [1M] [3M] [ALL]│
│                         │
│ Open Positions (2)      │
│ ┌─────────────────────┐ │
│ │ BTC Long   10x      │ │
│ │ +$12.80  (+2.56%)   │ │
│ │ $500 → $512.80      │ │
│ │ ████████░░ 76% to liq│ │
│ │          [Close]     │ │
│ └─────────────────────┘ │
│ ┌─────────────────────┐ │
│ │ ETH Short  5x       │ │
│ │  -$0.50  (-0.10%)   │ │
│ │ $100 → $99.50       │ │
│ │ █████████░ 92% to liq│ │
│ │          [Close]     │ │
│ └─────────────────────┘ │
│                         │
│ Available     $48.50    │
│ [Deposit]               │
│                         │
│ History                 │
│ ┌─────────────────────┐ │
│ │ SOL Long  Closed    │ │
│ │ +$45.00  (+15.0%)   │ │
│ │ 2 hours ago         │ │
│ └─────────────────────┘ │
│                         │
│ [Home] [Trade] [Portfolio]│
└─────────────────────────┘
```

**Key design decisions:**

1. **P&L is the hero.** Total portfolio value and total P&L at the top. Each position shows dollar P&L and percentage. Green = winning, red = losing. Visceral and immediate.

2. **Portfolio value chart.** An area chart directly under the total value shows how the portfolio has moved over time. Line and fill colour match overall P&L — green when up, red when down. Time-range pills (1D / 1W / 1M / 3M / ALL) let users zoom in or out. Touching the chart scrubs through time and updates the header value + P&L to that point. This gives users an instant emotional read on their trajectory without needing to interpret numbers.

3. **Liquidation as a health bar**, not a price. "76% to liquidation" with a visual bar is instantly understood. No one needs to mentally calculate distance from a liquidation price. The bar goes from green → yellow → red as risk increases.

4. **Inline close button.** One tap to close directly from the portfolio view. No need to drill into a position detail screen for the most common action.

5. **History below active positions.** Recent closed trades visible for reinforcement (wins) and learning (losses).

6. **Share-ready.** Long-press or swipe on any position card → "Share" generates a branded card showing your P&L. This is how we get viral spread — discoverable through gesture, not an onboarding tutorial.

---

### 6. Closing a Position

#### DreamCash Problem
Requires navigating into position detail, finding the close button, confirming, signing a transaction, waiting.

#### MF Perps Approach: "Swipe to close"

**Two paths to close:**

**Path A: Quick Close (from Portfolio)**
- Tap "Close" on any position card
- Bottom sheet slides up:
  ```
  ┌─────────────────────────┐
  │ Close BTC Long?         │
  │                         │
  │ Your P&L: +$12.80      │
  │ You'll receive: $512.80 │
  │                         │
  │ ┌───────────────────┐   │
  │ │  Close Full       │   │
  │ └───────────────────┘   │
  │     Close Partial ▼     │
  │                         │
  │ Cancel                  │
  └─────────────────────────┘
  ```
- "Close Full" is the default and primary action.
- "Close Partial" expands a slider to choose percentage — power feature, tucked away.
- No transaction signing. Executes instantly.

**Path B: Position Detail**
- Tapping the position card (not the close button) opens a detail view with full chart, entry/current price, funding rate, etc.
- Same close button at the bottom of this screen.

---

### 7. Withdrawals

#### MF Perps Approach: "Get your money out, fast"

```
Withdraw Screen
┌─────────────────────────┐
│   Withdraw              │
│                         │
│   Available: $512.80    │
│                         │
│        $512.80          │
│   ┌──────┬──────┬─────┐│
│   │  25% │  50% │ Max ││
│   └──────┴──────┴─────┘│
│                         │
│   Withdraw to:          │
│   ┌───────────────────┐ │
│   │  External Wallet  │ │
│   │    Paste or select │ │
│   │    wallet address  │ │
│   │    Instant         │ │
│   └───────────────────┘ │
│                         │
└─────────────────────────┘
```

- Percentage quick-select chips (25%, 50%, Max).
- Tapping the wallet card is the action — no separate CTA button needed. The card expands to show an address input (or list of saved addresses) and confirms the withdrawal.
- V1 supports external wallet withdrawal only. Fiat off-ramps (debit card, bank transfer) are in [plan-v5-fiat-integrations.md](plan-v5-fiat-integrations.md).

---

## Navigation Structure

```
┌─────────────────────────────────┐
│                                 │
│   [Home]  [Trade]  [Portfolio]  │
│                                 │
└─────────────────────────────────┘
```

Three tabs. That's it.

- **Home** — Markets feed, trending, watchlist, top movers.
- **Trade** — Opens to last-traded pair. Chart + trade input on one screen.
- **Portfolio** — Open positions, history, balance + deposit/withdraw.

Settings and profile are behind the hamburger menu (☰) or profile avatar. They exist but don't compete for primary navigation space.

---

## Interaction Patterns

### Haptics
- **Light tap** on button presses
- **Success burst** on trade execution
- **Warning rumble** when sliding leverage past 25x

### Animations
- Price chart updates in real-time with smooth interpolation
- P&L numbers count up/down (not just snap to new values)
- Position cards slide in/out on open/close
- Subtle pulse on the portfolio total when it updates

### Dark Mode Default
Trading apps live in dark mode. Our default is dark. Light mode available but secondary.

---

## Failure States & Recovery UX (Must-Design)

If we hide blockchain plumbing, we must still make failures legible and recoverable.

### Trade execution states
- **Submitting:** Inline spinner on CTA + disabled repeat taps.
- **Pending venue confirmation:** "Opening position…" state with clear retry-safe behavior.
- **Failed:** Human-readable reason + one-tap retry; never expose tx hash as primary UX.
- **Partial/edge execution handling:** If engine supports partial outcomes, show exact filled notional and remaining state.

### Funding states
- **Card/on-ramp pending:** "Processing deposit" status with ETA and push notification on completion. *(Applies when fiat on-ramps are added in V5.)*
- **Deposit failed/reversed:** Explicit status, reason code bucket, and next-best action (retry card / choose bank / support).

### Withdrawal states
- **Initiated:** "Withdrawal started" with expected settlement window by rail.
- **Delayed/reviewed:** Show compliance review state and expected follow-up path.
- **Failed/returned:** Explain outcome and where funds are now (available balance vs in-flight).

---

## Risk Controls (V1 Guardrails)

- First-trade leverage cap at 10x; raise limits only after completed trade history and risk checks.
- Notional and leverage limits by verification/risk tier.
- Cooldown and warning prompts after rapid loss sequences.
- Clear liquidation proximity and auto-notifications at risk thresholds.

---

## What We Intentionally Skip

| DreamCash Feature | Our Decision | Why |
|---|---|---|
| Crypto education screens | Skip entirely | Abstraction > education |
| Wallet import/export | No user-facing wallets | Privy embedded wallet |
| Network/chain selection | Auto-routed | Users don't care about L1/L2 |
| Gas fee display | Absorbed into trading fee | One fee, clearly shown |
| Transaction signing | Privy session keys | Invisible to user |
| Seed phrase backup | Not applicable | Privy wallet recovery via social login |
| Token swap | Later consideration | Focus on perps for MVP |

---

## V1 MVP Scope (30 Days)

### P0 — Must Have (30-day internal MVP)
- [ ] Sign up via Privy (Apple/Google/Email) + embedded wallet creation
- [ ] KYC flow (Onfido/Sumsub integration)
- [ ] Crypto transfer funding (Transfer Crypto from external wallet)
- [ ] Fiat on-ramps (Debit Card, Apple Pay) are deferred to V5 — see [plan-v5-fiat-integrations.md](plan-v5-fiat-integrations.md)
- [ ] Market list with prices (BTC, ETH + 3-5 others)
- [ ] Price chart (TradingView lightweight chart)
- [ ] Open Long/Short position (one-tap perp execution, Privy session keys for signing)
- [ ] Position management (view, close full)
- [ ] Portfolio view with P&L
- [ ] Push notifications (position opened, closed, approaching liquidation, funding status)
- [ ] Failure-state UX for trade/funding/withdrawal (pending, failed, retry)

### P1 — Should Have (immediately after internal MVP)
- [ ] Partial close
- [ ] Take profit / stop loss
- [ ] Share position card
- [ ] Watchlist
- [ ] Price alerts

### P2 — Deferred
- [ ] RWA yield exposure — see [plan-v2-rwa-yield.md](plan-v2-rwa-yield.md)
- [ ] Referral program — see [plan-v3-referral-program.md](plan-v3-referral-program.md)
- [ ] XP system + level progression (V4)
- [ ] Daily login streak tracking (V4)
- [ ] Daily / weekly challenges (V4)
- [ ] Leaderboards (V4)
- [ ] Achievement badges (V4)
- [ ] Reward drops (V4)
- [ ] Fiat on-ramps / off-ramps (V5)
- [ ] Social feed / copy trading

---

## MVP Success Metrics (Track from Day 1)

- Signup → KYC start rate
- KYC start → KYC approved rate and median approval time
- KYC approved → first successful deposit rate
- First deposit → first position opened rate
- Day-1 and Day-7 retention for funded users
- Support contact rate per 100 funded users (especially around deposits/withdrawals)

---

## OpenSpec Prompts

These prompts are for a **web clickable prototype** used to validate UX quickly in 30 days. Product target remains React Native for production.

Each prompt below is a self-contained spec that can be handed to an AI coding agent. They reference `build-v1-mvp.md` for tech stack, file structure, design tokens, and mock data. Build in the order listed.

---

### Prompt 0: Project Setup & Foundations

```
You are building a web clickable prototype using Next.js 14 (App Router), Tailwind CSS, Framer Motion, and TypeScript to simulate a mobile app UI. Read build-v1-mvp.md for the full tech stack and design tokens.

Do the following:

1. Initialize the project:
   npx create-next-app@latest mf-perps-prototype --typescript --tailwind --app --src-dir --no-eslint
   cd mf-perps-prototype
   npm install framer-motion lucide-react zustand

2. Set up the design tokens in src/lib/tokens.ts as exported constants matching the colors, typography, spacing, and radius specs in build-v1-mvp.md.

3. Configure tailwind to extend the theme with these tokens (custom colors: background, surface, surface-light, border, text-primary, text-secondary, text-muted, accent, green, red, yellow, orange).

4. Set up globals.css with:
   - Tailwind imports
   - Import Inter font from Google Fonts
   - Set html/body to use the background color (#0A0A0F), text-primary, and Inter font
   - Hide scrollbar for the phone frame

5. Create the Zustand store in src/lib/store.ts with the navigation state:
   - screen: one of 'welcome' | 'kyc' | 'youre-in' | 'home' | 'deposit' | 'deposit-amount' | 'trade' | 'portfolio' | 'withdraw'
   - overlay: null | 'trade-confirmation' | 'close-position' | 'share-card'
   - selectedPair: string (default 'BTC/USD')
   - navigate(screen) function
   - showOverlay(overlay) function
   - dismissOverlay() function

6. Create src/lib/mock-data.ts with all mock data from build-v1-mvp.md (markets, openPositions, user).

7. Create the base reusable components:
   - src/components/Button.tsx — Three variants: primary (accent bg), secondary (surface-light bg), ghost (transparent, underline). All have rounded-xl, font-semibold, full-width by default, press-scale animation (Framer Motion whileTap scale 0.97).
   - src/components/Card.tsx — Surface bg, rounded-2xl, p-4, subtle border.
   - src/components/Input.tsx — surface-light bg, rounded-xl, text-primary, placeholder in text-muted. Focus ring in accent color.

8. Create src/components/PhoneFrame.tsx:
   - Centred on page, max-w-[390px], h-[844px]
   - Rounded-[40px] corners, border border-[#2A2A3A]
   - Background color matches app bg
   - Overflow-y-auto with hidden scrollbar
   - The outer page background should be #111111

9. Create src/components/StatusBar.tsx:
   - Fake iOS status bar at the top of the phone frame
   - Shows time "9:41" (left), and signal + wifi + battery icons (right)
   - White text, small font, absolute positioned at top of frame with padding

10. Create src/components/BottomNav.tsx:
    - Three tabs: Home (House icon), Trade (TrendingUp icon), Portfolio (Wallet icon)
    - Fixed at the bottom of the phone frame
    - Active tab uses accent color, inactive uses text-muted
    - Tab labels below icons in text-xs
    - Surface bg with top border
    - Tapping a tab calls navigate() from the store

11. Wire it all up in src/app/page.tsx:
    - Render PhoneFrame containing StatusBar at top, a content area in the middle that renders the current screen based on store.screen, and BottomNav at the bottom
    - BottomNav only shows when screen is 'home', 'trade', or 'portfolio' (hide during onboarding)
    - Overlay renders on top of everything when store.overlay is set

The app should be runnable with `npm run dev` and show an empty phone frame with status bar and bottom nav on a dark background.
```

---

### Prompt 1: Onboarding — Welcome Screen

```
Read build-v1-mvp.md and plan-v1-mvp.md for full context. You are building Screen 01: Welcome/Sign Up for the MF Perps prototype.

Create src/screens/01-Welcome.tsx:

This is the first screen users see. It should feel premium, clean, and fast.

Layout (top to bottom, centred):
- MF Perps logo area: Use a bold text logo "MF" in accent color (#7B61FF) with "Perps" in white, text-3xl. Centre it in the top third of the screen with generous top padding (pt-24).
- Tagline: "Trade BTC, ETH & more" in text-lg text-primary, and "Up to 100x leverage" in text-sm text-secondary. Small gap between them.
- Three auth buttons (stacked, full width, gap-3, px-6):
  1. "Continue with Apple" — white bg, black text, rounded-xl, h-14. Apple icon on the left.
  2. "Continue with Google" — surface-light bg, white text, rounded-xl, h-14. Google "G" as text on the left.
  3. "Use email or phone" — ghost variant (transparent bg, border border-[#2A2A3A]), white text, rounded-xl, h-14. Mail icon on the left.
- Bottom area (mt-auto, pb-8): "Already have an account?" in text-secondary, "Sign in" as accent-colored text link. Centred.

Interactions:
- All three auth buttons navigate to 'kyc' screen on tap.
- Add Framer Motion: fade-in on mount (opacity 0→1 over 500ms), buttons stagger in from below (y: 20→0, staggered by 100ms).
- Buttons have whileTap={{ scale: 0.97 }} for press feedback.

The screen should use the full height of the phone frame content area. No bottom nav on this screen.
```

---

### Prompt 2: Onboarding — KYC Screen

```
Read build-v1-mvp.md and plan-v1-mvp.md for full context. You are building Screen 02: KYC for the MF Perps prototype.

Create src/screens/02-KYC.tsx:

This screen frames identity verification as a trust feature, not a chore.

Layout (centred, px-6):
- Back arrow (ChevronLeft icon from Lucide) in top-left, tapping goes back to 'welcome'.
- Heading: "Verify your identity" — text-2xl font-bold text-primary. Top-aligned with generous spacing (pt-16).
- Subtext: "Usually takes ~30 seconds. Verification helps keep the venue trusted." — text-sm text-secondary, mt-2.
- Two step cards (mt-8, gap-3). Each is a Card component with a horizontal layout:
  1. FileText icon (Lucide) in accent color on the left, "Scan your ID" as text-primary, "Government-issued ID" as text-xs text-secondary below.
  2. Camera icon (Lucide) in accent color on the left, "Take a selfie" as text-primary, "Quick face match" as text-xs text-secondary below.
  Each card has a chevron-right icon on the far right in text-muted.
- Trust badge (mt-auto area, pb-8 before button): Lock icon + "Bank-grade encryption. Your data is never shared." in text-xs text-muted, centred.
- CTA: Primary Button "Start verification", full width, fixed near bottom.

Interactions:
- "Start verification" button: On tap, show a loading spinner inside the button (swap text for a spinning Loader2 icon from Lucide) for 1.5 seconds, then navigate to 'youre-in' screen.
- Framer Motion: content fades/slides in from right (x: 30→0) on mount.
```

---

### Prompt 3: Onboarding — You're In

```
Read build-v1-mvp.md and plan-v1-mvp.md for full context. You are building Screen 03: You're In confirmation for the MF Perps prototype.

Create src/screens/03-YoureIn.tsx:

This is the gateway to the app. Celebrate, then get out of the way.

Layout (centred both axes, px-6):
- Large check circle icon (Lucide CheckCircle2) in accent color, size 64px, centred.
- "You're all set" — text-2xl font-bold text-primary, mt-4.
- Two buttons (mt-8, gap-3, full width):
  1. "Deposit & Trade" — Primary Button (accent bg). Navigates to 'deposit'.
  2. "Explore Markets" — Secondary Button (surface-light bg). Navigates to 'home'.

Interactions:
- On mount: The check icon scales up from 0→1 with a spring animation (Framer Motion, type: "spring", stiffness: 200). Buttons stagger in from below after a 300ms delay.

No bottom nav on this screen.
```

---

### Prompt 4: Home Screen

```
Read build-v1-mvp.md and plan-v1-mvp.md for full context. You are building Screen 05: Home for the MF Perps prototype. This is the main discovery hub.

Create src/components/MarketRow.tsx first, then create src/screens/05-Home.tsx.

**MarketRow:**
- Takes props: pair, price, change24h.
- Horizontal layout: pair name (text-sm font-semibold), price (text-sm tabular-nums, right-aligned), change percentage (text-sm, green if positive, red if negative, with + prefix for positive).
- Subtle bottom border. Tappable — navigates to 'trade' with selectedPair set.
- ChevronRight icon on far right in text-muted.

**Home Screen layout (scrollable, px-4, pt-2, pb-24 for bottom nav clearance):**
1. Header row: hamburger Menu icon (left), "MF Perps" text-lg font-bold (centre), "$648.50" balance text-sm font-semibold (right, tappable → 'portfolio').
2. "🔥 Trending" section (mt-4): section header in text-xs uppercase tracking-wider text-muted, then 3 MarketRows for the top 3 markets by change%.
3. "Your Watchlist" section (mt-4): section header, then MarketRows for BTC and ETH, followed by a "+ Add market" row in text-sm text-accent with Plus icon.
4. "Top Movers" section (mt-4): Horizontal scrollable row of small cards (w-24, surface bg, rounded-xl, p-3). Each shows pair name (text-xs font-semibold) and change% (text-sm, colored). Use markets from mock-data.

Interactions:
- Tapping any market row → navigates to 'trade' with that pair selected in store.
- Tapping balance → 'portfolio'.

Bottom nav is visible on this screen with Home as the active tab.
```

---

### Prompt 5: Deposit Method Selection

```
Read build-v1-mvp.md and plan-v1-mvp.md for full context. You are building Screen 06: Deposit Method Selection for the MF Perps prototype.

Create src/screens/06-Deposit.tsx:

Layout (px-6, pt-4):
- Header: back arrow (goes to previous screen — 'home' or 'youre-in' depending on flow) + "Fund Account" title centred.
- Three method option cards (mt-6, gap-3). Each is a Card component with:
  - Left: icon (use Lucide icons — Wallet for crypto)
  - Centre: method name (text-sm font-semibold text-primary) + timing label below (text-xs text-secondary: "From another wallet")
  - Right: ChevronRight icon in text-muted
  - Cards have hover/tap state: border changes to accent on press

  The method:
  1. "Transfer Crypto" — Wallet icon, "From another wallet"

  Fiat on-ramps (Debit Card, Apple Pay) are deferred to V5 — see plan-v5-fiat-integrations.md.

Interactions:
- Tapping the Transfer Crypto card shows a simple static screen with a QR code placeholder (a grey rounded square) and a mock address "0x1a2b...9f0e" with a copy icon. This can be a bottom sheet overlay.
- Framer Motion: cards stagger in on mount.

No bottom nav on this screen.
```

---

### Prompt 6: Deposit Amount Entry

```
Read build-v1-mvp.md and plan-v1-mvp.md for full context. You are building Screen 07: Deposit Amount Entry for the MF Perps prototype.

Create src/components/NumPad.tsx first, then create src/screens/07-DepositAmount.tsx.

**NumPad component:**
- Props: onInput(digit: string), onDelete(), onDecimal()
- 4x3 grid of circular buttons:
  Row 1: 1, 2, 3
  Row 2: 4, 5, 6
  Row 3: 7, 8, 9
  Row 4: ".", 0, ⌫ (Delete icon from Lucide)
- Each button: w-16 h-16, rounded-full, surface-light bg, text-xl text-primary, centred text.
- Active/press state: bg brightens slightly. Framer Motion whileTap scale 0.9.
- Grid is centred horizontally with gap-3.

**Deposit Amount Screen layout (px-6, flex column, full height):**
- Header: back arrow (goes to 'deposit') + "Fund Account" title centred.
- Amount display area (flex-1, centred): Large "$" prefix in text-2xl text-secondary, then the amount value in text-5xl font-bold text-primary tabular-nums. Starts at "$0". When user types, digits appear with a subtle scale-in animation.
- Quick-select chips row (mt-4, centred, gap-2): Three pill buttons — "$50", "$100", "$500". Each is rounded-full, px-4 py-2, surface-light bg, text-sm. Tapping one sets the amount directly. Active chip (matching current amount) gets accent border.
- NumPad component (mt-4).
- Fee breakdown (mt-4, px-2): Two rows in text-sm:
  - "Fee" (left, text-secondary) + "$1.50" (right, text-primary) — calculate as 1% of amount
  - "Buying power after fee" (left, text-secondary) + "$148.50" (right, text-primary font-semibold)
  These update dynamically as the amount changes.
- CTA (mt-4, pb-8): Primary Button "Fund $150.00" — full width. Amount in button text updates dynamically. Button is disabled (opacity-50) when amount is $0.

Interactions:
- NumPad input builds the dollar amount string (handle decimal properly — max 2 decimal places).
- Quick-select chips override the amount.
- Fee and receive amount update reactively.
- CTA tap: button shows brief loading state (1s), then navigates to 'home' with a success toast ("Account funded: +$150.00" — implement as a Framer Motion toast that slides in from top and auto-dismisses after 2s).

No bottom nav on this screen.
```

---

### Prompt 7: Trade Screen

```
Read build-v1-mvp.md and plan-v1-mvp.md for full context. You are building Screen 08: Trade for the MF Perps prototype. This is the most important screen in the app.

Create src/components/LeverageSlider.tsx first, then create src/screens/08-Trade.tsx.

**LeverageSlider component:**
- Props: value (number), onChange(value: number), min (default 2), max (default 100)
- Custom slider (don't use native HTML range — build with Framer Motion drag or a custom touch handler):
  - Track: h-2, rounded-full, full width. Track fill color changes based on value:
    - 2-25x: green (#00D68F)
    - 25-50x: yellow (#FFD93D)
    - 50-100x: red (#FF4757)
  - Thumb: w-6 h-6, rounded-full, white bg with shadow, draggable along track.
  - Label above thumb showing current value: "10x" in text-sm font-bold, same color as track fill.
- Below the slider: "2x" on left and "100x" on right in text-xs text-muted.

**Trade Screen layout (scrollable, pb-24):**
1. Header: back arrow + pair name "BTC / USD" (text-lg font-semibold) centred + current price "$67,156" on right in text-sm tabular-nums. Pair name and price come from the selected pair in store.

2. Chart placeholder (mt-2, mx-4): A Card with h-48. Inside, render a simple SVG line chart using mock data — just a wavy upward-trending line in accent color on transparent bg. Or use a gradient area chart. Below the chart: timeframe pills (1H, 4H, 1D, 1W) as small rounded-full buttons in a row, "1D" active by default (accent bg, others surface-light).

3. Long/Short toggle (mt-4, mx-4): Two buttons side by side, equal width, rounded-xl, h-12.
   - "Long" button: when selected → green bg (#00D68F), white text, with "(up)" in text-xs below the label. When unselected → surface-light bg, text-muted.
   - "Short" button: when selected → red bg (#FF4757), white text, with "(down)" in text-xs. When unselected → surface-light bg, text-muted.
   - Default: Long selected.

4. Amount input (mt-4, mx-4):
   - Label: "Amount" in text-xs text-secondary.
   - Input field: surface-light bg, rounded-xl, h-12, "$" prefix in text-muted inside the input, text-right for the value, text-lg. Default: "50.00".
   - Quick-select chips below (mt-2): "$25", "$50", "$100" as small rounded-full pills. Active one has accent border.

5. Leverage slider (mt-4, mx-4):
   - Label: "Leverage" in text-xs text-secondary.
   - LeverageSlider component, default 10x.
   - When leverage > 25x, show a one-line warning below in text-xs: "Higher leverage = higher risk of losing your deposit" in yellow/red matching the slider color.

6. Summary section (mt-4, mx-4): Three rows, each text-sm:
   - "Position size" (text-secondary) → "$500" (text-primary font-semibold) — calculated: amount × leverage
   - "Liquidation price" (text-secondary) → "$63,798" (text-primary) — mock: for long, entry price × (1 - 1/leverage × 0.95)
   - "Fee" (text-secondary) → "$0.25" (text-primary) — mock: 0.05% of position size

7. CTA (mt-4, mx-4, pb-4): Full-width button, h-14, rounded-xl.
   - Text: "Open Long $500 BTC at $67,156" (two lines: action on first, detail on second in text-xs opacity-80)
   - Color: green bg when Long selected, red bg when Short selected.
   - Dynamic: updates text and color as user changes direction/amount/leverage.
   - Disabled state (opacity-50) when amount is 0.

Interactions:
- Long/Short toggle switches direction, CTA color, and CTA text.
- Amount chips and manual input update position size, liquidation, fee, and CTA.
- Leverage slider updates position size, liquidation, fee, and CTA.
- CTA tap: show the 'trade-confirmation' overlay.
- All number transitions should animate smoothly (Framer Motion AnimatePresence with layout animations on the summary values).

Bottom nav visible with Trade as active tab.
```

---

### Prompt 8: Trade Confirmation Bottom Sheet

```
Read build-v1-mvp.md and plan-v1-mvp.md for full context. You are building the Trade Confirmation bottom sheet overlay for the MF Perps prototype.

Create src/screens/09-TradeConfirmation.tsx:

This is a bottom sheet overlay that appears on top of the Trade screen when the user taps the CTA.

**Bottom sheet container:**
- Framer Motion: slides up from the bottom (y: "100%" → 0) with spring animation.
- Backdrop: fixed overlay, bg-black/50, tapping it dismisses.
- Sheet: surface bg, rounded-t-3xl, px-6 py-8, max height 50% of phone frame.
- Small drag handle bar at top: w-10 h-1 rounded-full bg-[#2A2A3A] centred.

**Content:**
- Large green checkmark circle icon (CheckCircle2 from Lucide), size 48px, centred, in green color.
- "Position Opened" — text-xl font-bold text-primary, centred, mt-4.
- Summary card (mt-4, Card component): three rows in text-sm:
  - "BTC Long $500 @ 10x" (uses actual values from the trade)
  - "Entry: $67,156"
  - These should reflect the actual trade parameters the user set.
- Two buttons (mt-6, gap-3):
  1. "View Position" — Primary Button. Navigates to 'portfolio' and dismisses overlay.
  2. "Trade Again" — Secondary Button. Dismisses overlay, stays on trade screen.
  3. "Set TP/SL" — Secondary Button. Opens the position risk-controls sheet for take profit and stop loss.

Interactions:
- On mount: checkmark scales in with spring animation, then text fades in.
- Swipe down to dismiss (Framer Motion drag on the sheet, if dragY > 100 dismiss).

This renders as an overlay on top of whatever screen is showing. Use the store's overlay state.
```

---

### Prompt 9: Portfolio Screen

```
Read build-v1-mvp.md and plan-v1-mvp.md for full context. You are building Screen 10: Portfolio for the MF Perps prototype.

Create these components first:
- src/components/PositionCard.tsx
- src/components/HealthBar.tsx

**HealthBar component:**
- Props: percent (number 0-100, where 100 = safe, 0 = liquidated)
- Track: h-1.5, rounded-full, surface-light bg, full width.
- Fill: rounded-full, width = percent%.
  - Color: green (#00D68F) when >60%, yellow (#FFD93D) when 30-60%, red (#FF4757) when <30%.
- Label to the right: "{percent}% to liq" in text-xs, same color as fill.

**PositionCard component:**
- Props: position object (from mock-data openPositions type)
- Card component with:
  - Top row: "{pair} {direction} {leverage}x" — e.g. "BTC Long 10x". Direction text colored (green for long, red for short). Leverage in text-muted.
  - P&L row: "+$12.80 (+2.56%)" in green (or red if negative), text-lg font-bold.
  - Value row: "$500 → $512.80" in text-sm text-secondary.
  - HealthBar component with the position's healthPercent.
  - Close button: right-aligned, text-sm, surface-light bg, rounded-lg, px-3 py-1.5, "Close" text. On tap: shows 'close-position' overlay.
- Subtle left border accent: 3px left border in green (long) or red (short).

**Portfolio Screen layout (scrollable, px-4, pt-2, pb-24):**
1. Header: "Portfolio" (text-lg font-bold, left), total value "$648.50" (text-2xl font-bold, right) with P&L "+$12.30" below it in text-sm green.

2. "Open Positions (2)" section header (mt-4, text-xs uppercase tracking-wider text-muted).

3. Two PositionCards stacked with gap-3, using mock-data openPositions.

4. Available balance row (mt-4): "Available" (text-sm text-secondary) + "$48.50" (text-sm font-semibold). Next to it: "Deposit" link in text-sm text-accent, tapping goes to 'deposit'.

5. "History" section header (mt-6, text-xs uppercase tracking-wider text-muted).

6. Two closed position rows (mt-2, gap-2). Each is a simpler row (no card bg):
   - "SOL Long — Closed" in text-sm, "+$45.00 (+15.0%)" in green text-sm, "2 hours ago" in text-xs text-muted.
   - "DOGE Short — Closed" in text-sm, "-$12.00 (-8.0%)" in red text-sm, "Yesterday" in text-xs text-muted.

Interactions:
- Close button on PositionCard shows 'close-position' overlay.
- P&L numbers should use Framer Motion to count up on mount (e.g., $0 → $12.80 over 500ms).

Bottom nav visible with Portfolio as active tab.
```

---

### Prompt 10: Close Position Bottom Sheet

```
Read build-v1-mvp.md and plan-v1-mvp.md for full context. You are building the Close Position bottom sheet overlay.

Create src/screens/11-ClosePosition.tsx:

Same bottom sheet pattern as Trade Confirmation (slide up, backdrop, drag handle).

**Content:**
- "Close BTC Long?" — text-xl font-bold, centred.
- Summary (mt-4), two rows in text-sm:
  - "Your P&L" (text-secondary) → "+$12.80" (green, font-semibold)
  - "You'll receive" (text-secondary) → "$512.80" (text-primary, font-semibold)
- "Close Full Position" — Primary Button, full width, mt-6. Accent bg.
- "Close Partial ▼" — ghost text link, centred, mt-3, text-sm text-secondary. On tap: expand a slider (0-100%) with Framer Motion AnimatePresence. This is a stretch feature — just show the expand animation and a basic slider, doesn't need to be functional.
- "Cancel" — ghost text link, centred, mt-3, text-sm text-muted.

Interactions:
- "Close Full" tap: dismiss overlay, remove the position from the UI (animate it out of the portfolio list), show success toast "Position closed — $512.80 received".
- "Cancel" tap: dismiss overlay.
- Swipe down to dismiss.
```

---

### Prompt 11: Withdraw Screen

```
Read build-v1-mvp.md and plan-v1-mvp.md for full context. You are building Screen 12: Withdraw.

Create src/screens/12-Withdraw.tsx:

Layout (px-6, pt-4):
- Header: back arrow (goes to 'portfolio') + "Withdraw" title centred.
- Available balance: "Available: $512.80" in text-sm text-secondary, centred, mt-2.
- Large amount display (mt-4): "$512.80" in text-4xl font-bold text-primary, centred. Pre-filled with max.
- Quick-select chips (mt-3, centred): "25%", "50%", "Max" as rounded-full pills. "Max" active by default (accent border). Tapping recalculates the amount.
- "Withdraw to:" label (mt-6, text-xs uppercase tracking-wider text-muted).
- Single destination card (mt-2): Wallet icon + "External Wallet" + "Paste or select wallet address" in text-xs text-secondary + "Instant" in text-xs text-muted. Accent border, checkmark on right.
  - V1 supports external wallet only. Fiat off-ramps (debit card) are deferred to V5.

Interactions:
- Chips adjust the amount (25% = $128.20, 50% = $256.40, Max = $512.80).
- Tapping the wallet card is the action — it expands to show an address input (text field with paste button), then a "Confirm Withdraw" button within the expanded card. No separate bottom CTA needed.
- Confirm tap: loading state 1.5s, then navigate to 'portfolio' with success toast "Withdrawal initiated — $512.80".

No bottom nav.
```

---

### Prompt 12: Share Card Overlay

```
Read build-v1-mvp.md and plan-v1-mvp.md for full context. You are building the Share Card overlay.

Create src/screens/12-ShareCard.tsx:

This is a full-screen overlay showing a sharable position card.

**Overlay container:**
- Full screen within phone frame, bg-black/80 backdrop.
- Centred card with padding around it.

**Share card design (the actual card that would be shared):**
- w-full max-w-[320px], rounded-2xl, overflow-hidden.
- Background: linear gradient from surface (#14141F) to a slightly purple-tinted dark (#1a1530).
- Top accent bar: 4px tall, green gradient (for a long/winning position).
- Inner padding: p-6.
- Position info:
  - "🟢 BTC Long" in text-lg font-bold (green for long).
  - "+47.2%" in text-4xl font-bold text-green. The hero number.
  - "$500 → $735.00" in text-sm text-secondary.
- User info (mt-4): avatar circle (small, 24px) + "Jake" in text-xs.
- Divider line (mt-4, border-t border-[#2A2A3A]).
- Branding area (mt-4):
  - "Trade on MF Perps" in text-sm font-semibold.
  - "mfperps.app" in text-xs text-accent.

**Below the card:**
- Two buttons (mt-6, gap-3, px-6):
  1. "Share" — Primary Button with Share2 icon from Lucide.
  2. "Save Image" — Secondary Button with Download icon.
- "Done" text link below in text-sm text-muted, centred. Dismisses overlay.

Interactions:
- "Share" and "Save Image" just show a quick toast "Shared!" / "Saved!" (it's a prototype).
- "Done" dismisses the overlay.
- Card enters with Framer Motion: scale from 0.8→1 + opacity 0→1.
```

---

### Prompt 13: Screen Transitions & Polish

```
Read build-v1-mvp.md and plan-v1-mvp.md for full context. This is the final polish pass for the V1 MVP prototype.

1. **Screen transitions**: In the main page.tsx where screens are rendered, wrap the active screen in Framer Motion AnimatePresence with:
   - Onboarding screens (welcome→kyc→referral→youre-in): slide in from right (x: 30→0, exit x: -30), 300ms.
   - Tab screens (home, trade, portfolio): crossfade (opacity 0→1, 200ms). No slide.
   - Modal screens (deposit, deposit-amount, withdraw): slide up from bottom (y: 50→0, 300ms).
   - Overlays (trade-confirmation, close-position, share-card): already have their own animations.

2. **Toast notification component**: Create src/components/Toast.tsx:
   - Fixed at top of phone frame (below status bar), centred, z-50.
   - Pill shape: rounded-full, surface-light bg, px-4 py-2, text-sm.
   - Slides in from top (y: -20→0) and auto-dismisses after 2.5s (y→-20, opacity→0).
   - Add toast state to the Zustand store: showToast(message: string) that auto-clears.
   - Green left accent for success toasts.

3. **Number animations**: Anywhere dollar amounts or percentages are displayed (portfolio total, P&L, position size), use Framer Motion's useSpring or useMotionValue to animate from 0 to the target value on mount, counting up over 500ms. Use tabular-nums font-variant for stable number widths.

4. **Button micro-interactions**: Ensure all buttons have:
   - whileTap={{ scale: 0.97 }}
   - Primary buttons: slight brightness increase on hover/focus.

5. **Loading states**: The KYC "Start verification" and deposit "Add $X" buttons should show a Loader2 spinning icon during their loading states, replacing the button text.

6. **Overall scroll behaviour**: Ensure the PhoneFrame's inner content area scrolls smoothly. Add overscroll-behavior: contain and -webkit-overflow-scrolling: touch.

7. **Demo flow**: Make the prototype automatically start at the 'welcome' screen. Clicking through the onboarding flow should feel seamless and fast. After onboarding, the user lands on 'home' with the bottom nav.
```

---

## Summary: DreamCash vs MF Perps (V1 MVP)

| | DreamCash | MF Perps V1 |
|---|---|---|
| Onboarding | 13+ screens | 3 screens |
| Time to first value | 5-10 minutes | ~60 seconds to explore (+ KYC for live trading) |
| Funding | Crypto-native | Crypto transfer (V1); fiat on-ramps in V5 |
| Wallet | User-managed | Invisible (Privy embedded wallet) |
| Trading | 7-8 screen flow | Single screen |
| Transaction signing | Manual (MetaMask-style) | Invisible (Privy session keys) |
| Crypto knowledge needed | High | Zero |
| Language | Crypto jargon | Finance/fintech language |
| Referrals | Code entry buried in onboarding | Deferred to V3 — see [plan-v3-referral-program.md](plan-v3-referral-program.md) |
| Retention mechanics | Points (basic) | V4 — see [plan-v4-gamification.md](plan-v4-gamification.md) |
| RWA exposure | None | V2 — see [plan-v2-rwa-yield.md](plan-v2-rwa-yield.md) |
