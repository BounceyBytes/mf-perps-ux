# MF Perps DEX — Version Plan Overview

> A mobile-first perpetual futures DEX on MANTRA Finance. Attract traders with best-in-class perps trading, then convert them into RWA yield users.

---

## V1 — MVP (Core Trading Loop)

**Plan:** [plan-v1-mvp.md](plan-v1-mvp.md) · **Build:** [build-v1-mvp-openspec.md](build-v1-mvp-openspec.md)

The leanest possible trading app. A user who knows nothing about crypto should be able to trade with zero friction.

**What's included:**
- **Onboarding** — 3 screens: Sign Up (Privy social login), KYC (Onfido/Sumsub), You're In. No crypto wallet setup, no education screens.
- **Deposits** — Crypto transfer from external wallet. Amount entry with custom NumPad.
- **Markets / Discovery** — Home screen with trending, watchlist, and top movers.
- **Trading** — Single-screen trade execution: chart, Long/Short toggle, dollar amount, leverage slider, one-tap CTA. No transaction signing (Privy session keys).
- **Portfolio** — Open positions with live P&L, health bars (liquidation distance), inline close button, trade history.
- **Close Position** — Bottom sheet confirmation with full/partial close.
- **Withdrawals** — External wallet withdrawal with percentage chips.
- **Share Card** — Branded position P&L card for social sharing.

**What's NOT included:** No referral program, no RWA yield, no gamification, no fiat on-ramps.

---

## V2 — RWA Yield Exposure

**Plan:** [plan-v2-rwa-yield.md](plan-v2-rwa-yield.md)

The strategic differentiator — bridge from speculation to real-world assets. Yield is woven into the trading experience, not siloed in a separate section.

**What's included:**
- **Idle Balance Nudge** — Prompt users with idle funds to earn yield (dismissable, frequency-capped).
- **Post-Win Prompt** — After profitable trade closes, suggest putting profits to work.
- **Portfolio Yield Card** — Yield vault card alongside open positions showing deposited amount, target APY, and daily earnings.
- **Yield Vault Screen** — Full detail screen with deposit/withdraw to vault, yield history, and "About this vault" explainer.

**Key principle:** No crypto jargon. "Earn interest", not "stake" or "provide liquidity". All APY references include "variable, not guaranteed".

---

## V3 — Referral Program

**Plan:** [plan-v3-referral-program.md](plan-v3-referral-program.md)

Growth engine built into the product surface. Sharing a win *is* a referral.

**What's included:**
- **Referral Identity** — Every user gets an invite code + shareable deep link on signup.
- **Onboarding Referral Screen** — Optional screen between KYC and You're In. Skip is always visible.
- **Fee Rebates** — Referrers earn up to 10% of referrals' trading fees.
- **App-Wide Surfaces** — Share card embeds referral code + QR, portfolio "Invite & Earn" card, post-trade share prompts, milestone nudges.
- **Referral Dashboard** — Track referrals, earnings, and code management.
- **Anti-Abuse Controls** — Self-referral detection, velocity checks, payout holds.

---

## V4 — Gamification

**Plan:** [plan-v4-gamification.md](plan-v4-gamification.md) · **Build:** [build-v4-gamification.md](build-v4-gamification.md)

Daily retention engine. Turn sporadic "check my position" visits into a daily habit loop.

**What's included:**
- **XP & Levels** — Every action earns XP. Levels unlock perks (leverage caps, fee discounts). Progress bar with "next perk" preview.
- **Streaks** — Daily streak with low bar to maintain (just open the app). Streak freeze (1/week). Social pressure ("Jake is on a 23-day streak").
- **Daily/Weekly Challenges** — Fresh challenges daily (e.g. "View 5 markets", "Open a position"). Mix of low-effort and trading challenges. Progress bars.
- **Leaderboards** — Weekly P&L %, Volume, and Streaks boards. Top 10 earn bonus XP, top 3 earn fee rebates. Percentage-based ROI so small accounts can compete.
- **Achievement Badges** — Permanent collectibles (First Blood, On Fire, Diamond Hands, etc.). Displayed on profile.
- **Reward Drops** — Mystery reward reveals (fee-free trade, 2x XP, bonus XP, streak freeze). 30% chance after trades.

**Reference points:** Duolingo (streaks, XP), Snapchat (streaks as social contracts), Robinhood (confetti, free stock), sports betting apps (daily boosts).

---

## V5 — Fiat Integrations

**Plan:** [plan-v5-fiat-integrations.md](plan-v5-fiat-integrations.md)

Make MF Perps feel like a full fintech app with fiat deposit and withdrawal rails.

**What's included:**
- **Debit Card Deposit** — Instant fiat on-ramp via MoonPay/Transak.
- **Apple Pay Deposit** — Instant fiat on-ramp via Apple Pay SDK.
- **Bank Transfer Deposit** — ACH/bank transfer (1–2 business days) for higher limits.
- **Debit Card Off-Ramp** — Withdraw directly to a linked debit card (1–3 business days).
- **Bank Transfer Off-Ramp** — Withdraw to linked bank account via ACH/Plaid.
- **Regional Rails (Future)** — SEPA (EU), Faster Payments (UK), PIX (Brazil), UPI (India) identified for future regional expansion.

**Key principle:** Fiat methods become the primary deposit path, with crypto transfer as secondary. User enters dollars — fiat→stablecoin conversion is invisible.

---

## Version Dependencies

```
V1 MVP (Core Trading Loop)
 ├── V2 RWA Yield Exposure
 ├── V3 Referral Program
 ├── V4 Gamification
 └── V5 Fiat Integrations
```

All post-V1 versions build on V1 and can be developed independently of each other.
