# AI Agents

**Project:** {{PROJECT_NAME}}
**Date:** {{DATE}}
**Owner:** {{TECH_LEAD_NAME}}

---

## Overview

This project uses multiple AI agents under MOD-W.

Each agent has:

- a defined role
- controlled scope
- human moderation

---

## Agents

### Product Owner

**Role:** Product definition and scope
**Models:** ChatGPT + Perplexity
**Responsibility:**

- Define PRODUCT.md
- Maintain R-IDs
- Validate external facts

---

### Tech Lead

**Role:** Architecture and planning
**Model:** Codex
**Responsibility:**

- Maintain ARCHITECTURE.md (D-IDs)
- Generate ROADMAP.md
- Define STEP-XX.md

---

### Development Team

**Role:** Implementation
**Model:** Claude Code
**Responsibility:**

- Implement STEP-XX.md
- Produce code + tests
- Stay within scope

---

### Cross-Check Reviewer

**Role:** Independent validation
**Model:** Gemini
**Responsibility:**

- Validate plans and implementations
- Detect missing requirements
- Identify risks and scope drift

---

## Agent Interaction Rules

- No agent self-approves its work
- Planning and implementation are separated
- All work is Step-scoped
- Moderator approves all transitions

---

## Data Handling

- No credentials or sensitive data shared
- Only necessary context packets provided
- External data validated via Product Owner

---

## Update Rules

- Update when:
  - a new agent is introduced
  - model version changes
  - role responsibilities change
- Do NOT update per Step

---

MOD-W v2.1.0
