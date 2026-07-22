# Ceremonies in Moderated AI Development Workflow

Ceremonies are structured events that create rhythm, transparency, and shared understanding in a Moderated AI Development Workflow team.

---

## 1. Project Kickoff

The kickoff has up to three sequential, Moderator-gated phases. When the optional Prototype Ceremony runs (v4), it slots between Product Definition and Architecture Definition. No phase ends until the Moderator explicitly approves its output; the next phase does not begin until the previous is approved.

---

### 1a. Product Definition

**When:** Once at project start; revisited when scope changes materially  
**Who:** Moderator, with Claude chatbot, Perplexity, and Gemini as research and cross-validation tools  

**Purpose:** Produce a Moderator-approved `PRODUCT.md` before any architecture work begins.

Note: no `CLAUDE.md` or `AGENTS.md` exists yet at this stage. All tools are used as external chatbots or research assistants, not as configured agents.

**Activities:**

- Moderator uses Claude chatbot to draft and refine `PRODUCT.md`.
- Moderator uses Perplexity for fact-finding, market context, and requirement research.
- Moderator uses Gemini for informal cross-validation of scope, goals, and user workflows.
- Moderator iterates across tools until satisfied — requesting `options`, `ramifications`, or alternative framings as needed.
- Revisions loop until Moderator is satisfied.

**Gate:** Moderator explicitly approves `PRODUCT.md`. Architecture work does not begin until this gate is passed.

**Output:** Approved `PRODUCT.md`.

---

### 1b. Prototype Ceremony (v4, optional)

**When:** After `PRODUCT.md` is approved; when the Moderator decides the product warrants it
**Who:** Moderator, with Claude Design as the Designer + Prototyper

Produces `DESIGN-SPEC.md`, a working `prototype/` folder, and advisory `ARCHITECTURE-NOTES.md`. Run when the product has novel interaction models, real-time data, or unusual visual systems; skip for conventional UI.

**Gate:** Moderator explicitly approves the ceremony output (cross-validation pause required). Architecture Definition does not begin until this gate is passed.

**Output:** Approved `DESIGN-SPEC.md`, `prototype/` folder, `ARCHITECTURE-NOTES.md`.

See `docs/prototype-ceremony.md` for the full lifecycle.

---

### 1c. Architecture Definition

**When:** After `PRODUCT.md` is approved; revisited when product scope changes materially  
**Who:** Tech Lead (Codex) session, Moderator

**Purpose:** Produce a Moderator-approved `ARCHITECTURE.md` and `DOMAIN_LANGUAGE.md` before the roadmap and steps are defined.

**Activities:**

- Moderator triggers a Tech Lead Planning Session with the approved `PRODUCT.md`.
- Tech Lead drafts `ARCHITECTURE.md` and `DOMAIN_LANGUAGE.md`.
- Moderator reviews and iterates — requesting `options`, `ramifications`, or cross-validation from other agents as needed.
- Revisions loop until Moderator is satisfied.
- Once `ARCHITECTURE.md` is approved, Tech Lead generates `ROADMAP.md`, `CLAUDE.md`, and `AGENTS.md`.

**Gate:** Moderator explicitly approves `ARCHITECTURE.md`. Roadmap and step definition do not begin until this gate is passed.

**Output:** Approved `ARCHITECTURE.md`, `DOMAIN_LANGUAGE.md`, `ROADMAP.md`, `CLAUDE.md`, `AGENTS.md`.

> **v4 note:** If the Prototype Ceremony ran, this ceremony is the Architecture Handoff — Codex consumes all four kickoff inputs (`PRODUCT.md`, `DESIGN-SPEC.md`, `prototype/`, `ARCHITECTURE-NOTES.md`) and independently authors `ARCHITECTURE.md` with explicit authority to override prototype-implied structures. See `docs/architecture-handoff.md`.

---

## 2. Step Planning

**When:** Before each step begins  
**Who:** Tech Lead, (optional) Product Owner  
**Duration:** 30–60 minutes

**Purpose:** Define the scope, inputs, outputs, and quality gate for the next step.

**Activities:**

- Author or refine the [STEP-XX.md](../templates/STEP-XX.md) for the upcoming step
- Confirm acceptance criteria with the Product Owner
- Select the appropriate AI agent and prompt template
- Identify any risks or dependencies

**Output:** Approved STEP-XX.md for the next step

---

## 3. Development Team Session

**When:** During the step, after the Implementation Options Gate  
**Who:** Moderator + Development Team (Claude Code)  
**Duration:** Variable

**Purpose:** Implement the approved Step directly in the repository under human moderation.

**Activities:**

- Moderator opens a Claude Code session in the project root — `CLAUDE.md` loads automatically
- Moderator states the active Step (e.g. `The current Step is STEP-02.md`)
- Development Team restates the Step, proposes an implementation plan, and waits for Moderator approval before writing any files
- Development Team implements the Step, runs the build gate, and spawns QA and Product Owner SubAgents
- Moderator reviews the diff in the Workbench and responds to any clarifying questions
- See [development team prompt](../prompts/development-team-claude.md) and [workbench guide](../docs/workbench-guide.md) for detail

**Output:** Implemented Step with passing build, `QA.md`, and Product Owner sign-off

---

## 4. Step Review

**When:** After the AI work session, before the step is closed  
**Who:** Moderator, Tech Lead, (optional) Product Owner  
**Duration:** 30–60 minutes

**Purpose:** Moderate AI output against the quality gate and decide whether to accept, revise, or reject.

**Activities:**

- Review AI output against STEP-XX.md acceptance criteria
- Complete the [REVIEW.md](../templates/REVIEW.md) artifact
- Record moderation decisions and any concerns
- Accept, request revisions, or reject the output

**Output:** Completed REVIEW.md; accepted artifacts committed to the repository

---

## 5. QA Verification

**When:** After step acceptance, before the step is marked Done  
**Who:** QA / Tester  
**Duration:** Variable

**Purpose:** Verify that accepted AI output behaves correctly in context.

**Activities:**

- Execute the test plan in [QA.md](../templates/QA.md)
- Record test results and any defects found

**Output:** Completed QA.md; step marked Done or defects raised

---

## 6. Retrospective

**When:** At the end of each sprint, release, or significant milestone  
**Who:** All team members  
**Duration:** 1 hour

**Purpose:** Reflect on how the methodology is working and identify improvements.

**Activities:**

- What went well with MOD-W this iteration?
- What friction did we encounter?
- What should we change about our prompts, quality gates, or ceremonies?
- Are there adoption stories or method improvements to contribute to the community?

**Output:** Action items; potential community contributions (adoption story, method improvement issue)

---

MOD-W v4.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
