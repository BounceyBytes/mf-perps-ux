# MF Perps UX — Build Guide (V4 Gamification)

> **Prerequisite:** The V1 MVP prototype must be built first. See [build-v1-mvp.md](build-v1-mvp.md) for the core app. This guide adds gamification features on top of that foundation.

> **Scope:** XP & levels, streaks, daily/weekly challenges, leaderboards, achievement badges, reward drops, and gamification integration into existing V1 screens (Home, Trade Confirmation, Share Card).

## Overview
Layer gamification features onto the existing V1 prototype. These features add retention mechanics and social engagement without changing the core trading loop. All new screens render inside the same phone frame, using the same design tokens and navigation system.

## Additional Dependencies
No new dependencies needed — V1 already includes Framer Motion, Lucide React, and Zustand.

## Additional Components

Add these to the existing `src/components/` directory:

```
src/components/
├── ... (all V1 components)
├── StreakWidget.tsx    # Fire icon + day count + calendar dots
├── ChallengeCard.tsx   # Daily challenge with progress bar
├── BadgeIcon.tsx       # Achievement badge display
└── RewardDrop.tsx      # Mystery reward reveal animation
```

## Additional Screens

Add these to the existing `src/screens/` directory:

```
src/screens/
├── ... (all V1 screens 01-13)
├── 14-Profile.tsx
├── 15-Challenges.tsx
├── 16-Leaderboard.tsx
└── 17-RewardDrop.tsx
```

## Navigation Extensions

Extend the Zustand store types:

```typescript
// Additions to src/lib/store.ts

// Add to Screen type:
type Screen =
  | ... // all V1 screens
  | 'leaderboard' | 'profile' | 'challenges';

// Add to Overlay type:
type Overlay =
  | ... // all V1 overlays
  | 'reward-drop';
```

## Additional Mock Data

Add to `src/lib/mock-data.ts`:

```typescript
// Extend the user object:
export const user = {
  ...// V1 fields
  level: 12,
  xp: 3450,
  xpToNext: 6000,
  streak: 12,
};

export const dailyChallenges = [
  { id: '1', icon: '📊', title: 'Market Scout', desc: 'View 5 different markets', xp: 100, progress: 4, target: 5 },
  { id: '2', icon: '🎯', title: 'Quick Trade', desc: 'Open and close a position', xp: 100, progress: 0, target: 1 },
  { id: '3', icon: '🔍', title: 'Set Alert', desc: 'Set a price alert on any market', xp: 100, progress: 0, target: 1 },
];

export const weeklyChallenges = [
  { id: 'w1', icon: '🎲', title: 'Diversify', desc: 'Trade 3 different pairs', xp: 500, progress: 1, target: 3 },
  { id: 'w2', icon: '🔥', title: 'Streak Master', desc: 'Maintain your streak all week', xp: 500, progress: 5, target: 7 },
  { id: 'w3', icon: '👥', title: 'Recruiter', desc: 'Refer a friend who trades', xp: 1000, progress: 0, target: 1 },
];

export const badges = [
  { id: 'first-blood', name: 'First Blood', desc: 'Close your first trade', earned: true },
  { id: 'on-fire', name: 'On Fire', desc: '7-day streak', earned: true },
  { id: 'veteran', name: 'Veteran', desc: '30-day streak', earned: false },
  { id: 'century', name: 'Century', desc: '100-day streak', earned: false },
  { id: 'sharp-shooter', name: 'Sharp Shooter', desc: '5 profitable trades in a row', earned: false },
  { id: 'whale-watcher', name: 'Whale Watcher', desc: 'Trade $10,000+ volume', earned: false },
  { id: 'diversified', name: 'Diversified', desc: 'Trade 5 different pairs', earned: true },
  { id: 'ambassador', name: 'Ambassador', desc: 'Refer 10 active traders', earned: false },
  { id: 'diamond-hands', name: 'Diamond Hands', desc: 'Hold a position for 7+ days', earned: false },
  { id: 'speed-demon', name: 'Speed Demon', desc: 'Trade within 60 seconds', earned: false },
  { id: 'early-adopter', name: 'Early Adopter', desc: 'Signed up during beta', earned: true },
];

export const leaderboard = [
  { rank: 1, name: 'cryptoKing', pnl: 142.3 },
  { rank: 2, name: 'degenQueen', pnl: 98.7 },
  { rank: 3, name: 'tradeBro', pnl: 87.1 },
  { rank: 4, name: 'whale99', pnl: 72.4 },
  { rank: 5, name: 'moonshot', pnl: 65.8 },
  { rank: 6, name: 'rektproof', pnl: 54.2 },
  { rank: 7, name: 'leverageKid', pnl: 48.9 },
  { rank: 8, name: 'hodlqueen', pnl: 41.3 },
  { rank: 9, name: 'apeDegen', pnl: 38.7 },
  { rank: 10, name: 'sigmaTrader', pnl: 35.1 },
];
```

## Component Specs

### StreakWidget
**File:** `src/components/StreakWidget.tsx`

- Horizontal layout: fire emoji "🔥", streak count "12 day streak" in text-sm font-semibold text-orange, and on the far right "Lv. 12" in text-sm text-accent with a tiny XP bar below it (4px tall, accent color fill, surface bg, rounded-full, 60px wide, 57% filled representing 3450/6000 XP).
- Wrapped in a Card with reduced padding (py-2 px-4).
- Fire emoji should have a subtle glow animation (text-shadow pulse).

### ChallengeCard
**File:** `src/components/ChallengeCard.tsx`

- Props: icon (string emoji), title, description, xpReward, progress, target.
- Card component layout: icon + title on top row, description in text-xs text-secondary below, then a progress bar (h-1.5, rounded-full, accent fill over surface bg) with "4/5" text on the right, and "100 XP" reward badge in text-xs text-accent on the far right.
- Tappable — whole card navigates to 'challenges' screen.
- Progress bar should animate from 0% to current value on mount (500ms).

### BadgeIcon
**File:** `src/components/BadgeIcon.tsx`

- Props: name (string), earned (boolean), icon (emoji string).
- Size: w-16 h-16, rounded-2xl.
- Earned: surface-light bg, emoji centred in text-2xl, name below in text-xs text-primary.
- Unearned: surface bg, opacity-30, emoji centred, name in text-xs text-muted. Locked lock emoji overlay in corner.

Badge emoji mapping:
| Badge | Emoji |
|---|---|
| First Blood | ⚔️ |
| On Fire | 🔥 |
| Veteran | 🎖️ |
| Century | 💯 |
| Sharp Shooter | 🎯 |
| Whale Watcher | 🐋 |
| Diversified | 🎨 |
| Ambassador | 👑 |
| Diamond Hands | 💎 |
| Speed Demon | ⚡ |
| Early Adopter | 🌟 |

### RewardDrop
**File:** `src/components/RewardDrop.tsx` (or `src/screens/17-RewardDrop.tsx`)

Full-screen overlay with two states: unrevealed and revealed.

**State 1: Unrevealed**
- Full screen within phone frame, bg-black/70 with backdrop-blur-sm. Content centred.
- A card (w-64 h-80, rounded-3xl, surface bg) with:
  - Animated glowing border: pulsing box-shadow in accent color.
  - "✨ Reward Drop! ✨" in text-xl font-bold, centred in top third.
  - Three large "? ? ?" in text-4xl text-muted, floating animation (y oscillating ±5px).
  - "Tap to reveal" in text-sm text-secondary, bottom third.
- Card pulses subtly (scale 1→1.02→1, infinite loop, 2s).

**State 2: Revealed (after tap)**
- Card flips (rotateY 0→180→360) or scales down then up with new content.
- New content:
  - "🎉" in text-4xl, centred.
  - "You got:" in text-sm text-secondary.
  - Reward name in text-2xl font-bold text-accent (randomly selected).
  - Description in text-sm text-secondary, mt-2.
  - Primary Button "Nice!" at bottom.
- Optional confetti particles on reveal.

**Possible rewards (randomly select one):**
- "Fee-free trade!" / "Your next trade has zero fees."
- "2x XP for 24 hours" / "All XP earned is doubled until tomorrow."
- "150 Bonus XP" / "Added to your XP balance."
- "Streak Freeze" / "Banked for later. Use it to protect your streak."

---

## Screen Specs

### Screen 14: Profile
**Accessible from:** Hamburger menu or avatar tap

**Layout (scrollable, px-4, pt-4, pb-24):**
1. **Header:** back arrow + "Profile" centred.
2. **User card (mt-4):** Card with centred layout — avatar circle (w-16 h-16, rounded-full, accent bg, "J" initial), "Jake" name, "Level 12" badge in text-sm text-accent.
3. **Level progress card (mt-4):** "Level 12" + "3,450 / 6,000 XP", progress bar (h-2, accent fill, 57.5%), "Next: Unlock 50x leverage" text.
4. **Stats row (mt-4):** Three stat boxes: "127 Trades", "64% Win Rate", "+$340 Best Trade".
5. **Streak section (mt-4):** Card with "🔥 12 day streak", calendar grid (M-S, filled/empty dots), "Personal best: 23 days".
6. **Badges section (mt-4):** "Badges 4/11" header, grid of BadgeIcons (3 columns).
7. **Invite & Earn card (mt-4):** "3 friends joined · $12.40 earned · 850 XP from referrals", Share button, code display.

**Interactions:**
- Share Invite Link → "Link copied!" toast.
- Badge tap → tooltip with name/description (optional stretch).

---

### Screen 15: Challenges
**Accessible from:** Home screen challenge card tap

**Layout (scrollable, px-4, pt-2, pb-24):**
1. **Header:** back arrow + "Challenges" centred.
2. **"Today's Challenges" section (mt-4):** 3 ChallengeCard components from dailyChallenges mock data. Below: "Complete any 1 for daily bonus".
3. **"This Week" section (mt-6):** 3 larger challenge cards from weeklyChallenges. Each shows emoji + title, XP reward, progress bar.
4. **"Completed Today" section (mt-6):** One completed card (opacity-60, green checkmark, "Done ✓").

**Interactions:**
- Cards stagger in on mount.

---

### Screen 16: Leaderboard
**Accessible from:** Home screen or Profile

**Layout (px-4, pt-2, pb-24):**
1. **Header:** back arrow + "Leaderboard" centred + "This Week" badge.
2. **Tab pills (mt-3):** "P&L %", "Volume", "Streaks". Default: P&L % active (accent bg).
3. **Top 3 podium (mt-6):** Three cards side by side — #1 centre (larger, gold border), #2 left (silver), #3 right (bronze). Each: medal emoji, username, stat.
4. **Ranked list (mt-4):** Rows 4-10, each: rank, username, P&L stat. Subtle row borders.
5. **Divider (mt-4).**
6. **Your rank (pinned, mt-2):** Highlighted row "127. You +12.3%" with surface-light bg.
7. **Footer (mt-4):** "Top 10 earn bonus XP · Top 3 earn fee rebates" in text-xs text-secondary.

**Interactions:**
- Tab pills switch views (placeholder data for Volume/Streaks if needed).
- Podium cards scale up with spring animation on mount.
- List items stagger in.

---

## V1 Screen Modifications

### Home Screen (05-Home.tsx) — Add Gamification
Insert between the header row and the first content section:
1. **StreakWidget** component (mt-3).
2. **"Today's Challenge" section (mt-4):** Section header in text-xs uppercase, then a single ChallengeCard showing the first daily challenge. Tappable → 'challenges'.

Everything else on the Home screen stays unchanged.

### Trade Confirmation (09-TradeConfirmation.tsx) — Add XP + Reward Drop
1. Add after summary card: "+25 XP earned" line in text-sm text-accent with sparkle icon.
2. After dismissal (either button tap), implement: `if (Math.random() < 0.3)` → show 'reward-drop' overlay after 500ms delay.

### Share Card (13-ShareCard.tsx) — Add Gamification Display
Enhance the user info row to include:
- "Level 12" badge next to name.
- "🔥 12" streak count.
- 1-2 earned badge emojis.

---

## Build Order (V4 Phase)

Build after V1 is complete:

**Phase 7: Gamification Foundations**
1. Extend mock-data.ts with gamification data
2. Extend store.ts with new screens/overlays
3. Build StreakWidget, ChallengeCard, BadgeIcon components

**Phase 8: New Screens**
4. Screen 14 (Profile) — uses BadgeIcon, StreakWidget data
5. Screen 15 (Challenges) — uses ChallengeCard
6. Screen 16 (Leaderboard)
7. Screen 17 / RewardDrop component

**Phase 9: V1 Screen Integration**
8. Modify Home screen to add StreakWidget + ChallengeCard
9. Modify Trade Confirmation to add XP line + Reward Drop trigger
10. Modify Share Card to add level/badge display

**Phase 10: Gamification Polish**
11. XP toast animation (floating "+25 XP" text)
12. Badge earned celebration overlay
13. Level up animation
14. Screen transitions for new screens (slide up from bottom)
15. Streak fire glow animation
16. Challenge progress bar mount animation

## Key Notes for Agents
- **Build V1 first** — all gamification layers on top of existing screens and components.
- **Read `plan-v4-gamification.md`** — it has the full design rationale for every gamification feature.
- **Don't break V1** — gamification additions should be additive. The core trading flow must still work exactly as before.
- **Animations are critical** — Reward Drops, badge celebrations, and level-up animations are the dopamine hits. Make them feel premium.
- **XP is everywhere** — It should feel like every meaningful action rewards you, but never in an annoying or interruptive way. Subtle toasts, not modals.
