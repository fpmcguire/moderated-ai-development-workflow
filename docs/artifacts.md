# Artifacts

Moderated AI Development is artifact‑driven.  
Each role works against a small set of shared files that keep intent, architecture, implementation, and verification aligned.

---

## Overview

| Artifact                  | Owner (primary) | Purpose                                    |
| ------------------------- | --------------- | ------------------------------------------ |
| PRODUCT.md                | Product Owner   | What we’re building and why                |
| ARCHITECTURE.md           | Tech Lead       | How we’re building it                      |
| DOMAIN_LANGUAGE_MATRIX.md | Tech Lead       | Shared domain and agent language           |
| ROADMAP.md                | Tech Lead       | Ordered list of Steps                      |
| STEP.md                   | Tech Lead       | Brief for a single Step                    |
| REVIEW.md                 | Moderator       | Review history and decisions per Step      |
| QA.md                     | Moderator / QA  | Test and verification record per Step      |
| AGENTS.md                 | Tech Lead       | Instructions and conventions for AI agents |

Templates for each are in `/templates`.

---

## PRODUCT.md

**Owner:** Product Owner  
**Audience:** All roles and agents

Defines the product concept and scope:

- Problem, users, and value proposition
- Core workflows and feature set
- Functional and non‑functional requirements
- Constraints and out‑of‑scope items
- Acceptance intent at a product level

PRODUCT.md is the main reference for “what” and “why” in every Step.

---

## ARCHITECTURE.md

**Owner:** Tech Lead  
**Audience:** Tech Lead, Development Team, Moderator

Captures key technical decisions:

- Project type and stack
- Boundaries (modules, services, front/back split)
- Data model and integration points
- Testing strategy and tooling
- Risks and architectural decisions log

ARCHITECTURE.md is the main reference for “how” and “where” changes should be made.

---

## DOMAIN_LANGUAGE_MATRIX.md

**Owner:** Tech Lead (with Product Owner)  
**Audience:** All roles and agents

Defines the project’s shared vocabulary:

- Domain entities and important terms
- Business vs. technical meaning
- Allowed and banned synonyms
- Owner and source artifact for each term
- Code naming guidance

This keeps humans and agents aligned on terminology.

---

## ROADMAP.md

**Owner:** Tech Lead (with Product Owner)  
**Audience:** All roles and agents

Lists the project’s planned Steps:

- Ordered list of small, verifiable Steps
- Goal and acceptance checks per Step
- Dependencies and risks

ROADMAP.md is the bridge between product intent and implementation work.

---

## STEP.md

**Owner:** Tech Lead (per Step)  
**Audience:** Development Team, Moderator, Tech Lead

Defines a single Step:

- Goal and scope
- Inputs and relevant files
- Required changes
- Acceptance checks
- Risks and notes for reviewers

STEP.md is the main brief for the Development Team agent.

---

## REVIEW.md

**Owner:** Moderator  
**Audience:** Moderator, Tech Lead, Product Owner

Records review history and decisions per Step:

- Summary of changes
- Moderator findings
- Tech Lead recommendations
- Required revisions
- Final approval status

REVIEW.md is the narrative of why a Step was accepted.

---

## QA.md

**Owner:** Moderator / QA  
**Audience:** Moderator, Tech Lead, stakeholders

Captures verification evidence per Step:

- Builds and tests run and their results
- Manual checks (UX, flows)
- Bugs found and their disposition
- Regression risks and confidence level

QA.md is the ground‑truth view of quality for each Step.

---

## AGENTS.md

**Owner:** Tech Lead  
**Audience:** All agents; Moderator

Defines how agents should behave in this repo:

- Global rules and constraints
- Build, test, and lint commands
- Coding conventions and style rules
- Review expectations
- Role descriptions and limits for Product Owner Agent, Tech Lead Agent, and Development Team Agent

AGENTS.md is effectively the “repo constitution” for AI behaviour.

---

## Usage

For each new project or example:

1. Copy templates from `/templates` into the project root.
2. Fill out PRODUCT.md and ARCHITECTURE.md first.
3. Create DOMAIN_LANGUAGE_MATRIX.md as soon as core terms appear.
4. Maintain ROADMAP.md and STEP.md as you plan work.
5. Update REVIEW.md and QA.md for every Step.
6. Keep AGENTS.md aligned with your actual tools and commands.

---

MAID v1.0.0 · Moderated AI Development · https://github.com/fpmcguire/moderated-ai-development
