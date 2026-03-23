# From Vibe Coding to Viable Coding with Moderated AI Development

## Overview

AI coding tools have made it possible to “just start typing” and let the model fill in the rest.  
That style — often called **vibe coding** — is fun, fast, and great for exploration, but it breaks down quickly in real products.

**Moderated AI Development** exists to turn that same power into **viable coding**: a disciplined, reviewable workflow where AI is a powerful collaborator, not an ungoverned committer.

This article explains:

- what “vibe coding” and “viable coding” mean in practice
- why vibe coding fails for serious systems
- how Moderated AI Development makes viable coding concrete through roles, artifacts, and quality gates

---

## What is “vibe coding”?

Vibe coding is an informal pattern that looks roughly like this:

- Open an AI assistant (chat or IDE).
- Describe what you want in natural language.
- Let the model generate or edit large chunks of code.
- Skim the result, maybe tweak a few lines.
- Run it and see what happens.

It is **not** inherently wrong. Vibe coding is useful when:

- you are exploring a new API or library
- you are doing quick UI experiments
- you are hacking together a one‑off script or proof of concept

The problem is what happens when this becomes the **default** for production work:

- No stable source of truth (specs live inside the last prompt).
- Little or no artifact trail (no clear “what changed, why, and based on which assumptions”).
- Large, opaque diffs that are hard to review properly.
- Hidden missing pieces: validation, logging, error paths, edge cases.

Vibe coding optimizes for **speed of typing**, not **safety of change**.

---

## What is “viable coding”?

**Viable coding** is a pattern where AI is still heavily used, but within a workflow that makes changes:

- reviewable
- reproducible
- traceable
- and safe to extend

In practical terms, viable coding means:

- Work is broken into **small, bounded steps** with explicit goals and acceptance criteria.
- There are **clear roles** for product, architecture, implementation, and moderation.
- AI assistants are used **inside** that structure, not instead of it.
- Every change leaves behind **artifacts** (PRODUCT, ARCHITECTURE, STEP, REVIEW, QA).
- Nothing enters the product without passing a **human quality gate**.

Instead of “prompt and hope,” viable coding is “prompt, plan, implement, review, verify.”

Moderated AI Development is one concrete implementation of viable coding.

---

## How Moderated AI Development turns vibe into viable

Moderated AI Development makes viable coding explicit through three pillars:

1. **Roles** – who thinks about what
2. **Artifacts** – where that thinking is recorded
3. **Gates** – how changes are accepted or rejected

### 1. Roles

Moderated AI Development v1.0.0 defines four core roles:

- **Product Owner** – defines _what_ is built and _why_.
- **Tech Lead** – defines _how_ it is built and how work is sliced.
- **Development Team** – implements each Step (often with AI support).
- **Moderator** – runs the Workbench, reviews output, and controls quality gates.

These roles may be supported by different AI tools (e.g., Perplexity, ChatGPT, Claude, Copilot), but the human Moderator retains final authority.

By splitting responsibilities, Moderated AI Development makes sure no single AI interaction silently covers product, design, architecture, and implementation.

### 2. Artifacts

Instead of burying decisions inside chat logs, Moderated AI Development uses a small set of shared artifacts:

- `PRODUCT.md` – what we are building and why
- `ARCHITECTURE.md` – how we are structuring it
- `ROADMAP.md` – ordered list of Steps
- `STEP.md` – brief for a single Step
- `REVIEW.md` – review decisions per Step
- `QA.md` – verification evidence per Step
- `DOMAIN_LANGUAGE_MATRIX.md` – shared vocabulary
- `AGENTS.md` – rules and conventions for AI agents

Vibe coding tends to generate code first and documentation later (if at all).  
Moderated AI Development insists that **intent and design are captured in artifacts before and alongside code**.

### 3. Quality gates

Each Step in Moderated AI Development has an explicit **quality gate**:

- defined in `STEP.md`
- evaluated in `REVIEW.md` and `QA.md`
- enforced by the Moderator in the Workbench

A Step is not “done” because the model says so. It is done when:

- the implementation matches PRODUCT and ARCHITECTURE intent
- tests and checks in QA are green
- the Moderator accepts the Step and tags it in Git

Vibe coding treats model output as a suggestion you might ship.  
Moderated AI Development treats it as **raw material** that must survive review and verification.

---

## Blue‑red pattern in Moderated AI Development

Many viable‑coding discussions talk about a **blue‑red** pattern:

- **Blue** – plans and implements (makes changes).
- **Red** – reviews and verifies (tries to break them).

Moderated AI Development implements this pattern across roles:

- Tech Lead and Development Team act as the **blue side** (planning and implementation through ROADMAP + STEP).
- Tech Lead (in review mode) and Moderator form the **red side** (review and verification through REVIEW + QA + Workbench).

The point is that the same agent that proposed the change does **not** unilaterally approve it.

---

## Where vibe coding still fits

Moderated AI Development does not ban vibe coding. It just defines **where it is safe**:

- early exploration and spike solutions
- quick experiments in a throwaway branch
- trying out an unfamiliar API or UI pattern

The key difference is what happens **after** the spike:

- For throwaway work, you can stop there.
- For anything that will live in the main codebase, Moderated AI Development asks you to move into the viable‑coding path:
  - capture the insight in PRODUCT / ARCHITECTURE / DOMAIN LANGUAGE
  - design a Step
  - implement it under moderation

“Vibe to learn, Moderated AI Development to ship.”

---

## Summary: Moderated AI Development as viable coding in practice

If you want one sentence:

> Moderated AI Development is a viable‑coding workflow: it turns AI‑assisted development from ad‑hoc vibe coding into step‑based, artifact‑driven, human‑moderated change.

Use vibe coding when you are exploring.  
Use Moderated AI Development when you care about what happens next week, next month, and after your next teammate joins.

---

MAID v1.0.0 · Moderated AI Development · https://github.com/fpmcguire/moderated-ai-development
