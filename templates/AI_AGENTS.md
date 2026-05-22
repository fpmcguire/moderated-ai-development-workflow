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

**Role:** Product definition and acceptance validation
**Interface (Definition):** Claude chatbot + Perplexity + Gemini — no project infrastructure yet
**Interface (Validation):** Claude Code SubAgent
**Responsibility:**

- Author and maintain PRODUCT.md (via chatbot at project start)
- Validate completed Steps against acceptance checks (via SubAgent, after Tech Lead approval)
- Sign off before Moderator final gate

---

### Tech Lead

**Role:** Architecture, planning, and technical review
**Interface:** Codex (full session, reads AGENTS.md)
**Responsibility:**

- Author and maintain ARCHITECTURE.md, ROADMAP.md, STEP-XX.md
- Generate project-specific CLAUDE.md and AGENTS.md
- Review completed Steps and write REVIEW.md

---

### Development Team

**Role:** Implementation
**Interface:** Claude Code SubAgent (reads CLAUDE.md)
**Responsibility:**

- Implement STEP-XX.md following the approved plan
- Run blocking build gate before handing off
- Produce code + tests scoped to the active Step

---

### QA

**Role:** Acceptance validation
**Interface:** Claude Code SubAgent
**Responsibility:**

- Validate implementation against STEP-XX.md acceptance checks
- Write QA.md with results and manual check list
- Runs after Tech Lead approval

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

MOD-W v3.0.0
