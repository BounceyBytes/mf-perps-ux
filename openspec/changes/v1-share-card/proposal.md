## Why

After a user opens a winning position, there is no way to celebrate or share their success. A share card overlay gives users a polished, branded visual they can screenshot or share — driving social proof and organic referrals through a built-in referral link and QR code. This is Screen 13 in the prototype flow.

## What Changes

- Create `ShareCard` component (`src/components/overlays/ShareCard.tsx`) — a full-screen Framer Motion overlay that renders when `store.overlay === 'share-card'`
- Overlay: full screen within phone frame, `bg-black/80` backdrop, centered layout
- Share card (max-w-[320px], rounded-2xl, overflow-hidden): gradient background from surface (#14141F) to purple-tinted dark (#1a1530), top accent bar (4px, green gradient for long/winning positions), position info ("🟢 BTC Long", hero PnL "+47.2%", dollar breakdown "$500 → $735.00"), user info (avatar + name), divider, referral area ("Trade on MF Perps", referral link, QR placeholder)
- Below card: "Share" primary button with Share2 icon, "Save Image" secondary button with Download icon, "Done" text link to dismiss
- Card entrance animation: scale 0.8→1 + opacity 0→1 via Framer Motion
- Share and Save buttons show prototype toasts ("Shared!" / "Saved!")
- Wire overlay into the overlay layer in `page.tsx`

## Capabilities

### New Capabilities
- `share-card`: Full-screen overlay displaying a sharable position card with PnL, referral link, QR placeholder, and share/save actions

### Modified Capabilities

## Impact

- Adds 1 new file under `src/components/overlays/`
- Updates `page.tsx` overlay layer to render ShareCard when `store.overlay === 'share-card'`
- Depends on: PhoneFrame, Button, Zustand store (from core-components change)
- Depends on: position data from store (pair, direction, entryPrice, currentPrice, amount, leverage, user info)
- May be triggered from portfolio screen or trade-confirmation flow in the future
