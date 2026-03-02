## ADDED Requirements

### Requirement: All buttons apply whileTap scale 0.97
The Button component SHALL include Framer Motion `whileTap={{ scale: 0.97 }}` so that every button in the app compresses slightly on press.

#### Scenario: User presses any button
- **WHEN** the user taps and holds any Button
- **THEN** the button scales to 0.97 while pressed and returns to 1.0 on release

### Requirement: Primary variant has hover brightness increase
The Button component with variant="primary" SHALL apply a slight brightness increase on hover (e.g., `whileHover={{ brightness: 1.1 }}` or a CSS hover brightness filter).

#### Scenario: User hovers over primary button
- **WHEN** the user hovers over a primary (accent) button
- **THEN** the button background brightness increases slightly

#### Scenario: Non-primary buttons do not change brightness on hover
- **WHEN** the user hovers over a secondary or ghost button
- **THEN** no brightness change occurs on hover

### Requirement: Button renders as Framer Motion motion.button
The Button component SHALL render as a `motion.button` element (from Framer Motion) to enable the whileTap and whileHover props natively.

#### Scenario: Button is a motion element
- **WHEN** the Button component renders
- **THEN** the underlying DOM element is a motion.button with Framer Motion animation capabilities
