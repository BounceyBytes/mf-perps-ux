## ADDED Requirements

### Requirement: AnimatedNumber counts from 0 to target on mount
The AnimatedNumber component SHALL accept a `value` prop (number) and animate from 0 to that value on mount over approximately 500ms using Framer Motion useSpring or useMotionValue. The animation SHALL use a natural deceleration curve.

#### Scenario: Dollar amount animates on mount
- **WHEN** AnimatedNumber renders with value={1234.56}
- **THEN** the displayed number counts up from 0 to 1234.56 over ~500ms

#### Scenario: Percentage animates on mount
- **WHEN** AnimatedNumber renders with value={12.5} and a "%" suffix
- **THEN** the displayed number counts up from 0 to 12.5 over ~500ms followed by "%"

### Requirement: AnimatedNumber renders with tabular-nums font variant
The AnimatedNumber component SHALL apply `font-variant-numeric: tabular-nums` (Tailwind class `tabular-nums`) to prevent layout shift as digits change during the animation.

#### Scenario: Digits do not cause layout shift
- **WHEN** the number is animating from 0 to 999.99
- **THEN** the text uses tabular-nums so each digit occupies equal width and the element does not shift horizontally

### Requirement: AnimatedNumber supports prefix and suffix
The AnimatedNumber component SHALL accept optional `prefix` (e.g., "$") and `suffix` (e.g., "%") string props. The prefix renders before the animated number, the suffix renders after.

#### Scenario: Dollar prefix renders
- **WHEN** AnimatedNumber renders with prefix="$" and value={500}
- **THEN** the output reads "$500" after animation completes

### Requirement: AnimatedNumber formats with appropriate decimal places
The AnimatedNumber component SHALL accept an optional `decimals` prop (default 2) to control the number of decimal places rendered.

#### Scenario: Two decimal places for dollar amounts
- **WHEN** AnimatedNumber renders with value={100} and decimals={2}
- **THEN** the final displayed value is "100.00"

#### Scenario: One decimal place for percentages
- **WHEN** AnimatedNumber renders with value={12.5} and decimals={1}
- **THEN** the final displayed value is "12.5"
