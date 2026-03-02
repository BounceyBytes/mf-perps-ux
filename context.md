# MF Perps DEX — Project Context

## Canonical Copy (Source of Truth)

Use these exact phrases across all docs and prototype specs to prevent wording drift.

| Area | Canonical wording |
|---|---|
| Onboarding promise | "Explore in 60 seconds" |
| Time-to-value statement | "~60 seconds to explore (+ KYC for live trading)" |
| KYC subtext | "Usually takes ~30 seconds. Verification helps keep the venue trusted." |
| Compliance value prop | "Stronger venue trust through verified access" |
| Execution wording | "Open Long/Short position (one-tap perp execution, Privy session keys for signing)" |
| Post-open actions | "View Position" / "Trade Again" / "Set TP/SL" |
| TP/SL expansion | "Set TP/SL" maps to "take profit / stop loss" controls |
| Yield teaser | "Earn up to 8.2% target APY (variable) on your idle balance" |
| Yield disclosure | "Not guaranteed" and "Yield is variable, not guaranteed." |
| Platform framing | "Platform target: React Native app on iOS & Android" + "30-day internal MVP delivery: Next.js clickable prototype" |

## Vision
Building the bridge from degen trading to real-world assets. A mobile-first perpetual futures DEX on MANTRA Finance that serves as a "trojan horse" — attract traders with best-in-class perps trading, then convert them into RWA yield users.

## Strategic Funnel
1. **ACQUIRE** — Mobile-first perps app catches degen traders where they live
2. **ENGAGE** — Best-in-class trading UX with deep liquidity and low fees
3. **EXPOSE** — Surface RWA yields alongside trading — show what real yield looks like
4. **CONVERT** — Users move capital from speculation into productive RWA collateral

## Competitive Landscape

### HyperLiquid
- 60%+ of all perpetual DEX open interest
- Fastest-growing protocol in DeFi
- Desktop-first UX — clunky on mobile
- No KYC — anonymous counterparties
- No RWA integration — pure speculation

### DreamCash (Direct Competitor)
- Mobile app for perps trading
- Crypto-native UX with heavy onboarding education
- Wallet management, seed phrases, QR code funding
- Requires crypto literacy to use effectively

## Our Edge
1. **Mobile-First** — Native app from day one. Built for how traders actually trade.
2. **MANTRA Finance Regulation** — Regulatory-compliant infra from L1 to dApp. KYC is a feature — stronger trust and accountability in the venue.
3. **Trojan Horse** — Attract perps traders -> expose them to RWA yields -> convert to full platform users.

## Key Technology Decisions
- **Embedded Wallet: Privy** — Handles social login (Apple, Google, email/phone), automatic wallet creation, and session key management. Users never see a wallet, seed phrase, or signing modal. Privy abstracts the entire on-chain identity layer.
- **Auth flows through Privy** — Apple/Google/email sign-in, biometric re-auth, and wallet creation are all handled by Privy's SDK in a single integration.

## Growth Strategy
- **Referral-led acquisition (V3)** — Referral codes, shareable invite links, fee rebates. See [plan-v3-referral-program.md](plan-v3-referral-program.md).
- **Gamification for retention (V4)** — Daily streaks, XP, levels, challenges, and leaderboards. See [plan-v4-gamification.md](plan-v4-gamification.md).

## MVP Targets
- **Timeline**: 30 days to internal MVP
- **Pairs**: BTC, ETH + additional pairs
- **Platform target**: React Native app on iOS & Android
- **MVP delivery format (30-day internal)**: high-fidelity clickable prototype in Next.js to validate UX and flows before React Native build-out
- **UX North Star**: A user who knows nothing about crypto should be able to trade with zero friction

## DreamCash User Journeys (Reference)
The following journeys were mapped from the DreamCash app:

### Summary Flow
Onboarding → Funding → Open Position (Long/Short) → Watch Position → Close Position → Withdrawal
- Branch: Swap on Spot (from Funding)

### Onboarding (DreamCash)
Sign up → Enter code/join → Pick username → Welcome animation → Enable Face ID → Import/export wallet → Trade with money → Share positions with leverage → Understand liquidation → Manage portfolio → Choose funding → Enter referral code → Points/rewards system

### Funding (DreamCash)
Wallet overview ($0.00) → View assets → Deposit options → Select method → Buy crypto → QR code / address → Confirmation

### Open LONG Position (DreamCash)
Market list → Select pair (e.g. Pepe) → View chart ($67,156) → Enter amount ($15) → Set leverage (100x) → Review position ($300) → Confirm order details → Sign transaction → Position opened

### Open SHORT Position (DreamCash)
Market list → Select pair → View chart ($83.98) → Enter amount ($15) → Set leverage → Adjust size → Review ($299.8) → Confirm → Sign transaction → Position opened

### Close Position (DreamCash)
Open positions list → Select position ($67,071) → View position detail → Close/reduce → Confirm close → Settlement ($60.19)

## Key UX Problems in DreamCash
- Crypto-native onboarding (wallet setup, seed phrases, Face ID for signing)
- Requires understanding of wallets, gas, transaction signing
- Funding requires owning crypto already or navigating fiat-to-crypto separately
- Jargon-heavy (liquidation, collateral, gas, slippage)
- Education screens add friction rather than removing complexity
