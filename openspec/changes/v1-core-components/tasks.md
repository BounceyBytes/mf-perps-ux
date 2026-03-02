## 1. Zustand Store & Mock Data

- [ ] 1.1 Create `src/lib/store.ts` with screen state (default 'welcome'), overlay state (default null), selectedPair (default 'BTC/USD'), and navigate/showOverlay/dismissOverlay functions
- [ ] 1.2 Create `src/lib/mock-data.ts` with markets (7 pairs), openPositions (2 positions), and user objects matching the build guide types

## 2. Phone Frame Components

- [ ] 2.1 Create `src/components/PhoneFrame.tsx` — centered 390×844 container with rounded-[40px] corners, border, bg-background, overflow-y-auto hidden scrollbar, outer page bg #1a1a1a
- [ ] 2.2 Create `src/components/StatusBar.tsx` — fake iOS status bar with "9:41" time, signal/wifi/battery icons, white text, absolute positioned at top

## 3. Base Components

- [ ] 3.1 Create `src/components/Button.tsx` — variant prop (primary/secondary/ghost), rounded-xl, font-semibold, full-width default, Framer Motion whileTap scale 0.97
- [ ] 3.2 Create `src/components/Card.tsx` — surface bg, rounded-2xl, p-4, subtle border
- [ ] 3.3 Create `src/components/Input.tsx` — surface-light bg, rounded-xl, text-primary, text-muted placeholder, accent focus ring

## 4. Bottom Navigation

- [ ] 4.1 Create `src/components/BottomNav.tsx` — three tabs (Home/Trade/Portfolio) with Lucide icons, labels in text-xs, active tab in accent color, inactive in text-muted, surface bg with top border, fixed at bottom, navigate on tap

## 5. App Shell Wiring

- [ ] 5.1 Update `src/app/page.tsx` to render PhoneFrame with StatusBar, screen router (switch on store.screen), overlay layer (switch on store.overlay), and conditional BottomNav (only on home/trade/portfolio)
- [ ] 5.2 Verify the app runs and shows an empty phone frame with status bar on dark background
