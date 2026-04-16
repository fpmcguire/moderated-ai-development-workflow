# Ceremonies in Moderated AI Development Workflow

Ceremonies are structured events that create rhythm, transparency, and shared understanding in a Moderated AI Development Workflow team.

---

## 1. Project Kickoff

The kickoff is split into two sequential, Moderator-gated phases. Neither phase ends until the Moderator explicitly approves its output. The second phase does not begin until the first is approved.

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

### 1b. Architecture Definition

**When:** After `PRODUCT.md` is approved; revisited when product scope changes materially  
**Who:** Tech Lead session, Moderator  

**Purpose:** Produce a Moderator-approved `ARCHITECTURE.md` and `DOMAIN_LANGUAGE.md` before the roadmap and steps are defined.

**Activities:**

- Moderator triggers a Tech Lead Planning Session with the approved `PRODUCT.md`.
- Tech Lead drafts `ARCHITECTURE.md` and `DOMAIN_LANGUAGE.md`.
- Moderator reviews and iterates — requesting `options`, `ramifications`, or cross-validation from other agents as needed.
- Revisions loop until Moderator is satisfied.
- Once `ARCHITECTURE.md` is approved, Tech Lead generates `ROADMAP.md`, `CLAUDE.md`, and `AGENTS.md`.

**Gate:** Moderator explicitly approves `ARCHITECTURE.md`. Roadmap and step definition do not begin until this gate is passed.

**Output:** Approved `ARCHITECTURE.md`, `DOMAIN_LANGUAGE.md`, `ROADMAP.md`, `CLAUDE.md`, `AGENTS.md`.

---

## 2. Step Planning

**When:** Before each step begins  
**Who:** Tech Lead, (optional) Product Owner  
**Duration:** 30–60 minutes

**Purpose:** Define the scope, inputs, outputs, and quality gate for the next step.

**Activities:**

- Author or refine the [STEP.md](../templates/STEP.md) for the upcoming step
- Confirm acceptance criteria with the Product Owner
- Select the appropriate AI agent and prompt template
- Identify any risks or dependencies

**Output:** Approved STEP.md for the next step

---

## 3. AI Work Session

**When:** During the step, as needed  
**Who:** Moderator + Development Team agent  
**Duration:** Variable

**Purpose:** Generate the step's artifacts using the AI agent under human guidance.

**Activities:**

- Submit prompts to the AI agent following [development team guidelines](../prompts/development-team-claude.md)
- Review response in Workbench following [workbench guideline](../docs/workbench-guide.md)
- Iteratively refine prompts if output is unsatisfactory
- Record all prompts and responses

**Output:** Raw AI-generated artifacts ready for moderation

---

## 4. Step Review

**When:** After the AI work session, before the step is closed  
**Who:** Moderator, Tech Lead, (optional) Product Owner  
**Duration:** 30–60 minutes

**Purpose:** Moderate AI output against the quality gate and decide whether to accept, revise, or reject.

**Activities:**

- Review AI output against STEP.md acceptance criteria
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

MOD-W v3.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
