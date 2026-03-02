# MF Perps DEX — UX Plan (V3 Referral Program)

> **Prerequisite:** This builds on top of the V1 MVP core trading loop defined in [plan-v1-mvp.md](plan-v1-mvp.md). All features here layer onto the existing app without changing the core flows.

> **Scope:** Referral program — invite codes, shareable deep links, fee rebates, referral surfaces throughout the app, and onboarding referral screen.

---

## Why V3?

Referrals are a growth engine, but they add complexity to onboarding (extra screen), require backend infrastructure (code generation, tracking, fee rebates), and introduce abuse vectors (self-referral, velocity gaming). V1 focuses on validating the core trading loop. V3 adds the referral layer once we have a product worth referring.

---

## Philosophy

Referrals aren't a feature — they're a **growth engine built into the product surface**.

- Every user gets a referral identity on signup.
- Sharing a win *is* a referral. The share card includes the invite link.
- Referral entry is low-friction and optional during onboarding.
- Rewards are clear and mutual — both referrer and referee benefit.

---

## V3 Features

### 1. Referral Identity

**Every user gets a referral identity on signup:**
- A unique invite code (auto-generated, editable once — e.g. "JAKE2026")
- A shareable deep link: `mfperps.app/join/JAKE2026`

---

### 2. Onboarding Referral Screen

Added as an optional screen between KYC and "You're In":

```
┌─────────────────────────┐
│                         │
│   Got an invite code?   │
│                         │
│   ┌───────────────────┐ │
│   │                   │ │
│   │  Enter code       │ │
│   │                   │ │
│   └───────────────────┘ │
│                         │
│   You'll both earn      │
│   trading rewards       │
│                         │
│   ┌───────────────────┐ │
│   │     Continue      │ │
│   └───────────────────┘ │
│                         │
│        Skip →           │
│                         │
└─────────────────────────┘
```

- **Shown to every user** — referrals are critical for early growth, so we ask. But it's zero-friction: one optional text field, a skip link, and a continue button.
- **"You'll both earn trading rewards"** — clear mutual incentive in one line. No lengthy explanation of the program.
- **Deep link pre-fill**: If the user came via a referral link (shared from another user), the code is already filled in and this screen just confirms it. "Invited by @Jake — you'll both earn rewards. [Continue]"
- **Skip is always visible** — no one gets stuck here.
- Takes 3 seconds to skip, 5 seconds to enter a code. Acceptable friction for the growth upside.

---

### 3. Referrer Rewards

- **Fee rebate**: Earn up to 10% of your referrals' trading fees for a defined promotional window (e.g., first 12 months).
- **Tier multipliers**: Tiered boosts are gated behind economics and abuse-review, then enabled progressively.

> **V4 addition:** Referrals also earn XP bonuses when referred friends complete key actions. See [plan-v4-gamification.md](plan-v4-gamification.md).

---

### 4. Referral Surfaces in the App

**Where referrals surface:**

1. **Onboarding** — Optional referral code entry screen (see above).

2. **Share position card** — When sharing a winning trade, the share image includes your referral code and a QR. Your flex *is* your referral.
   ```
   ┌─────────────────────────┐
   │  🟢 BTC Long  +47.2%    │
   │  $500 → $735.00         │
   │                         │
   │  Trade on MF Perps      │
   │  mfperps.app/join/JAKE  │
   │  [QR Code]              │
   └─────────────────────────┘
   ```

3. **Portfolio / profile area** — "Invite friends" card showing:
   ```
   ┌─────────────────────────┐
   │  Invite & Earn           │
   │  3 friends joined        │
   │  $12.40 earned from fees │
   │                         │
   │  [Share Invite Link]     │
   │  Your code: JAKE2026    │
   └─────────────────────────┘
   ```

4. **Post-trade prompt** (occasional, not every time) — After a good trade: "Share this win? Your referral link is included."

5. **Milestone nudges** — "You're 2 referrals away from Ambassador! Share your link."

---

### 5. Referral Dashboard

Accessible from profile/settings:

```
┌─────────────────────────┐
│ ← Referrals              │
│                          │
│ Your Code: JAKE2026      │
│ [Copy Link]  [Share]     │
│                          │
│ 3 friends joined         │
│ $12.40 earned from fees  │
│                          │
│ Referral History         │
│ @sarah — joined 2d ago   │
│ @mike — joined 1w ago    │
│ @lisa — joined 2w ago    │
│                          │
│ Fee Rebate: 10%          │
│ Active until Dec 2026    │
└─────────────────────────┘
```

---

## Risk Controls

- Self-referral detection (device fingerprinting, IP matching).
- Velocity checks — flag accounts creating many referrals rapidly.
- Payout holds — fee rebates held for review period before release.
- Abuse review — manual review for outlier referral patterns.

---

## Relationship to V1

V1 ships with no referral features. V3 adds:
- Referral code generation for every user
- Onboarding referral screen (optional)
- Shareable invite links
- Share card with embedded referral code + QR
- Portfolio "Invite & Earn" card
- Referral dashboard
- Fee rebate tracking

See [plan-v1-mvp.md](plan-v1-mvp.md) for the V1 scope.

---

## Integration Dependencies

| Feature | Dependency | Complexity |
|---|---|---|
| Code generation | Backend service | Low |
| Deep links | Mobile deep link handling | Medium |
| Fee rebate tracking | Trading fee attribution | Medium-High |
| Referral dashboard | Backend API + frontend | Medium |
| Abuse detection | Device fingerprinting, analytics | Medium-High |
