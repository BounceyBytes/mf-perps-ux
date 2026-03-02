## 1. Project Initialization

- [ ] 1.1 Run `npx create-next-app@latest mf-perps-prototype --typescript --tailwind --app --src-dir --no-eslint`
- [ ] 1.2 Install dependencies: `npm install framer-motion lucide-react zustand`
- [ ] 1.3 Verify project runs with `npm run dev`

## 2. Design Tokens

- [ ] 2.1 Create `src/lib/tokens.ts` exporting `colors`, `typography`, `spacing`, and `radius` objects with all values from the build guide
- [ ] 2.2 Extend Tailwind config to add custom color names (background, surface, surface-light, border, text-primary, text-secondary, text-muted, accent, green, red, yellow, orange) using values from tokens

## 3. Global Styles

- [ ] 3.1 Configure `src/app/globals.css` with Tailwind imports, Inter Google Font import, dark background/text defaults on html/body, and hidden scrollbar styles
- [ ] 3.2 Update `src/app/layout.tsx` to apply Inter font and dark background as the root layout

## 4. Verification

- [ ] 4.1 Confirm `npm run dev` starts successfully with dark background and Inter font visible in browser
