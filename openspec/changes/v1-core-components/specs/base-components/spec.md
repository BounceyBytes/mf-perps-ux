## ADDED Requirements

### Requirement: Button supports three variants
The Button component SHALL accept a `variant` prop with values: `primary` (accent bg `#7B61FF`, white text), `secondary` (surface-light bg `#1E1E2E`, white text), `ghost` (transparent bg, border `#2A2A3A`, white text). All variants SHALL use rounded-xl, font-semibold, full-width by default.

#### Scenario: Render primary button
- **WHEN** a Button with variant="primary" renders
- **THEN** it displays with accent purple background and white text

#### Scenario: Render ghost button
- **WHEN** a Button with variant="ghost" renders
- **THEN** it displays with transparent background and a subtle border

### Requirement: Button has press animation
All Button variants SHALL use Framer Motion `whileTap={{ scale: 0.97 }}` for press feedback.

#### Scenario: User taps a button
- **WHEN** user presses down on any Button
- **THEN** the button scales to 97% and returns to 100% on release

### Requirement: Card renders a surface container
The Card component SHALL render a div with surface bg (`#14141F`), rounded-2xl, p-4, and a subtle border (`#2A2A3A`).

#### Scenario: Card renders with correct styling
- **WHEN** a Card component renders with children
- **THEN** children appear inside a rounded dark container with padding

### Requirement: Input renders a dark-themed text field
The Input component SHALL render with surface-light bg (`#1E1E2E`), rounded-xl, text-primary color, placeholder in text-muted, and accent-color focus ring.

#### Scenario: Input has accent focus ring
- **WHEN** user focuses the Input field
- **THEN** a ring in accent color (`#7B61FF`) appears around the input
