## 1. MarketRow Component

- [ ] 1.1 Create `src/components/MarketRow.tsx` accepting pair (string), price (string), and change24h (number) props
- [ ] 1.2 Render horizontal layout: pair name (text-sm font-semibold left), price (text-sm tabular-nums right-aligned), change% (text-sm, green #00D68F if positive with "+" prefix, red #FF4757 if negative), ChevronRight icon (text-muted far right)
- [ ] 1.3 Add subtle bottom border (border-b border-border) to each row
- [ ] 1.4 Wire tap handler to set `store.selectedPair` to the row's pair and call `store.navigate('trade')`

## 2. HomeScreen Layout

- [ ] 2.1 Create `src/components/screens/HomeScreen.tsx` with scrollable container (px-4 pt-2 pb-24 overflow-y-auto)
- [ ] 2.2 Add header row: Menu icon (left), "MF Perps" text-lg font-bold (center), "$648.50" balance text-sm font-semibold (right) using flex justify-between items-center
- [ ] 2.3 Wire balance tap to call `store.navigate('portfolio')`

## 3. Trending Section

- [ ] 3.1 Add "🔥 Trending" section header (mt-4, text-xs uppercase tracking-wider text-muted)
- [ ] 3.2 Sort mock markets by absolute change24h descending, render top 3 as MarketRow components

## 4. Watchlist Section

- [ ] 4.1 Add "Your Watchlist" section header (mt-4, text-xs uppercase tracking-wider text-muted)
- [ ] 4.2 Render MarketRow for BTC/USD and ETH/USD from mock data
- [ ] 4.3 Add "+ Add market" row with Plus icon in accent color (#7B61FF) and text-sm text-accent (decorative only, no action)

## 5. Top Movers Section

- [ ] 5.1 Add "Top Movers" section header (mt-4, text-xs uppercase tracking-wider text-muted)
- [ ] 5.2 Render horizontal scrollable container (flex overflow-x-auto gap-3, hide scrollbar) with small cards (w-24, surface bg, rounded-xl, p-3) for each mock market
- [ ] 5.3 Each card shows pair name (text-xs font-semibold) and change% (text-sm, green/red colored)
- [ ] 5.4 Wire tap on each card to set selectedPair and navigate to 'trade'

## 6. App Shell Wiring

- [ ] 6.1 Add HomeScreen to the screen router in `page.tsx` so it renders when `store.screen === 'home'`
- [ ] 6.2 Confirm BottomNav renders with Home as active tab when on this screen

## 7. Verification

- [ ] 7.1 Run the app and confirm the Home screen renders inside PhoneFrame with header, three sections, and BottomNav
- [ ] 7.2 Tap a MarketRow and confirm navigation to 'trade' with the correct selectedPair
- [ ] 7.3 Tap the balance and confirm navigation to 'portfolio'
- [ ] 7.4 Confirm Top Movers scrolls horizontally and all cards display correctly
