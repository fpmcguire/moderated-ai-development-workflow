# Moderated AI Development Workflow (MOD-W) + OpenSpec

## Overview

**OpenSpec** is a lightweight, open-source framework for **Spec-Driven Development (SDD)**. It specializes in **brownfield development**, emphasizing a "structure before code" approach for existing codebases. Its core loop is **Propose → Apply → Archive**.

**Moderated AI Development Workflow (MOD-W)** provides the governance layer, defining the roles and human-driven checkpoints that ensure OpenSpec’s lightweight automation remains safe and aligned with project goals.

This playbook explains:

- How OpenSpec's change-centric artifacts map to MOD-W's core documents.
- How MOD-W roles supervise OpenSpec CLI commands.
- A checklist for running a **Moderated OpenSpec Change Cycle**.

---

## Conceptual mapping

OpenSpec operates on a **Change Management** model where every feature or fix lives in an independent subfolder under `openspec/changes/<id>/` until it is merged into the system's "Source of Truth".

| OpenSpec Artifact | MOD-W Artifact(s)             | MOD-W Purpose                                                |
| :---------------- | :---------------------------- | :----------------------------------------------------------- |
| `openspec/specs/` | `PRODUCT.md`                  | The "Source of Truth" representing the current system state. |
| `proposal.md`     | `ROADMAP.md` / `STEP-XX.md`   | The "Why" and "What" of a specific change delta.             |
| `design.md`       | `ARCHITECTURE.md`             | Technical approach, trade-offs, and decisions.               |
| `tasks.md`        | `STEP-XX.md` (Implementation) | The concrete checklist for the AI agent.                     |
| `archive/`        | Git History / Tags            | The audit trail of validated and merged changes.             |

---

## Roles in a MOD-W + OpenSpec setup

- **Product Owner (PO)**
  - Owns the `proposal.md` and `specs/` delta.
  - Ensures the OpenSpec **Propose** phase accurately captures user needs and acceptance criteria.
- **Tech Lead**
  - Owns `design.md` and technical consistency.
  - Reviews the OpenSpec **Proposal** to ensure it doesn't break existing module boundaries or introduce technical debt.
- **Development Team**
  - Executes the **Apply** phase.
  - Follows the generated `tasks.md` sequentially to implement the code.
- **Moderator**
  - Controls the **Archive** phase.
  - Performs the final **Workbench** verification (build/test/UX).
  - Signs off on the `REVIEW.md` and `QA.md` before the change is merged into the Source of Truth.

---

## Phase-by-phase playbook

### 1. Proposal ↔ Step Initialization

**Goal:** Define a change delta without polluting the main codebase.

- **OpenSpec:** Run `/opsx:propose <change-name>` to scaffold a new folder in `openspec/changes/`.
- **MOD-W:** The Moderator assigns a **Step ID** (e.g., `STEP-05`) that matches the OpenSpec `change-id`.
- **Gate:** The Tech Lead must approve the `design.md` before implementation begins to avoid "catastrophic forgetting" of system constraints.

### 2. Implementation ↔ The Apply Phase

**Goal:** Drive the AI agent using the isolated spec context.

- **OpenSpec:** Run `/opsx:apply`. The agent reads _only_ the spec deltas, making it highly token-efficient.
- **MOD-W:** The Development Team agent must update the status of `tasks.md` as it progresses.
- **Gate:** If the AI encounters ambiguity, it must pause and ask the Moderator for a decision rather than "vibe coding" a solution.

### 3. Verification ↔ The Verify Phase

**Goal:** Ensure the implementation matches the intent.

- **OpenSpec:** Use `/opsx:verify` to validate that all requirements in the spec delta are implemented.
- **MOD-W:** The Moderator performs a manual code review against the `design.md` and recorded scenarios.
- **Gate:** Record evidence in `QA.md`. The implementation must pass all "GIVEN/WHEN/THEN" scenarios defined in the proposal.

### 4. Archiving ↔ Step Closure

**Goal:** Merge the validated change into the permanent record.

- **OpenSpec:** Run `/opsx:archive` (or `/opsx:sync`) to move the delta into the `openspec/specs/` source of truth.
- **MOD-W:** The Moderator marks the Step as **Done** in the `ROADMAP.md` and creates a Git tag.

---

## Running a Moderated OpenSpec Change

1. **Scaffold:** Run `openspec init` (if first time) and `/opsx:propose`.
2. **Refine:** Human PO/Tech Lead edits `proposal.md` and `design.md`.
3. **Validate:** Run `openspec validate <id> --strict`.
4. **Implement:** Run `/opsx:apply`. AI executes `tasks.md`.
5. **Moderate:** Moderator checks the Workbench and runs `/opsx:verify`.
6. **Finalize:** Run `/opsx:archive` to update the living specification.

---

## Best practices

- **Brownfield Focus:** Use OpenSpec's ability to "capture existing state" to build the `PRODUCT.md` and `ARCHITECTURE.md` incrementally if they don't already exist.
- **Token Efficiency:** Keep change deltas small. If a proposal has more than 5-7 major tasks, break it into two MOD-W Steps.
- **Living Documentation:** Ensure the **Archive** phase is never skipped; this ensures your MOD-W "Source of Truth" never rots.

---

## **The MOD-W + OpenSpec Lifecycle**

This detailed section outlines the end-to-end lifecycle of a project using **MOD-W governance** and **OpenSpec automation**. By combining these frameworks, you ensure that AI-driven development remains disciplined, traceable, and human-verified from the initial baseline to the final product.

### **1. Setup & Baselining (The "Project Constitution")**

Before writing code, you must establish the "Source of Truth" for your codebase.

- **Initialize OpenSpec:** Run `openspec init` to create the global `openspec/specs/` directory.
- **Establish the Baseline:** Use the `/opsx:explore` command to have the AI analyze your existing codebase and generate a project-wide `PRODUCT.md` and initial specs.
- **MOD-W Governance:** The **Moderator** and **Tech Lead** review these baseline specs to ensure the AI's "mental model" of the system matches the actual business intent and architecture.

### **2. Proposal & Design (The "What" and "How")**

For every new feature or fix, follow a change-centric workflow to avoid context pollution.

- **Create a Change Folder:** Run `/opsx:new <feature-name>`. This scaffolds a dedicated environment in `openspec/changes/<id>/` where all artifacts for this delta will live.
- **Draft the Proposal:** Use `/opsx:continue` to generate `proposal.md`.
  - **MOD-W Role:** The **Product Owner** reviews this to ensure the "What" is correct before technical design begins.
- **Technical Design:** Generate `design.md` and `tasks.md`.
  - **MOD-W Role:** The **Tech Lead** approves the technical approach, checking for architectural fit and potential regressions.

### **3. Implementation & Validation (The "Apply" Phase)**

The implementation phase is strictly bound by the approved specifications.

- **Execute Implementation:** Run `/opsx:apply <change-name>`. The AI agent reads the `tasks.md` checklist and implements the code changes in isolation.
- **MOD-W Role:** If the AI encounters a technical blocker, it must not "guess." It must pause and flag the **Development Team** for human intervention or a spec update.
- **Verify Compliance:** Run `/opsx:verify` to audit the code against the `GIVEN/WHEN/THEN` scenarios in your specs. Critical issues must be resolved before the Moderator proceeds.

### **4. Moderation & Workbench Check (The "Gatekeeper")**

OpenSpec confirms the code matches the spec, but MOD-W confirms the code is "production-ready".

- **Workbench Verification:** The **Moderator** pulls the changes into their local environment and runs manual UX checks, performance tests, and security scans.
- **The Artifact Sign-off:** The Moderator updates `REVIEW.md` and `QA.md` with final findings. If accepted, they give the final command to integrate the change.

### **5. Archiving & Sync (The "Finished Product")**

The change is only "finished" when it moves from a delta to the system's permanent record.

- **Merge & Sync:** Run `/opsx:archive`. This merges the delta specs into the main `openspec/specs/` directory, updating your "Source of Truth" for future AI sessions.
- **Clean Workspace:** The change folder is moved to an `archive/` directory to maintain a clean audit trail and prevent context drift in subsequent features.

---

## **Summary Table: Workflow Integration**

| Phase      | Command(s)                     | Lead Role     | MOD-W Outcome                         |
| :--------- | :----------------------------- | :------------ | :------------------------------------ |
| **Setup**  | `openspec init` / `explore`    | Tech Lead     | Validated baseline `PRODUCT.md`.      |
| **Define** | `/opsx:new` / `/opsx:continue` | Product Owner | Approved `proposal.md` & `specs`.     |
| **Plan**   | `/opsx:continue`               | Tech Lead     | Approved `design.md` & `tasks.md`.    |
| **Build**  | `/opsx:apply`                  | Dev Team      | Verified implementation via `verify`. |
| **Finish** | `/opsx:archive`                | Moderator     | `REVIEW.md` sign-off & spec sync.     |

---

MOD-W v2.1.0 · Moderated AI Development Workflow
