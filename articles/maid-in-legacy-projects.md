# Introducing Moderated AI Development into a Legacy Codebase

## Overview

Moderated AI Development (MAID) is a great fit for greenfield projects, but many teams actually need it more in **legacy systems**:

- old frameworks and mixed styles
- partial or outdated docs
- unpredictable coupling and side‑effects

This article shows how to introduce Moderated AI Development into a legacy (brownfield) codebase **incrementally**, without a big‑bang process rewrite.

---

## Design goal: Moderated AI Development as a thin layer

For legacy, treat Moderated AI Development as a **thin governance layer** over your existing process:

- keep your current deployment, CI, and ticketing flow
- add **roles**, **artifacts**, and **quality gates** around AI‑assisted work
- start with **one lane** (one feature or area), not the whole system

Think “add rails around AI use,” not “replace everything with MAID.”

---

## Step 1: Define roles lightly

You do not need a full reorg to use MAID in a legacy codebase. Map existing people to MAID roles:

- **Product Owner** – whoever currently decides “what” and “why” for this area
- **Tech Lead** – whoever is the go‑to person for architecture and code review
- **Development Team** – the people writing code (with AI assistance)
- **Moderator** – a concrete human who:
  - runs builds and tests locally,
  - reviews AI changes,
  - decides whether a Step is accepted

On very small teams, the same person may hold multiple roles. The important part is that **the Moderator role is explicit**.

---

## Step 2: Start with a minimal doc set

For legacy, you can start with a very small set of MAID docs:

- `PRODUCT.md` – for the specific feature/area you’re touching:
  - what problem you’re solving,
  - which users are affected,
  - constraints and non‑goals in the legacy system.
- `ARCHITECTURE.md` – focused on existing structure:
  - modules involved,
  - major dependencies,
  - “do not touch” zones.
- `STEP.md` – for the **one** piece of work you want to run through MAID.
- `REVIEW.md` and `QA.md` – to record what was checked and why it was accepted.

You don’t need to document the entire legacy system up front.  
Start with the **slice you are actually changing**.

---

## Step 3: Pick the right first Step

Choose a Step that is:

- **meaningful, but low‑risk**, for example:
  - adding logging around a tricky area,
  - introducing a single new validation,
  - extracting one small piece of logic.
- **bounded in impact**:
  - limited number of files,
  - minimal new dependencies,
  - easy to revert if needed.

Avoid starting with:

- wide‑ranging refactors,
- cross‑cutting behavior changes,
- multi‑service migrations.

Your goal is to prove that **MAID can improve clarity and safety** on a small change first.

---

## Step 4: Run one Step end‑to‑end

For that first legacy Step:

1. **Shape the Step**
   - Fill in `STEP.md`:
     - current behavior (as observed),
     - desired change,
     - affected files or modules,
     - acceptance criteria (including regression checks).

2. **Use AI under MAID**
   - Let the Development Team use AI (e.g., Copilot, Claude Code, Cursor) to:
     - propose changes,
     - suggest tests,
     - draft refactors.
   - Keep prompts grounded in `PRODUCT.md` and `ARCHITECTURE.md`.

3. **Moderate in the Workbench**
   - The Moderator:
     - checks out the branch locally,
     - runs builds and tests,
     - manually exercises critical flows,
     - inspects diffs with an eye on legacy constraints (“do we risk breaking X?”).

4. **Record REVIEW + QA**
   - Capture in `REVIEW.md`:
     - what changed,
     - issues found and fixed,
     - any compromises made.
   - Capture in `QA.md`:
     - tests run (automated and manual),
     - results,
     - remaining risks and confidence level.

5. **Tag and move on**
   - When satisfied, tag the Step (e.g., `maid-step-001-<name>`).
   - Merge via your normal process (PR, code review, etc.).

---

## Step 5: Make MAID the default for AI work only

You do **not** have to put every change through MAID on day one.  
A practical pattern for legacy is:

- **MAID required** for:
  - any change where AI generates or heavily edits code,
  - changes in high‑risk or historically fragile areas,
  - changes that touch core flows or data models.
- **MAID optional** (at first) for:
  - tiny, manual fixes,
  - pure config changes,
  - documentation‑only edits.

Over time, as the team sees the benefits, you can expand MAID coverage.

---

## Step 6: Use MAID to recover structure

A hidden benefit of MAID in legacy projects is **structure recovery**:

- Each Step leaves a documented trail of:
  - what changed and why,
  - how it was tested,
  - where in the legacy system it lives.
- Over multiple Steps you naturally accumulate:
  - clarified architecture in `ARCHITECTURE.md`,
  - updated terminology in `DOMAIN_LANGUAGE_MATRIX.md`,
  - known risk areas recorded in REVIEW/QA notes.

You’re effectively turning a messy system into a **gradually better‑documented system**, one Step at a time.

---

## Step 7: Watch out for common traps

A few things to avoid when applying MAID to legacy code:

- **Too big, too soon** – starting with a huge refactor and blaming MAID when it’s painful. Start small.
- **Skipping the Moderator** – letting AI and PR reviews stand in for real, local testing.
- **Letting docs lag behind** – making changes without updating PRODUCT/ARCHITECTURE/STEP, which erodes the value of MAID.
- **Expecting AI to understand legacy quirks** – the Moderator must still know (or learn) the system’s sharp edges.

---

## Where MAID helps most in legacy projects

MAID is especially valuable when:

- new contributors or juniors need to work safely in a legacy system,
- you’re introducing AI coding tools for the first time and want guardrails,
- the system has a history of “safe‑looking changes” causing regressions later,
- you want a clearer audit trail of AI‑assisted changes.

By scoping MAID to **AI‑touching work** first, you add discipline where risk is highest while keeping the rest of your process familiar.

---

## Summary

To introduce MAID into a legacy project:

1. Map existing people to MAID roles, especially the Moderator.
2. Start with a **minimal document set** focused on a single area.
3. Run one well‑chosen Step end‑to‑end under MAID.
4. Require MAID for AI‑assisted changes first.
5. Let MAID slowly **recover structure** in your legacy system over multiple Steps.

You don’t have to fix the legacy system all at once.  
You just need to make sure every AI‑assisted change makes it a little safer and clearer than before.

---

MAID v1.0.0 · Moderated AI Development · [https://github.com/fpmcguire/moderated-ai-development](https://github.com/fpmcguire/moderated-ai-development)
