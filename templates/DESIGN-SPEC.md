# Design Spec — {{PROJECT_NAME}}

**Date:** {{DATE}}
**Designer:** {{DESIGNER_NAME}}
**Authored in:** {{CLAUDE_DESIGN | CLAUDE_CHATBOT | GEMINI}}
**Prototype:** {{PROTOTYPE_PATH or "n/a"}}

---

## Design Principles

- Clear
- Consistent
- Minimal
- Accessible

---

## 1. Visual Identity

### 1.1 Color Palette

### 1.2 Typography

### 1.3 Spacing & Layout System

### 1.4 Borders, Radius & Elevation

### 1.5 Tone & Personality

---

## 2. Accessibility Baseline

- WCAG AA compliance
- Keyboard navigation required
- Visible focus states

---

## 3. Component Library

> One section per component. For each component document: name (from `DOMAIN_LANGUAGE.md`), one-sentence purpose, states (default / hover / active / disabled / loading / empty / error), variants, and `data-testid` convention.

### 3.x {{COMPONENT_NAME}}

- **Purpose:**
- **States:**
- **Variants:**
- **data-testid:** `{{feature}}-{{component}}-{{element}}-{{modifier?}}`

---

## 4. Screen Layouts

> One section per screen. Document layout structure, components present and their positions, empty / loading / error states, and responsive behaviour (if in scope).

### 4.x {{SCREEN_NAME}}

---

## 5. Interaction Patterns

- Selection / hover / focus
- Keyboard navigation
- Transitions

---

## 6. Component–Step Mapping

| Component | First Step | Notes |
| --------- | ---------- | ----- |
|           | STEP-01    |       |

---

## 7. Domain Language Proposals  *(v4)*

> Terms the prototype surfaced that are NOT in `DOMAIN_LANGUAGE.md`. Each entry is a proposal for the Tech Lead to ratify, modify, or reject during Architecture Definition. Do not treat any term here as canonical.

| Proposed term | Form (type / value / both) | Definition | Rationale | First appearance |
| ------------- | -------------------------- | ---------- | --------- | ---------------- |
|               |                            |            |           |                  |

If no terms proposed, state "None proposed."

---

## 8. Scope Rules

- Only define components required for current or near-term Steps
- Do not design beyond ROADMAP scope
- Each component must map to a Step

---

## 9. UI Scope Rules

- Only implement UI elements in current `STEP-XX.md`
- Future states must not be implemented early
- Design supports incremental delivery

---

## 10. Open Questions

| Question | Owner | Status |
| -------- | ----- | ------ |

---

MOD-W v4.0.0
