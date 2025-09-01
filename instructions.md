# PRD – Money to Time Calculator

## 1. Project Overview

The **Money to Time Calculator** is a web-based tool that helps users understand the real-time cost of their purchases in terms of hours, minutes, days, weeks, months, or years of their working time.

Users will input their **annual gross income** (stored in browser localStorage) and a **purchase amount**. The app will then calculate how much working time (down to seconds) that purchase represents, based on the user’s income.

The calculator is designed to be **simple, mobile-first, responsive, and user-friendly** with a clean UI.

---

## 2. Objectives

* Allow users to input and save their annual gross income.
* Calculate derived pay rates (monthly, biweekly, hourly).
* Convert purchase cost into equivalent work time.
* Display results in an intuitive format (hours/minutes/days/weeks/months/years).
* Make the income editable anytime with recalculations reflecting instantly.
* Provide a **minimalistic, mobile-first UI** with a clean design.
* Support system color scheme with an auto light/dark theme and a user toggle to override it.

---

## 3. Target Users

* Anyone interested in budgeting and financial awareness.
* People who want to better visualize their spending in terms of their work time.

---

## 4. Features & Requirements

### 4.1 Core Features

1. **Annual Income Input**

   * User can enter annual gross income.
   * Stored in **localStorage**.
   * Display the currently saved annual income in the UI.
   * User can update this anytime.

2. **Derived Pay Rates**

   * Based on the annual income, calculate:

     * Monthly income = Annual ÷ 12
     * Biweekly income = Annual ÷ 26
     * Hourly income = Annual ÷ (52 × 40) *(assuming 40-hour work week)*

3. **Purchase Input & Calculation**

   * User enters purchase amount.
   * System calculates equivalent work time:

     * Total Hours = Purchase ÷ Hourly rate
     * Convert to minutes/seconds for finer breakdown

4. **Result Display Logic**

   * If ≤ 8 hours → show hours/minutes/seconds.
   * If > 8 hours → convert into days (8 hours = 1 day).
   * If > 5 days → convert into weeks.
   * If > 4 weeks → convert into months.
   * If > 12 months → convert into years.

5. **Editable Income**

   * Annual income should be displayed in UI with an “Edit” option.
   * On update, recalculations should reflect instantly.

---

### 4.2 UI/UX Requirements

* **Clean and minimal design** with primary focus on usability.
* **Mobile-first responsive layout**.
* Use the given **color scheme** consistently:

  * Primary Green: `#1C973D`
  * Accent Blue: `#33AFC5`
  * Accent Pink/Red: `#C82057`
  * White: `#FFFFFF`
* The app now supports light and dark themes. By default the app follows the device OS preference (`prefers-color-scheme`). Users may toggle between light, dark, and "follow OS" using the theme button in the header.
* Clear typography, large input fields, and easy-to-read results.

---

### 4.3 Technical Requirements

* Technologies: **HTML, CSS, Vanilla JS**.
* Storage: **localStorage** for persisting annual income.
* Theme preference is stored in localStorage under key `mtt_theme_pref`. Possible values: `"light"`, `"dark"`, or omitted (null) to follow OS preference.
* No backend required (fully client-side).
* Should work offline once loaded.

---

### 4.4 Non-Functional Requirements

* Performance: Calculation must be instant (<100ms).
* Accessibility: High contrast and readable font sizes.
* Simplicity: No unnecessary UI clutter.

---

## 5. User Flow

1. **First Visit**

   * User prompted to enter **annual income**.
   * Value saved in localStorage.

2. **Returning Visit**

   * Saved income auto-populates.
   * User can edit/update anytime.

3. **Entering Purchase**

   * User enters purchase amount.
   * App calculates equivalent work time.
   * Result displayed in most meaningful unit (hours, days, weeks, months, years).

4. **Editing Income**

   * User edits annual income.
   * Stored value updates in localStorage.
   * All future calculations reflect updated income.

   5. **Theme behavior**

       * On first load the app follows the device color scheme via the CSS `prefers-color-scheme` media query.
       * The header includes a theme toggle. Clicking it cycles between:
          1. Explicit Dark
          2. Explicit Light
          3. Follow OS (clears user preference)
       * When a user selects Dark or Light, the choice is saved to `localStorage` under `mtt_theme_pref` and will persist across visits.

   ---

   ### Manual verification / smoke test for theme

   1. Open the app on a device or browser. If your OS is in dark mode the UI should appear dark by default; otherwise light.
   2. Click the header theme toggle button. The app should switch to the chosen theme and persist on refresh.
   3. Clear `mtt_theme_pref` from localStorage (or use the toggle until it returns to "follow OS"). Changing the OS-level theme should update the app automatically.

---

## 6. Deliverables

* Responsive, mobile-first web app.
* Functional income input with persistence.
* Purchase-to-time calculator with conversion rules.
* Clean UI styled with provided color scheme.

---

## 7. Future Enhancements (not in MVP)

* Option to set different working hours per week (customizable instead of fixed 40).
* Multiple saved profiles for different income scenarios.
* Graphical visualization of “time cost” (progress bar or clock animation).
* Export/share results.
