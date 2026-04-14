# AI Agents

**Project:** {{PROJECT_NAME}}  
**Date:** {{DATE}}  
**Owner:** {{TECH_LEAD_NAME}}

---

> **Note on related files:**
> - `AI_AGENTS.md` (this file) — project registry of all AI agents, models, interfaces, and data handling decisions. Lives in the `mod-w/` folder.
> - `AGENTS.md` — role configuration for Codex (Tech Lead agent). Read automatically by Codex at session start. Lives at the **repo root**.
> - `CLAUDE.md` — role configuration for Claude Code (Development Team agent). Read automatically by Claude Code at session start. Lives at the **repo root**.

---

## Overview

<!-- Describe the AI agents used in this project, their roles, and the models they run on. -->

---

## Agents

### Product Owner Agent

**Role:** Assists the human Product Owner with planning, user story authoring, and PRODUCT.md drafting  
**Model:** <!-- e.g. ChatGPT (GPT-4o) -->  
**Interface:** <!-- e.g. ChatGPT web, API -->  
**Prompt template:** [prompts/product-owner-chatgpt.md](../prompts/product-owner-chatgpt.md)  
**Context provided:** PRODUCT.md brief, DOMAIN_LANGUAGE.md  
**Moderator:** <!-- Name of the human who reviews this agent's output -->

---

### Tech Lead Agent

**Role:** Assists the human Tech Lead with architecture drafting and domain language definition  
**Model:** <!-- e.g. ChatGPT (GPT-4o) -->  
**Interface:** <!-- e.g. ChatGPT web, API -->  
**Prompt template:** [prompts/tech-lead-chatgpt.md](../prompts/tech-lead-chatgpt.md)  
**Context provided:** PRODUCT.md, existing ARCHITECTURE.md, DOMAIN_LANGUAGE.md  
**Moderator:** <!-- Name of the human who reviews this agent's output -->

---

### Development Team Agent

**Role:** Generates implementation artifacts (code, tests, documentation) for each step  
**Model:** <!-- e.g. Claude 3.5 Sonnet -->  
**Interface:** <!-- e.g. Claude.ai, API -->  
**Prompt template:** [prompts/development-team-claude.md](../prompts/development-team-claude.md)  
**Context provided:** STEP.md, ARCHITECTURE.md, DOMAIN_LANGUAGE.md, relevant source files  
**Moderator:** <!-- Name of the human who reviews this agent's output -->

---

## Data Handling Notes

<!-- Record any decisions about what data is and is not shared with AI models. -->

- **Shared with AI agents:** <!-- e.g. anonymised data models, architecture diagrams, code snippets -->
- **Not shared with AI agents:** <!-- e.g. production data, credentials, PII, proprietary algorithms -->
- **AI provider data policy reviewed:** <!-- Yes / No, and date -->
- **Organisation AI usage policy reviewed:** <!-- Yes / No, and date -->

---

MOD-W v2.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
