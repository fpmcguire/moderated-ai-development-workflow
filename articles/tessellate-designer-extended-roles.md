# Tessellate Designer: Example of Extended Roles in Moderated AI Development Workflow

## Overview

Moderated AI Development Workflow v1.0.0 defines a **minimal role set** (Product Owner, Tech Lead, Development Team, Moderator, QA/Workbench).  
Tessellate Designer is an example project that shows how you can **add upstream roles**—specifically **Customer** and **Product Designer**—without changing the core method.

This article explains:

- what Tessellate Designer is (at a high level)
- how it extends Moderated AI Development Workflow’s roles with Customer and Product Designer
- which artifacts those roles influence
- how a single Step flows through the extended lane

---

## What is Tessellate Designer?

Tessellate Designer is a Moderated AI Development Workflow example project focused on a **UI/UX‑heavy feature** (e.g., designing and managing “tessellated” layouts or views in a SaaS frontend). Its purpose in the repo is to:

- demonstrate Moderated AI Development Workflow’s Step‑based workflow, and
- illustrate how **Customer** and **Product Designer** roles can wrap around the core Product → Architecture → Implementation chain.

Rather than changing Moderated AI Development Workflow v1.0.0’s base roles, Tessellate Designer **adds**:

- a Customer lane at the very start (real problems, language, constraints), and
- a Product Designer lane between Customer and Product Owner (flows, screens, interactions).

---

## Extended roles in Tessellate Designer

### Customer (example role)

The Customer role represents real users or stakeholders of Tessellate Designer.

They:

- bring in **raw input**—interviews, support tickets, analytics, existing workflows;
- describe pains, goals, constraints, and vocabulary;
- react to prototypes and early flows.

They do _not_ decide scope or architecture. Their voice is mediated through the Product Designer and Product Owner.

### Product Designer (example role)

The Product Designer translates customer reality into **experience design**:

- user flows and scenarios,
- key screens and states,
- interaction rules and UX constraints,
- accessibility considerations.

They:

- collaborate with the Customer (where available) and Product Owner,
- influence `PRODUCT.md` and any design‑oriented artifact (e.g., a DESIGN.md or design section),
- collaborate with the Tech Lead to ensure designs respect technical constraints.

They do _not_ merge code or override technical decisions; they are peers to the Product Owner on the “what/experience” side.

---

## How extended roles fit into Moderated AI Development Workflow v1.0.0

Tessellate Designer keeps Moderated AI Development Workflow’s core roles intact:

- **Product Owner** – defines what and why in `PRODUCT.md`.
- **Tech Lead** – defines how in `ARCHITECTURE.md` and designs `ROADMAP.md` + Steps.
- **Development Team** – implements Steps, often with AI assistance.
- **Moderator** – runs the Workbench and controls quality gates.

It simply adds **two upstream contributors**:

- Customer → influences inputs to PRODUCT and DESIGN.
- Product Designer → transforms Customer inputs into flows and UX, and co‑shapes PRODUCT.

In other words, the **conceptual lane** becomes:

> Customer → Product Designer → Product Owner → Tech Lead → Development Team → Moderator

Moderated AI Development Workflow still only _requires_ the core v1.0.0 roles. Tessellate Designer **shows how to extend** them.

---

## Artifacts in Tessellate Designer

Tessellate Designer demonstrates how extended roles can be grounded in artifacts rather than chat history. A typical setup is:

- `PRODUCT.md`
  - Owned by Product Owner.
  - Incorporates insights from Customer and Product Designer  
    (problems, workflows, UX constraints, non‑goals).

- `DESIGN.md` or a design section within `PRODUCT.md`
  - Owned by Product Designer.
  - Contains flows, key screens, interaction notes, accessibility considerations.
  - Links to external design tools (e.g., Figma) if used.

- `ARCHITECTURE.md`
  - Owned by Tech Lead.
  - Reflects constraints discovered by Customer and Product Designer (performance, platform, layout limitations).

- `ROADMAP.md`, `STEP-XX.md`, `REVIEW.md`, `QA.md`
  - Same as in base Moderated AI Development Workflow: Steps, briefs, review notes, verification evidence.

Extended roles **add context and constraints** to existing artifacts; they don’t require new core file types in Moderated AI Development Workflow v1.0.0.

---

## Example Step flow in Tessellate Designer

Here’s how a typical Step might flow with extended roles:

1. **Customer input**
   - A customer complains that rearranging a tessellated layout is confusing and inconsistent across devices.
   - Insights are captured in notes that feed into PRODUCT/DESIGN work.

2. **Product Designer exploration**
   - Product Designer sketches updated flows and layout interactions.
   - Records the chosen flows and key states in `DESIGN.md` (or a design section).

3. **Product Owner shaping**
   - Product Owner updates `PRODUCT.md` to reflect:
     - new user goals and success criteria,
     - scope for the current iteration (MVP of layout improvements),
     - out‑of‑scope items.

4. **Tech Lead planning**
   - Tech Lead updates `ARCHITECTURE.md` (constraints, components involved, data impact).
   - Designs a small set of Steps in `ROADMAP.md`.
   - Authors a specific `STEP-XX.md` for “Improve layout drag‑and‑drop behavior” aligned with the design.

5. **Development Team implementation**
   - Development Team uses AI tooling (e.g., Claude, Copilot, Cursor) to implement the Step.
   - Prompts include relevant excerpts from PRODUCT, DESIGN, ARCHITECTURE, and the Domain Language Matrix.

6. **Moderator verification**
   - Moderator runs builds/tests locally, exercises the flow, and compares against:
     - `PRODUCT.md` goals,
     - `DESIGN.md` interactions,
     - `STEP-XX.md` acceptance checks.
   - Records outcomes in `REVIEW.md` and `QA.md` and decides whether to accept or request revisions.

This shows **how** Customer and Product Designer inform the Step, without requiring them to be baked into Moderated AI Development Workflow’s core v1.0.0 roles.

---

## Why Tessellate Designer is v2‑ish but not v2

Tessellate Designer serves as a **preview of Moderated AI Development Workflow v2‑style usage**:

- demonstrates upstream roles (Customer, Product Designer),
- shows how to anchor them in artifacts and ceremonies,
- gives a concrete example others can copy or adapt.

But Moderated AI Development Workflow itself stays at **v1.0.0**:

- core docs and roles remain minimal,
- extended roles are presented as **optional patterns**,
- no one is forced to adopt Customer / Product Designer roles just to use Moderated AI Development Workflow.

This keeps the methodology approachable while still showing a credible path to richer, cross‑validated workflows.

---

MOD-W v1.1.0 · Moderated AI Development Workflow · [https://github.com/fpmcguire/moderated-ai-development-workflow](https://github.com/fpmcguire/moderated-ai-development-workflow)
