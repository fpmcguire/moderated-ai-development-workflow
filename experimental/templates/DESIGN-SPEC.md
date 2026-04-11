# Design Spec — {{PROJECT_NAME}}

**Product:** {{PROJECT_NAME}}
**Date:** {{DATE}}
**Designer:** {{DESIGNER_NAME}}
**Status:** Draft · In Review · Approved

---

## 1. Visual Identity

### 1.1 Color Palette

| Token                  | Hex       | Usage                                      |
| ---------------------- | --------- | ------------------------------------------ |
| `color-primary`        | `#______` | Primary actions, active state, focus rings |
| `color-primary-hover`  | `#______` | Primary button hover                       |
| `color-primary-subtle` | `#______` | Active item background, selected highlight |
| `color-secondary`      | `#______` | Secondary actions                          |
| `color-surface`        | `#______` | Page / app background                      |
| `color-surface-raised` | `#______` | Cards, panels, sidebars                    |
| `color-border`         | `#______` | Dividers, input borders                    |
| `color-border-subtle`  | `#______` | Subtle separators                          |
| `color-text-primary`   | `#______` | Body text, headings                        |
| `color-text-secondary` | `#______` | Labels, captions, placeholders             |
| `color-text-disabled`  | `#______` | Disabled controls                          |
| `color-error`          | `#______` | Validation errors, destructive states      |
| `color-error-subtle`   | `#______` | Error message backgrounds                  |
| `color-success`        | `#______` | Confirmation, positive feedback            |
| `color-warning`        | `#______` | Non-blocking warnings                      |

> Notes: <!-- Any color usage rules, brand constraints, or dark mode considerations -->

### 1.2 Typography

**Font families:**

| Role                   | Family   | Fallback                |
| ---------------------- | -------- | ----------------------- |
| Base / body            | `______` | `system-ui, sans-serif` |
| Monospace (code, JSON) | `______` | `monospace`             |

**Type scale:**

| Token             | Size    | Line height | Weight | Usage                         |
| ----------------- | ------- | ----------- | ------ | ----------------------------- |
| `text-heading-lg` | `__rem` | `__`        | `__`   | Page titles, modal headings   |
| `text-heading-md` | `__rem` | `__`        | `__`   | Section headings              |
| `text-heading-sm` | `__rem` | `__`        | `__`   | Card titles, sidebar headings |
| `text-body`       | `__rem` | `__`        | `__`   | Default body copy             |
| `text-label`      | `__rem` | `__`        | `__`   | Form labels, column headers   |
| `text-caption`    | `__rem` | `__`        | `__`   | Helper text, timestamps       |
| `text-overline`   | `__rem` | `__`        | `__`   | Section labels, category tags |

### 1.3 Spacing & Layout System

**Base unit:** `__px` (e.g. 4px or 8px)

| Token     | Value  | Usage                          |
| --------- | ------ | ------------------------------ |
| `space-1` | `__px` | Tight inner padding, icon gaps |
| `space-2` | `__px` | Default inner padding          |
| `space-3` | `__px` | Component gaps                 |
| `space-4` | `__px` | Section gaps                   |
| `space-6` | `__px` | Panel / page padding           |
| `space-8` | `__px` | Large section separation       |

**Layout approach:**

<!-- Describe the primary layout strategy: sidebar + main, single column, grid, etc.
     Note any fixed widths, max-widths, or flex/grid conventions. -->

### 1.4 Borders, Radius & Elevation

| Token            | Value                    | Usage                        |
| ---------------- | ------------------------ | ---------------------------- |
| `radius-sm`      | `__px`                   | Badges, tags, small controls |
| `radius-md`      | `__px`                   | Buttons, inputs, cards       |
| `radius-lg`      | `__px`                   | Modals, panels               |
| `radius-full`    | `9999px`                 | Pills, avatars               |
| `border-default` | `1px solid color-border` | Component outlines           |
| `shadow-sm`      | `__`                     | Raised cards, dropdowns      |
| `shadow-md`      | `__`                     | Modals, overlays             |

### 1.5 Tone & Personality

<!-- 3–5 words or phrases that describe the intended visual feeling.
     Examples: "clean, low-noise, professional", "friendly, approachable, modern"
     Briefly explain how each word should manifest in the UI. -->

**Words:** **\_\_**, **\_\_**, **\_\_**

| Word     | What it means in the UI |
| -------- | ----------------------- |
| `______` |                         |
| `______` |                         |
| `______` |                         |

---

## 2. Accessibility Baseline

| Concern                                     | Requirement                                                                    |
| ------------------------------------------- | ------------------------------------------------------------------------------ |
| Color contrast — body text                  | WCAG AA (4.5 : 1 minimum)                                                      |
| Color contrast — large text / UI components | WCAG AA (3 : 1 minimum)                                                        |
| Focus indicators                            | Visible on all interactive elements; `outline` or `ring` using `color-primary` |
| Keyboard navigation                         | All interactive elements reachable and operable by keyboard                    |
| Touch targets                               | Minimum `44 × 44px` for interactive controls on touch devices                  |
| ARIA labels                                 | Applied where interactive element text alone is insufficient                   |
| Reduced motion                              | Respect `prefers-reduced-motion`; disable or reduce transitions                |

> Notes: <!-- Any additional a11y constraints or known gaps to resolve -->

---

## 3. Component Library

<!-- One sub-section per component. Copy the template block below for each component.
     Use names exactly as they appear in the Domain Language Matrix. -->

---

### 3.x {{ComponentName}}

**Purpose:** <!-- One sentence describing what this component does. -->

**States:**

| State             | Description |
| ----------------- | ----------- |
| Default           |             |
| Hover             |             |
| Focus             |             |
| Active / Selected |             |
| Disabled          |             |
| Loading           |             |
| Empty             |             |
| Error             |             |

**Variants:**

| Variant | Description |
| ------- | ----------- |
|         |             |

**`data-testid` conventions:**

| Element | `data-testid` |
| ------- | ------------- |
|         |               |

**Layout / structure notes:**

<!-- Prose or ASCII diagram describing the internal layout of the component if non-trivial. -->

**Do / Don't:**

<!-- Optional: one or two critical usage rules for developers. -->

---

## 4. Screen Layouts

<!-- One sub-section per screen or major UI region. -->

---

### 4.x {{ScreenName}}

**Description:** <!-- What is this screen for? When does the user see it? -->

**Layout structure:**

<!-- Describe the layout: e.g. "Fixed header + sidebar (240px) + main content area (flex 1)".
     Include an ASCII diagram if helpful. -->

```
┌─────────────────────────────────────────────┐
│  Header                                     │
├───────────────┬─────────────────────────────┤
│               │                             │
│  Sidebar      │  Main Content               │
│               │                             │
└───────────────┴─────────────────────────────┘
```

**Components present:**

| Component | Position | Notes |
| --------- | -------- | ----- |
|           |          |       |

**States:**

| State            | Trigger | What the user sees |
| ---------------- | ------- | ------------------ |
| Default / loaded |         |                    |
| Empty            |         |                    |
| Loading          |         |                    |
| Error            |         |                    |

**Responsive behaviour:**

<!-- Describe breakpoint behaviour if in scope, or note "not in scope for this Step". -->

---

## 5. Interaction Patterns

### 5.1 Selection

<!-- How does the user select an item? Click, keyboard, toggle?
     What visual change indicates selection? How is deselection handled? -->

### 5.2 Hover & Focus

<!-- Describe hover treatment for interactive elements.
     Describe focus ring style and when it appears (keyboard-only vs always). -->

### 5.3 Keyboard Navigation

| Key        | Behaviour |
| ---------- | --------- |
| `Tab`      |           |
| `Enter`    |           |
| `Space`    |           |
| `Escape`   |           |
| Arrow keys |           |

### 5.4 Transitions & Animation

<!-- Describe any transitions (duration, easing) or note "no transitions in scope".
     Note reduced-motion fallback. -->

---

## 6. Component–Roadmap Map

| Component / Screen | First introduced | Step scope note |
| ------------------ | ---------------- | --------------- |
|                    |                  |                 |

> Components or states marked _(Step N+)_ should not be implemented until that Step is in scope.
> The Development Team must not build ahead of the current Step boundary.

---

## 7. Open Questions & Deferred Decisions

<!-- List anything that needs Product Owner, Tech Lead, or Moderator input before
     implementation can proceed. Be specific about what is blocked and why. -->

| #   | Question | Owner | Status |
| --- | -------- | ----- | ------ |
| 1   |          |       | Open   |
| 2   |          |       | Open   |

---

MOD-W v2.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
