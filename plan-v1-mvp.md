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
