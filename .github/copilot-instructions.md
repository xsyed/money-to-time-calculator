## Money → Time Calculator — Copilot instructions

This repository is a tiny, client-side web app that converts a purchase amount into equivalent working time based on a user-provided annual gross income. The app is implemented with vanilla HTML/CSS/JS and stores the annual income in localStorage.

Quick facts
- Language: plain HTML, CSS and vanilla JavaScript (no build step).
- Entry point: `index.html` (loads `src/script.js` and `src/styles.css`).
- Dev server: `npm start` runs `npx serve -s . -l 5000` (see `package.json`).

What to know before editing
- All logic lives in `src/script.js`. Changes to behavior (calculation rules, formatting, storage key) should be made there.
- UI structure and IDs in `index.html` are used directly by `script.js` (for example `#annual-display`, `#edit-income`, `#purchase-input`, `#result`). When changing markup, update the JS selectors accordingly.
- Styling conventions live in `src/styles.css` and use CSS variables (see `:root`). Prefer small, non-breaking visual tweaks.
 - The app now supports light/dark themes. Styling uses CSS variables and `prefers-color-scheme`; JS exposes a header theme toggle wired to `#theme-toggle` and stores user preference under `localStorage` key `mtt_theme_pref` (values: `"light"`, `"dark"`, or omitted to follow OS`).

Project-specific patterns and examples
- Persisted state: the annual income is stored under localStorage key `mtt_annual_income`. Use `loadAnnual()` / `saveAnnual()` in `src/script.js` when interacting with this value.
- Pay-rate calculation: `calcRates(annual)` derives `monthly`, `biweekly`, and `hourly` (hourly = annual / (52 * 40)). If you change the working-hours assumptions, update this function and the PRD in `instructions.md`.
- Result formatting: `formatWorkTime(hours)` chooses the most meaningful unit using thresholds (<=8h → h/m/s, <=5 days → days + hours, <=4 weeks → weeks + days, <=12 months → months + weeks, else years + months). Tests or UI changes should respect these thresholds.
- Accessibility: the income form toggles `aria-hidden` and focus is managed (`annualInput.focus()`). Preserve these behaviors when refactoring.

Developer workflows
- Run locally: `npm start` then open http://localhost:5000 or the printed address. There is no build step — edits to files are reflected on refresh.
- Quick smoke test: set an annual income, enter a purchase amount, click Calculate, and verify the output text in `#result`.
 - Theme smoke test: verify the app follows your OS theme on first load. Use the header theme toggle to set Light, Dark, or clear preference (follow OS). Check `localStorage` for `mtt_theme_pref` to ensure persistence.

Helpful editing rules for AI agents
- Keep changes minimal and isolated. This is a small, single-page app: prefer editing `src/script.js` and `src/styles.css` over adding complex new frameworks.
- When renaming DOM IDs or adding elements, update `src/script.js` selectors and any references in `index.html` and `instructions.md`.
- Preserve localStorage key `mtt_annual_income` unless performing a deliberate migration; if changing the key, implement a safe migration path (read old key, write new key) and document it in the repo.
- Use existing helper functions (`moneyFmt`, `calcRates`, `formatWorkTime`, `loadAnnual`, `saveAnnual`) rather than duplicating logic.
 - New theme helpers exist in `src/script.js` (loadThemePref/saveThemePref/applyTheme). Prefer using them when changing theme behavior.

Examples to reference
- Changing hourly rate logic: edit `calcRates` in `src/script.js`.
- Changing display thresholds: edit `formatWorkTime` in `src/script.js`.
- Toggling the income editor: see `showIncomeForm(show)` and its callers `#edit-income` and `#cancel-income` handlers.

Tests, linting, and CI
- There are no tests or CI configs. Keep changes small and add simple unit tests if expanding logic significantly. For JS logic, prefer small node test scripts or a single Jest setup.

When in doubt
- If a change touches storage, UI, and formatting, include a short note in the PR describing manual steps to verify (e.g., "Set income to 60000, calculate for 19.99 → expected ~1h").
