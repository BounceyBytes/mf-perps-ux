# MF Perps DEX — UX Plan (V4 Gamification)

> **Prerequisite:** This builds on top of the V1 MVP core trading loop defined in [plan-v1-mvp.md](plan-v1-mvp.md). All features here layer onto the existing app without changing the core flows.

> **Scope:** XP & levels, streaks, daily/weekly challenges, leaderboards, achievement badges, reward drops, and gamification integration across existing screens.

---

## 10. Gamification — Daily Retention Engine

### Philosophy
Perps traders are already wired for dopamine. We don't need to create the urge — we need to **give it structure**. The gamification layer turns sporadic "check my position" visits into a daily habit loop, even when a user has no open positions.

Our reference points: **Duolingo** (streaks, XP, leagues), **Snapchat** (streaks as social contracts), **Robinhood** (confetti, free stock rewards), and **sports betting apps** (daily boosts, parlays, challenges).

---

### 10a. XP & Levels

Every action earns XP. XP accumulates into levels. Levels unlock tangible perks.

**XP Sources:**
| Action | XP |
|---|---|
| Daily login | 10 XP |
| Open a position | 25 XP |
| Close a profitable trade | 50 XP |
| Close any trade | 15 XP |
| Complete a daily challenge | 100 XP |
| Complete a weekly challenge | 500 XP |
| Refer a friend (signs up) | 200 XP |
| Referred friend's first trade | 300 XP |
| Deposit funds | 50 XP |
| 7-day streak | 150 XP bonus |
| 30-day streak | 1000 XP bonus |

**Level Progression:**
| Level | XP Required | Perk Unlocked |
|---|---|---|
| 1 | 0 | Basic access |
| 5 | 1,000 | Unlock 25x leverage cap |
| 10 | 3,000 | Fee discount: 5% off |
| 15 | 6,000 | Unlock 50x leverage cap |
| 20 | 10,000 | Fee discount: 10% off |
| 25 | 15,000 | Unlock 100x leverage cap |
| 30 | 25,000 | Fee discount: 15% off + custom profile badge |
| 50 | 75,000 | "OG Trader" badge + early access to new features |

- Leverage caps tied to levels protect new users *and* give experienced traders something to progress toward. This replaces the awkward "first trade at 10x max" rule with a proper system.
- Fee discounts are the killer perk — they have real dollar value and get better the more you trade.

**Level display:**
```
┌─────────────────────────┐
│ Level 12        3,450 XP│
│ ████████░░░░  → Level 15│
│ Next: Unlock 50x leverage│
└─────────────────────────┘
```
- Shown in the profile/menu area and subtly on the home screen.
- The progress bar and "next perk" creates a constant pull toward the next milestone.

---

### 10b. Streaks

**Daily streak** — Log in and perform any action (check portfolio, view a market, place a trade) to maintain your streak.

```
Home Screen (streak widget)
┌─────────────────────────┐
│ 🔥 12 day streak        │
│ M T W T F S S           │
│ ✓ ✓ ✓ ✓ ✓ ✓ ✓           │
│ ✓ ✓ ✓ ✓ ✓ ·  ·          │
│                         │
│ Keep it going!          │
└─────────────────────────┘
```

**Design decisions:**
- **Low bar to maintain**: You don't have to trade. Just open the app and look at something. This drives daily opens without encouraging reckless trading.
- **Streak freeze**: Users can "freeze" their streak once per week (earned or purchased with XP) — prevents frustration from a single missed day destroying a long streak. Borrowed from Duolingo.
- **Streak milestones**: 7 days, 30 days, 100 days award bonus XP and a badge. 30-day streak unlocks a permanent profile flair.
- **Social pressure**: If a friend also uses the app, show "Jake is on a 23-day streak" — Snapchat-style motivation.

**Streak recovery prompt (push notification):**
"Your 12-day streak expires in 3 hours! Open the app to keep it alive."
- This is the single most effective re-engagement notification in consumer apps.

---

### 10c. Daily & Weekly Challenges

Fresh challenges every day/week give users a reason to return even when they have no positions.

**Daily Challenges (pick 1 of 3):**
```
┌─────────────────────────┐
│ Today's Challenges       │
│                         │
│ ┌─────────────────────┐ │
│ │ 📊 Market Scout      │ │
│ │ View 5 different     │ │
│ │ markets today        │ │
│ │ Reward: 100 XP       │ │
│ │ ░░░░░░░░░░ 0/5       │ │
│ └─────────────────────┘ │
│ ┌─────────────────────┐ │
│ │ 🎯 Quick Trade       │ │
│ │ Open and close a     │ │
│ │ position today       │ │
│ │ Reward: 100 XP       │ │
│ └─────────────────────┘ │
│ ┌─────────────────────┐ │
│ │ 🔍 Set a Price Alert │ │
│ │ Set an alert on any  │ │
│ │ market               │ │
│ │ Reward: 100 XP       │ │
│ └─────────────────────┘ │
│                         │
│ Complete any 1 for      │
│ daily bonus             │
└─────────────────────────┘
```

**Weekly Challenges (bigger scope, bigger reward):**
- "Trade 3 different pairs this week" — 500 XP
- "Maintain your streak all week" — 500 XP
- "Refer a friend who makes their first trade" — 1000 XP
- "Hit a cumulative $1,000 in trading volume" — 500 XP

**Design decisions:**
- **Mix of low-effort and trading challenges** — "View 5 markets" requires no capital. "Open a position" requires engagement. This ensures even zero-balance users have something to do.
- **Challenges rotate** — Keeps it fresh. Never the same set two days in a row.
- **No penalty for skipping** — Challenges are upside-only. Missing them doesn't hurt your streak or level.
- **Progress bars** — Visual completion tracking drives the "just one more" impulse.

---

### 10d. Leaderboards

Competition drives engagement for power users. Leaderboards add a social/competitive layer.

```
Leaderboard Screen
┌─────────────────────────┐
│ Leaderboard    This Week│
│ [P&L %] [Volume] [Streaks]│
│                         │
│ 🥇 @cryptoKing  +142.3% │
│ 🥈 @degenQueen  +98.7%  │
│ 🥉 @tradeBro    +87.1%  │
│  4. @whale99    +72.4%  │
│  5. @moonshot   +65.8%  │
│  ...                    │
│  ─────────────────────  │
│  127. You       +12.3%  │
│  ─────────────────────  │
│                         │
│ Top 10 earn bonus XP    │
│ Top 3 earn fee rebates  │
│                         │
│ Resets every Monday      │
└─────────────────────────┘
```

**Three leaderboard types:**
1. **P&L % (ROI)** — Percentage-based, so small accounts can compete with whales. The great equalizer.
2. **Volume** — For whales who want volume bragging rights.
3. **Streaks** — For consistent users. The longest active streak.

**Design decisions:**
- **Weekly reset** — Fresh start every Monday. Prevents permanent domination by early users.
- **Show the user's rank** pinned at the bottom, even if they're #127. "You're closer than you think" psychology.
- **Top 10 earn bonus XP, Top 3 earn fee rebates** — Real tangible rewards, not just clout.
- **Optional participation** — Users can opt out of being shown on public leaderboards (privacy). They still see their own rank.
- **Anti-gaming**: Leaderboard only counts positions held for 5+ minutes. No wash trading for rank.

---

### 10e. Achievements & Badges

Permanent collectibles that mark milestones. Displayed on profile.

**Example badges:**
| Badge | Requirement |
|---|---|
| First Blood | Close your first trade |
| On Fire | 7-day streak |
| Veteran | 30-day streak |
| Century | 100-day streak |
| Sharp Shooter | 5 profitable trades in a row |
| Whale Watcher | Trade $10,000+ cumulative volume |
| Diversified | Trade 5 different pairs |
| Ambassador | Refer 10 active traders |
| Diamond Hands | Hold a position for 7+ days |
| Speed Demon | Open and close a trade within 60 seconds |
| Early Adopter | Sign up during beta |

- Badges show on the user's profile card (visible when sharing trades).
- Some badges are **secret** (not shown until earned) — drives exploration and surprise.
- Earning a badge triggers a celebratory animation + haptic burst.

---

### 10f. Reward Drops (Mystery Rewards)

Random, delightful rewards that create variable-ratio reinforcement — the most addictive reward schedule in behavioral psychology.

**How it works:**
- After certain actions (closing a profitable trade, maintaining a streak milestone, completing a challenge), there's a **chance** of a reward drop.
- The drop appears as a glowing card that the user taps to reveal:
  ```
  ┌─────────────────────────┐
  │                         │
  │    ✨ Reward Drop! ✨     │
  │                         │
  │   [Tap to reveal]       │
  │                         │
  │    ┌───────────────┐    │
  │    │   ??? ??? ???  │    │
  │    │               │    │
  │    └───────────────┘    │
  │                         │
  └─────────────────────────┘

  → reveals →

  ┌─────────────────────────┐
  │                         │
  │   🎉 You got:           │
  │   Fee-free trade!       │
  │                         │
  │   Your next trade has   │
  │   zero fees.            │
  │                         │
  │   [Nice!]               │
  │                         │
  └─────────────────────────┘
  ```

**Possible rewards:**
- Fee-free next trade
- 2x XP for 24 hours
- Streak freeze (banked for later)
- Bonus XP (50-500)
- Fee rebate on next trade (25-50% off)

**Design decisions:**
- **Variable and unexpected** — Not every action triggers a drop. The randomness is the hook.
- **Always positive** — Drops are upside-only. Never a penalty or "you missed out."
- **Shareable** — "I just got a fee-free trade drop!" adds social spread.
- **Not purchasable** — Can't buy drops with money. Earned through engagement only. This keeps the system feeling fair.

---

## Gamification — Where It Lives in the UI

The gamification system is **woven into the existing UI**, not siloed into its own tab.

| Element | Location |
|---|---|
| Streak counter | Home screen (top), push notifications |
| XP / Level | Profile area, post-trade confirmation |
| Daily challenges | Home screen (below watchlist), dedicated section |
| Leaderboard | Dedicated screen, accessible from home |
| Badges | Profile screen |
| Reward drops | Overlay after qualifying actions |
| Referral XP bonuses | Profile / invite section |

**The home screen evolves to include gamification:**
```
Home Screen (with gamification — V2)
┌─────────────────────────┐
│ ☰  MF Perps     $648.50│
│                         │
│ 🔥 12 day streak  Lv.12 │
│                         │
│ Today's Challenge       │
│ ┌─────────────────────┐ │
│ │ 📊 View 5 markets    │ │
│ │ ████████░░ 4/5       │ │
│ │ Reward: 100 XP       │ │
│ └─────────────────────┘ │
│                         │
│ 🔥 Trending             │
│ PEPE  +47.2%  24h       │
│ SOL   +12.8%  24h       │
│                         │
│ Your Watchlist          │
│ BTC    $67,156      📈  │
│ ETH     $3,842      📉  │
│ + Add market            │
│                         │
│ [Home] [Trade] [Portfolio]│
└─────────────────────────┘
```

---

## V2 Changes to Existing V1 Screens

### Home Screen Additions
- **Streak + Level row** below header: "🔥 12 day streak" (left), "Lv. 12" with mini XP bar (right)
- **Daily Challenge card** below the streak row: single active challenge with progress bar + XP reward. Tappable → Challenges screen.

### Trade Confirmation Addition
- After dismissing the trade confirmation bottom sheet, there's a **30% chance** of showing a Reward Drop overlay. This creates the variable-ratio reinforcement loop.

### Post-Trade XP Notification
- After opening or closing a position, show a subtle "+25 XP" or "+50 XP" toast animation (small, top-right, fades away in 1.5s).

### Referral XP Bonuses (addition to V1 referral system)
- **XP bonus**: Earn bonus XP whenever a referral completes key actions (first deposit, first trade, hits Level 5).
- Referral XP earnings shown in Profile alongside fee earnings.

---

## New Screens

### Leaderboard Screen
Accessible from Home screen or Profile.

```
Layout:
1. Header: "Leaderboard" + "This Week"
2. Tab pills: P&L % | Volume | Streaks
3. Top 3 podium: Gold/silver/bronze icons with username + stat
4. Ranked list: 4th onwards, each row: rank, username, stat
5. Divider
6. Your rank (pinned): "127. You +12.3%"
7. Footer: "Top 10 earn bonus XP. Top 3 earn fee rebates."
```

### Profile Screen
Accessible from hamburger menu or avatar tap.

```
Layout:
1. User info: Avatar (initial-based), display name, level badge
2. Level card: Level 12, XP progress bar, "Next: Unlock 50x leverage"
3. Stats row: Total trades | Win rate | Best trade
4. Streak section: Calendar view of current month with streak dots
5. Badges section: Grid of earned badges (greyed out for unearned)
6. Invite & Earn card: (already in V1, enhanced with XP stats)
   - "3 friends joined"
   - "$12.40 earned from fees"
   - "850 XP earned from referrals"
   - [Share Invite Link] button
   - "Your code: JAKE2026"
7. Settings link
```

### Challenges Screen
Accessible from Home screen challenge card tap.

```
Layout:
1. Header: "Challenges"
2. Daily section: "Today's Challenges" with 3 challenge cards
3. Weekly section: "This Week" with 2-3 larger challenge cards
4. Completed section: Greyed out / checked challenges from today
```

### Reward Drop Overlay
Full-screen overlay with two states: unrevealed and revealed.

```
State 1: Unrevealed
- Glowing/pulsing card in centre
- "✨ Reward Drop!"
- "Tap to reveal"

State 2: Revealed (after tap)
- Card flips/opens with animation
- Shows reward: "Fee-free trade!" or "2x XP for 24 hours" or "150 bonus XP"
- Description of the reward
- [Nice!] button to dismiss
```

---

## V2 Scope

### Must Have
- [ ] XP system + level progression (core loop)
- [ ] Daily login streak tracking + streak counter on home screen
- [ ] Daily challenges (3 per day, rotating)
- [ ] Profile screen with level, stats, streak calendar, badges
- [ ] Achievement badges (first batch: First Blood, On Fire, Veteran, Early Adopter, Sharp Shooter, Diversified)

### Should Have (if time allows)
- [ ] Weekly challenges
- [ ] Leaderboard (P&L % weekly)
- [ ] Reward drops (fee-free trade, XP bonus)
- [ ] Streak freeze mechanic
- [ ] Referral XP bonuses
- [ ] Share card with level/badge display
- [ ] Social streak comparison

### Future / V3
- [ ] Seasonal competitions / limited-time events
- [ ] Leaderboard expansion (volume, streaks)
- [ ] Social feed / copy trading
- [ ] XP marketplace (spend XP on perks)

---

## OpenSpec Prompts

Each prompt below is a self-contained spec for adding gamification features to the existing V1 prototype. They reference `build-v4-gamification.md` for additional components, screens, and mock data. Build in the order listed — earlier prompts create components used by later ones.

---

### Prompt G0: Gamification Components & Data

```
You are extending the MF Perps prototype (V1 already built — see build-v1-mvp.md). Read build-v4-gamification.md for additional components and mock data.

Do the following:

1. Add gamification mock data to src/lib/mock-data.ts:
   - dailyChallenges array (3 items with icon, title, desc, xp, progress, target)
   - weeklyChallenges array (3 items, same shape but bigger targets/rewards)
   - badges array (11 items with id, name, desc, earned boolean)
   - leaderboard array (10 entries with rank, name, pnl)

2. Extend the Zustand store in src/lib/store.ts:
   - Add screens: 'leaderboard' | 'profile' | 'challenges'
   - Add overlay: 'reward-drop'
   - Add user XP/level state if not already present

3. Create src/components/StreakWidget.tsx:
   - Horizontal layout: fire emoji "🔥", streak count "12 day streak" in text-sm font-semibold text-orange, and on the far right "Lv. 12" in text-sm text-accent with a tiny XP bar below it (4px tall, accent color fill, surface bg, rounded-full, 60px wide, 57% filled representing 3450/6000 XP).
   - Wrapped in a Card with reduced padding (py-2 px-4).

4. Create src/components/ChallengeCard.tsx:
   - Takes props: icon (string emoji), title, description, xpReward, progress, target.
   - Card component layout: icon + title on top row, description in text-xs text-secondary below, then a progress bar (h-1.5, rounded-full, accent fill over surface bg) with "4/5" text on the right, and "100 XP" reward badge in text-xs text-accent on the far right.
   - Tappable — whole card navigates to 'challenges' screen.

5. Create src/components/BadgeIcon.tsx:
   - Props: name (string), earned (boolean), icon (emoji string).
   - Size: w-16 h-16, rounded-2xl.
   - Earned: surface-light bg, emoji centred in text-2xl, name below in text-xs text-primary.
   - Unearned: surface bg, opacity-30, emoji centred, name in text-xs text-muted. Locked lock emoji overlay in corner.

6. Create src/components/RewardDrop.tsx (overlay):
   - Full-screen overlay with two states: unrevealed and revealed.
   - See build-v4-gamification.md for full spec.
```

---

### Prompt G1: Home Screen Gamification Layer

```
Read build-v4-gamification.md and plan-v4-gamification.md for full context. You are adding gamification elements to the existing Home screen.

Modify src/screens/05-Home.tsx to add:

1. StreakWidget component between the header row and the first content section.
2. "Today's Challenge" section below the StreakWidget: section header in text-xs uppercase, then a single ChallengeCard showing the first daily challenge from mock data. Tappable → 'challenges' screen.

The rest of the home screen (Trending, Watchlist, Top Movers) stays unchanged.
```

---

### Prompt G2: Profile Screen

```
Read build-v4-gamification.md and plan-v4-gamification.md for full context. You are building the Profile screen.

Create src/screens/14-Profile.tsx:

Layout (scrollable, px-4, pt-4, pb-24):
1. Header: back arrow + "Profile" centred.

2. User card (mt-4): Card with centred layout:
   - Avatar circle: w-16 h-16, rounded-full, accent bg, "J" initial in text-2xl font-bold white, centred.
   - "Jake" name below in text-lg font-semibold.
   - "Level 12" badge below in text-sm text-accent.

3. Level progress card (mt-4): Card with:
   - "Level 12" (left) + "3,450 / 6,000 XP" (right) in text-sm.
   - Progress bar: h-2 rounded-full, accent fill, surface-light bg. 57.5% filled.
   - "Next: Unlock 50x leverage" in text-xs text-secondary, mt-1.

4. Stats row (mt-4): Three stat boxes in a row (flex, gap-3). Each is a small Card:
   - "127" + "Trades" in text-xs text-muted.
   - "64%" + "Win Rate" in text-xs text-muted.
   - "+$340" + "Best Trade" in text-xs text-muted.
   - Number in text-lg font-bold text-primary.

5. Streak section (mt-4): Card with:
   - "🔥 12 day streak" header in text-sm font-semibold.
   - Calendar grid: 7 columns (M T W T F S S labels), 2 rows of dots. Completed days: filled circles in orange. Future/missed: empty circles.
   - "Personal best: 23 days" in text-xs text-muted.

6. Badges section (mt-4):
   - "Badges" header in text-sm font-semibold + "4/11" count in text-xs text-muted.
   - Grid of BadgeIcons (3 columns, gap-3). Badge emoji mapping: First Blood→⚔️, On Fire→🔥, Veteran→🎖️, Century→💯, Sharp Shooter→🎯, Whale Watcher→🐋, Diversified→🎨, Ambassador→👑, Diamond Hands→💎, Speed Demon→⚡, Early Adopter→🌟.

7. Invite & Earn card (mt-4): Card with:
   - "Invite & Earn" header.
   - "3 friends joined · $12.40 earned · 850 XP from referrals" in text-xs text-secondary.
   - Primary Button "Share Invite Link".
   - "Your code: JAKE2026" in text-xs text-muted. Tap to copy.

Bottom nav visible.
```

---

### Prompt G3: Leaderboard Screen

```
Read build-v4-gamification.md and plan-v4-gamification.md for full context. You are building the Leaderboard screen.

Create src/screens/13-Leaderboard.tsx:

Layout (px-4, pt-2, pb-24):
- Header: back arrow + "Leaderboard" centred + "This Week" in text-xs text-secondary on right.
- Tab pills (mt-3): "P&L %", "Volume", "Streaks". Default: "P&L %" active (accent bg).
- Top 3 podium (mt-6): Three cards side by side (middle one slightly larger for #1):
  - #1: gold "🥇", "@cryptoKing", "+142.3%" in green, subtle gold border.
  - #2: silver "🥈", "@degenQueen", "+98.7%".
  - #3: bronze "🥉", "@tradeBro", "+87.1%".
- Ranked list (mt-4): Rows 4-10 from mock data.
- Divider.
- Your rank (pinned): highlighted row "127. You +12.3%".
- Footer: "Top 10 earn bonus XP · Top 3 earn fee rebates" in text-xs text-secondary.

Interactions:
- Tab pills switch views (or show placeholder for Volume/Streaks).
- Podium cards scale up with spring animation on mount.

Bottom nav visible.
```

---

### Prompt G4: Challenges Screen

```
Read build-v4-gamification.md and plan-v4-gamification.md for full context. You are building the Challenges screen.

Create src/screens/15-Challenges.tsx:

Layout (scrollable, px-4, pt-2, pb-24):
- Header: back arrow + "Challenges" centred.
- "Today's Challenges" section (mt-4): 3 ChallengeCards from dailyChallenges mock data.
  - Below: "Complete any 1 for daily bonus" in text-xs text-secondary.
- "This Week" section (mt-6): 3 larger challenge cards from weeklyChallenges:
  1. "🎲 Trade 3 different pairs" — 500 XP — 1/3
  2. "🔥 Maintain your streak all week" — 500 XP — 5/7
  3. "👥 Refer a friend who trades" — 1,000 XP — 0/1
- "Completed Today" section (mt-6): One completed card with opacity-60 and green checkmark.

Cards stagger in on mount.
Bottom nav visible.
```

---

### Prompt G5: Reward Drop Overlay

```
Read build-v4-gamification.md and plan-v4-gamification.md for full context. You are building the Reward Drop overlay.

Create src/screens/17-RewardDrop.tsx (or use src/components/RewardDrop.tsx):

Full-screen overlay, bg-black/70 with backdrop-blur-sm.

**State 1: Unrevealed**
- Card (w-64 h-80, rounded-3xl, surface bg) with:
  - Pulsing glow border (Framer Motion animated box-shadow in accent color)
  - "✨ Reward Drop! ✨" in text-xl font-bold
  - Three "? ? ?" in text-4xl text-muted, subtly floating (y oscillating ±5px)
  - "Tap to reveal" in text-sm text-secondary
  - Card pulses (scale 1→1.02→1, infinite, 2s)

**State 2: Revealed (after tap)**
- Card flips (rotateY animation) or scales down→up with new content:
  - "🎉" in text-4xl
  - "You got:" in text-sm text-secondary
  - Reward name in text-2xl font-bold text-accent (randomly selected from: "Fee-free trade!", "2x XP for 24 hours", "150 Bonus XP", "Streak Freeze")
  - Description in text-sm text-secondary
  - "Nice!" Primary Button at bottom

Interactions:
- Tap unrevealed card → flip to revealed.
- "Nice!" → dismiss overlay.
- Optional: confetti particles on reveal.

Wire this into the trade confirmation flow: after dismissing TradeConfirmation, 30% chance of showing reward-drop overlay.
```

---

### Prompt G6: Trade Confirmation XP & Reward Drop Integration

```
Read build-v4-gamification.md for context. Modify the existing trade confirmation bottom sheet (src/screens/09-TradeConfirmation.tsx) to:

1. Add an XP earned line below the summary: "+25 XP earned" in text-sm text-accent with a small sparkle icon.

2. After the user taps "View Position" or "Trade Again" and the sheet dismisses, implement a 30% chance of showing the 'reward-drop' overlay. Use setTimeout(500ms) after dismissal to show it.

This creates the variable-ratio reinforcement that keeps users engaged.
```

---

### Prompt G7: Share Card V2 Enhancement

```
Read build-v4-gamification.md for context. If the Share Card overlay (src/screens/13-ShareCard.tsx or 16-ShareCard.tsx) was built in V1, enhance it to include:

1. User info row: avatar circle + "Jake" + "Level 12" badge + "🔥 12" streak count.
2. Display 1-2 earned badge icons next to the user info.

These additions make shared cards more aspirational and showcase the gamification system to potential new users.
```

---

### Prompt G8: Gamification Polish

```
Read build-v4-gamification.md for context. Final polish for gamification features:

1. **XP toast animation**: Create a small floating "+25 XP" or "+50 XP" toast that appears in the top-right of the screen after XP-earning actions. Animate: fade in, float up 20px, fade out over 1.5s. Accent color text.

2. **Badge earned celebration**: When navigating to Profile and a new badge is earned (mock this), show a brief full-screen overlay: badge icon scales up with spring animation, confetti burst, "Achievement Unlocked! 🎯 Sharp Shooter" text. Auto-dismisses after 2s or on tap.

3. **Level up animation**: When XP crosses a level threshold (mock this as a button in Profile for demo), show: level number counting up, "Level Up!" text, perk unlocked text. Confetti/particles.

4. **Screen transitions for new screens**: 
   - Profile: slide up from bottom.
   - Leaderboard: slide up from bottom.
   - Challenges: slide up from bottom.
   - Reward Drop overlay: already has its own animation.

5. **Home screen gamification polish**: Streak counter should have a subtle fire glow animation. Challenge progress bar should animate on mount (0% → current value over 500ms).
```
