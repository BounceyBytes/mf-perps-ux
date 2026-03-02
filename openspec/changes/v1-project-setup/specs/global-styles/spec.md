## ADDED Requirements

### Requirement: Tailwind CSS is imported globally
The `globals.css` file SHALL import Tailwind CSS base, components, and utilities layers.

#### Scenario: Tailwind utilities available
- **WHEN** any component uses a Tailwind utility class (e.g., `p-4`, `text-sm`)
- **THEN** the utility styles are applied correctly

### Requirement: Inter font is loaded globally
The `globals.css` file SHALL import the Inter font from Google Fonts and set it as the default font-family on `html` and `body`.

#### Scenario: Page renders with Inter font
- **WHEN** the app loads in a browser
- **THEN** all text uses the Inter font family (with system-ui fallback)

### Requirement: Dark background is applied globally
The `globals.css` file SHALL set `html` and `body` background to `#0A0A0F` and text color to `#FFFFFF` (text-primary).

#### Scenario: Page has dark background
- **WHEN** the app loads
- **THEN** the page background is near-black (`#0A0A0F`) and default text is white

### Requirement: Scrollbar is hidden
The `globals.css` file SHALL hide the scrollbar for the phone frame content area using webkit and standard scrollbar-width CSS properties.

#### Scenario: No visible scrollbar in phone frame
- **WHEN** content inside the phone frame overflows
- **THEN** the user can scroll but no scrollbar is visible
