# MF Perps DEX — UX Plan (V2 RWA Yield Exposure)

> **Prerequisite:** This builds on top of the V1 MVP core trading loop defined in [plan-v1-mvp.md](plan-v1-mvp.md). All features here layer onto the existing app without changing the core flows.

> **Scope:** RWA yield exposure — the "trojan horse" that converts perps traders into RWA yield users. Includes idle balance nudges, post-win prompts, portfolio yield card, and yield vault UX.

---

## Why V2?

The strategic differentiator for MF Perps is the bridge from speculation to real-world assets. But this only works if the core trading loop is proven first. V1 validates that users can onboard, deposit, trade, and withdraw with zero friction. V2 adds the yield layer once we have active traders to convert.

---

## Philosophy

We don't build a separate "RWA section". We **weave yield into the trading experience**.

- Yield is presented as "earn interest" — same language as a savings account.
- No mention of "RWA", "tokenization", "staking", or "liquidity provision".
- Users never need to understand that their yield comes from real-world assets.
- The complexity (RWA collateral, tokenization, yield sources) is available in an "About this vault" link for curious users.
- Show disclosure copy near every CTA: "Yield is variable, not guaranteed."

---

## V2 Features

### 1. Idle Balance Nudge

When a user has uninvested funds sitting in their account for 24+ hours:

```
┌─────────────────────────┐
│ 💰 Your $348.50 is      │
│    sitting idle          │
│                         │
│ Earn up to 8.2% target  │
│ APY (variable) on your  │
│ balance while you wait   │
│ for your next trade.     │
│                         │
│ [Earn Yield]  [Dismiss]  │
└─────────────────────────┘
```

- Appears as a card on the Home screen or as a bottom sheet after app open.
- Dismissable — respects user choice. Don't show again for 7 days after dismiss.
- "Earn Yield" navigates to a yield vault screen.

---

### 2. Post-Win Prompt

After closing a profitable position:

```
┌─────────────────────────┐
│ Nice trade! +$45.00 🎉   │
│                         │
│ Put your profits to work?│
│ Up to 8.2% target APY    │
│ (variable) on idle bal.  │
│                         │
│ [Earn on $45]  [Maybe Later]│
└─────────────────────────┘
```

- Shows as a card in the close-position success flow.
- Only appears after profitable closes, not losses.
- "Earn on $45" pre-fills the yield deposit amount with the profit.

---

### 3. Portfolio Yield Card

In the portfolio view, show a yield card alongside positions:

```
┌─────────────────────────┐
│ 🌱 Yield Vault           │
│ $200.00 earning up to     │
│ 8.2% target APY (variable)│
│ +$0.45 est. earned today  │
│ [Add More]  [Withdraw]    │
└─────────────────────────┘
```

- Card with subtle gradient border (accent to green).
- Shows current deposited amount, target APY, and estimated daily earnings.
- "Add More" opens yield deposit flow.
- "Withdraw" returns funds to trading balance instantly.
- Tiny disclosure text: "Not guaranteed."

---

### 4. Yield Vault Screen

Full detail screen for the yield product:

```
┌─────────────────────────┐
│ ← Yield Vault            │
│                          │
│ Your Balance  $200.00    │
│ Est. Daily    +$0.45     │
│ Target APY    8.2%       │
│ (variable, not guaranteed)│
│                          │
│ ┌──────────────────────┐ │
│ │ Deposit to Vault     │ │
│ └──────────────────────┘ │
│ ┌──────────────────────┐ │
│ │ Withdraw to Balance  │ │
│ └──────────────────────┘ │
│                          │
│ About this vault →       │
│                          │
│ Yield History            │
│ +$0.45 today             │
│ +$0.44 yesterday         │
│ +$0.43 2 days ago        │
└─────────────────────────┘
```

- Clean, savings-account-style interface.
- "About this vault" link expands to explain yield source for curious users (RWA collateral, tokenization details).
- Deposit/withdraw are instant from the user's perspective.

---

## Relationship to V1

V1 ships with no yield features. V2 adds:
- Idle balance nudge (Home screen + app open)
- Post-win yield prompt (close position flow)
- Portfolio yield card
- Yield vault screen
- Yield deposit/withdraw flows

See [plan-v1-mvp.md](plan-v1-mvp.md) for the V1 scope.

---

## Integration Dependencies

| Feature | Dependency | Complexity |
|---|---|---|
| Yield vault | RWA vault smart contract on MANTRA | High |
| Deposit to vault | Stablecoin → vault token conversion | Medium |
| Withdraw from vault | Vault token → stablecoin conversion | Medium |
| APY display | Yield oracle / rate feed | Medium |
| Yield history | On-chain yield tracking | Medium |

---

## Design Principles

1. **No jargon** — "Earn interest", not "stake", "provide liquidity", or "deposit into RWA vault".
2. **Always disclosed** — Every APY mention includes "variable" and "not guaranteed".
3. **Non-intrusive** — Nudges are dismissable and respect frequency caps.
4. **Instant UX** — Deposit/withdraw to vault feels instant, even if settlement takes a block or two.
5. **Trust through clarity** — "About this vault" is always accessible for users who want to understand the yield source.
