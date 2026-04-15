# Ceremonies in Moderated AI Development Workflow

Ceremonies are structured events that create rhythm, transparency, and shared understanding in a Moderated AI Development Workflow team.

---

## 1. Project Kickoff

**When:** Once, at the start of a project or major initiative  
**Who:** Product Owner, Tech Lead, (optional) Moderator  
**Duration:** 1–2 hours

**Purpose:** Align the team on scope, methodology, and tooling before AI work begins.

**Activities:**

- Review and agree on [PRODUCT.md](../templates/PRODUCT.md)
- Draft or review [ARCHITECTURE.md](../templates/ARCHITECTURE.md)
- Establish the [DOMAIN_LANGUAGE.md](../templates/DOMAIN_LANGUAGE.md)
- Agree on which AI agents will be used and for which roles
- Review the [ROADMAP.md](../templates/ROADMAP.md) and identify the first step

**Output:** Completed PRODUCT.md, initial ARCHITECTURE.md, DOMAIN_LANGUAGE.md, first STEP.md created

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

MOD-W v2.1.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
