## ADDED Requirements

### Requirement: Color tokens are defined as JS constants
The system SHALL export a `colors` object from `src/lib/tokens.ts` containing all brand colors: background (`#0A0A0F`), surface (`#14141F`), surface-light (`#1E1E2E`), border (`#2A2A3A`), text-primary (`#FFFFFF`), text-secondary (`#8888AA`), text-muted (`#555577`), accent (`#7B61FF`), green (`#00D68F`), red (`#FF4757`), yellow (`#FFD93D`), orange (`#FF9F43`).

#### Scenario: Import color tokens in a component
- **WHEN** a component imports `colors` from `src/lib/tokens`
- **THEN** all 12 color values are available as string hex codes

### Requirement: Typography tokens are defined as JS constants
The system SHALL export a `typography` object from `src/lib/tokens.ts` with font-family set to `"Inter"` with `system-ui` fallback, and size presets: large-number (`text-3xl font-bold tabular-nums`), section-head (`text-lg font-semibold`), body (`text-sm`), caption (`text-xs`).

#### Scenario: Import typography tokens
- **WHEN** a component imports `typography` from `src/lib/tokens`
- **THEN** font family and size presets are accessible

### Requirement: Spacing and radius tokens are defined as JS constants
The system SHALL export `spacing` and `radius` objects from `src/lib/tokens.ts`. Spacing: card-padding (`p-4`), screen-padding (`px-4 py-6`), card-gap (`gap-3`). Radius: buttons (`rounded-xl`), cards (`rounded-2xl`), inputs (`rounded-xl`), full-round (`rounded-full`).

#### Scenario: Import spacing and radius tokens
- **WHEN** a component imports `spacing` and `radius` from `src/lib/tokens`
- **THEN** padding, gap, and border-radius values are accessible

### Requirement: Tailwind theme extends with custom colors
The Tailwind configuration SHALL extend the theme with custom color names matching the token names (background, surface, surface-light, border, text-primary, text-secondary, text-muted, accent, green, red, yellow, orange) so that utility classes like `bg-surface`, `text-accent`, `border-border` work.

#### Scenario: Use custom Tailwind color class
- **WHEN** a component uses the class `bg-surface`
- **THEN** the element background is `#14141F`

#### Scenario: Use custom text color class
- **WHEN** a component uses the class `text-accent`
- **THEN** the text color is `#7B61FF`
