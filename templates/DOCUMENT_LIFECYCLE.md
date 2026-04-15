# Document Lifecycle

**Project:** {{PROJECT_NAME}}
**Owner:** Moderator
**Version:** MOD-W v2.1.0

---

## Purpose

This document defines:

- ownership of each MOD-W document
- when it is created
- when it is updated
- how it flows through the workflow

It ensures:

- consistency across agents
- traceability (R-ID / D-ID)
- controlled evolution over time

---

## Core Principle

> Documents are not static — they evolve in controlled stages.

All changes must flow **forward**:

```text
PRODUCT → ARCHITECTURE → ROADMAP → STEP → REVIEW / QA → CODE
```

No document should be updated out of order without Moderator approval.

---

## Document Ownership Matrix

| Document           | Owner          | Role Responsibility   |
| ------------------ | -------------- | --------------------- |
| PRODUCT.md         | Product Owner  | Define intent (R-IDs) |
| ARCHITECTURE.md    | Tech Lead      | Define design (D-IDs) |
| ROADMAP.md         | Tech Lead      | Define execution plan |
| STEP-XX.md         | Tech Lead      | Define scoped work    |
| REVIEW.md          | Moderator      | Accept / reject       |
| QA.md              | QA / Moderator | Validate behavior     |
| DOMAIN_LANGUAGE.md | Tech Lead      | Define terminology    |
| DESIGN-SPEC.md     | Designer / PO  | Define UI/UX          |
| AI_AGENTS.md       | Tech Lead      | Define agent setup    |

---

## Lifecycle by Phase

---

### 🟢 Phase 1 — Product Definition

**Primary document:** `PRODUCT.md`

**Owner:** Product Owner (ChatGPT + Perplexity)

#### Actions:

- Define problem, users, goals
- Create requirements with R-IDs
- Define scenarios and risks

#### Output:

- Approved PRODUCT.md

#### Triggers:

- New feature request
- Marketing change
- Scope change

---

### 🟡 Phase 2 — Architecture

**Primary document:** `ARCHITECTURE.md`

**Owner:** Tech Lead (Codex)

#### Actions:

- Define system structure
- Create D-IDs
- Map R-IDs → D-IDs

#### Output:

- Approved architecture decisions

#### Rules:

- Do not rewrite — append decisions
- Mark deprecated decisions instead of deleting

---

### 🔵 Phase 3 — Planning

**Primary document:** `ROADMAP.md`

**Owner:** Tech Lead

#### Actions:

- Break work into STEP-XX units
- Map each step to R-IDs
- Ensure steps are small and verifiable

#### Output:

- Ordered step plan

---

### 🟣 Phase 4 — Step Definition

**Primary document:** `STEP-XX.md`

**Owner:** Tech Lead

#### Actions:

- Define scope
- Define acceptance checks
- Define expected file changes
- Reference R-IDs

#### Rules:

- Must be implementable in one iteration
- Must define clear boundaries

---

### 🔴 Phase 5 — Implementation

**Primary actor:** Development Team (Claude Code)

#### Inputs:

- STEP-XX.md
- Relevant PRODUCT / ARCHITECTURE excerpts

#### Actions:

- Restate Step
- Propose plan
- Wait for approval
- Implement

#### Output:

- Code + summary

---

### ⚫ Phase 6 — Review

**Primary document:** `REVIEW.md`

**Owner:** Moderator

#### Actions:

- Validate against STEP scope
- Validate R-ID coverage
- Evaluate quality

#### Outcomes:

- Accept
- Request Revisions
- Reject

---

### ⚪ Phase 7 — QA

**Primary document:** `QA.md`

**Owner:** QA / Moderator

#### Actions:

- Execute test cases
- Validate behavior
- Check regressions

#### Output:

- Pass / Fail decision

---

## Supporting Documents Lifecycle

---

### DOMAIN_LANGUAGE.md

**Owner:** Tech Lead

#### Update when:

- New concept introduced
- Naming inconsistency found

#### Enforced by:

- Development Team
- Review process

---

### DESIGN-SPEC.md

**Owner:** Designer / Product Owner

#### Update when:

- New UI component introduced
- Interaction pattern defined

#### Rules:

- Must align with ROADMAP
- Must not exceed current Step scope

---

### AI_AGENTS.md

**Owner:** Tech Lead

#### Update when:

- Agent added or removed
- Model changes
- Role responsibilities change

#### Do NOT update:

- per Step
- per feature

---

## Handling Product Changes

When Product Owner updates PRODUCT.md:

### Required sequence:

1. Update PRODUCT.md (R-IDs)
2. Tech Lead performs impact analysis
3. Update ARCHITECTURE.md if needed
4. Update ROADMAP.md
5. Update affected STEP-XX.md files

---

## Active Context Rule

At any moment:

> Only one STEP-XX.md is active

Agents must:

- focus on that Step
- ignore unrelated scope
- use only relevant R-IDs and D-IDs

---

## Traceability Model

```text
R-ID → D-ID → STEP → CODE → REVIEW → QA
```

---

## Change Discipline Rules

- No silent changes
- No skipping documents
- No direct code changes from PRODUCT updates
- Always propagate changes forward

---

## Moderator Authority

The Moderator:

- selects active Step
- approves plans
- approves changes
- resolves conflicts
- controls context

---

MOD-W v2.1.0 · Document Lifecycle
