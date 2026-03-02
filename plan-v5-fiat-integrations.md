# MF Perps DEX — UX Plan (V5 Fiat Integrations)

> **Scope:** Fiat on-ramp and off-ramp integrations deferred from V1. V1 ships with crypto transfer (external wallet) for deposits and external wallet withdrawal only. V5 adds fiat deposit rails (Debit Card, Apple Pay), fiat off-ramps, and additional payment methods to make MF Perps feel like a full fintech app.

---

## Why V5?

V1 prioritises getting users trading fast with the fewest integration dependencies. Fiat on-ramps and off-ramps add significant third-party complexity (payment processor contracts, compliance review, settlement flows, chargeback handling) without improving the core trading loop. V1 uses crypto transfer only for deposits. We add fiat rails once the trading experience is validated and user demand is proven.

---

## V5 Features

### 1. Debit Card Deposit (On-Ramp)

**What:** Allow users to deposit funds instantly via debit card.

**Deposit screen addition:**
```
┌───────────────────┐
│ 💳 Debit Card     │
│    Instant         │
└───────────────────┘
```

- Appears above Transfer Crypto card on the deposit screen.
- Navigates to 'deposit-amount' screen for dollar amount entry.
- Requires fiat on-ramp partner integration (e.g. MoonPay, Transak).
- Instant settlement from user's perspective (fiat→stablecoin handled behind the scenes).

---

### 2. Apple Pay Deposit (On-Ramp)

**What:** Allow users to deposit funds instantly via Apple Pay.

**Deposit screen addition:**
```
┌───────────────────┐
│  Apple Pay        │
│    Instant         │
└───────────────────┘
```

- Appears below Debit Card, above Transfer Crypto card.
- Navigates to 'deposit-amount' screen for dollar amount entry.
- Requires Apple Pay SDK integration via on-ramp partner.
- Instant settlement from user's perspective.

**UX considerations for both fiat deposit methods:**
- When fiat on-ramps are added, the deposit screen shows Debit Card and Apple Pay above a divider ("or"), with Transfer Crypto below. Fiat methods are the primary path; crypto transfer is secondary.
- User enters a dollar amount. Fiat→stablecoin conversion is handled behind the scenes.

---

### 3. Debit Card Off-Ramp (Withdraw to Card)

**What:** Allow users to withdraw funds directly to a linked debit card.

**Withdraw screen addition:**
```
┌───────────────────┐
│ 💳 Debit Card     │
│    **** 4829       │
│    1-3 business days│
└───────────────────┘
```

- Remembers previously used card from deposit.
- "Withdraw back to card **** 4829" — one-tap familiar path.
- Requires fiat off-ramp partner integration (e.g. MoonPay, Transak off-ramp API).
- Settlement: 1-3 business days typical.
- Must handle compliance holds, KYC re-verification for large withdrawals, and chargeback-reversal edge cases.

**UX considerations:**
- When card off-ramp is available alongside external wallet, the withdraw screen shows both options. Tapping either card initiates the withdrawal — no separate CTA button (same pattern as V1 external wallet).
- Card should be the default/top option for users who deposited via card (match the funding method).

---

### 4. Bank Transfer Deposit

**What:** Allow users to fund their account via ACH / bank transfer.

**Deposit screen addition:**
```
┌───────────────────┐
│ 🏦 Bank Transfer  │
│    1-2 business days│
└───────────────────┘
```

- Appears below Apple Pay, above the "or" crypto divider.
- Slower settlement (1-2 business days) — show clear ETA and push notification on arrival.
- Higher limits than card typically — good for larger deposits.
- Requires bank linking flow (Plaid or similar) or manual ACH details.

**UX considerations:**
- While transfer is pending, show a "Pending deposit" card in the portfolio view with ETA and amount.
- Consider allowing users to trade on a portion of pending funds (credit line model) if risk-appropriate.

---

### 5. Bank Transfer Off-Ramp (Withdraw to Bank)

**What:** Allow users to withdraw directly to a linked bank account.

- Same bank linking as deposit (Plaid).
- Settlement: 1-3 business days (ACH) or same-day for supported banks.
- Useful for larger withdrawals where card limits are restrictive.

---

### 6. Additional Fiat Rails (Regional)

Future consideration based on user geography:
- **SEPA (EU)** — instant or 1-day bank transfers for European users.
- **Faster Payments (UK)** — near-instant GBP transfers.
- **PIX (Brazil)** — instant transfers if LatAm expansion occurs.
- **UPI (India)** — if Indian market is targeted.

These are identified here for planning but not scoped in detail until regional expansion strategy is defined.

---

## Integration Dependencies

| Rail | Direction | Likely Partner | Settlement | Complexity |
|---|---|---|---|---|
| Debit Card | On-ramp | MoonPay / Transak | Instant | Medium |
| Apple Pay | On-ramp | MoonPay / Transak | Instant | Medium |
| Debit Card | Off-ramp | MoonPay / Transak | 1-3 days | Medium |
| Bank Transfer (ACH) | On-ramp | MoonPay / Plaid | 1-2 days | Medium-High |
| Bank Transfer (ACH) | Off-ramp | MoonPay / Plaid | 1-3 days | Medium-High |
| SEPA / Faster Payments | Both | TBD | Instant-1 day | High (regulatory) |

---

## Relationship to V1

V1 ships with:
- **Deposits:** Transfer Crypto (from external wallet)
- **Withdrawals:** External Wallet only (instant)

V5 adds:
- **Deposits:** Debit Card (instant), Apple Pay (instant), Bank Transfer
- **Withdrawals:** Debit Card, Bank Transfer
- **Future:** Regional fiat rails

See [plan-v1-mvp.md](plan-v1-mvp.md) for the V1 scope.
