# Roles in Moderated AI Development

Moderated AI Development defines a small set of core roles with clear boundaries and accountability. Some roles may be supported or implemented by AI tools, but the role names remain the same regardless of tool choice.

---

## Human Roles

### Moderator

The Moderator is the primary human-in-the-loop operator of Moderated AI Development.

The Moderator:

- Orchestrates handoffs between roles and artifacts
- Works in the **Workbench** (e.g., VS Code + Copilot) to build, run, test, debug, and fine‑tune changes
- Reviews each step’s AI output against the quality gate criteria
- Records decisions in the [REVIEW.md](../templates/REVIEW.md) and [QA.md](../templates/QA.md) artifacts
- Has authority to reject output, request retries, or adjust scope

On very small teams the Moderator may also be the Tech Lead and/or Product Owner.

### Product Owner

The Product Owner is responsible for defining _what_ is built and _why_.

The Product Owner:

- Authors and maintains the [PRODUCT.md](../templates/PRODUCT.md) artifact
- Sets acceptance intent and criteria for each roadmap step
- Reviews and approves the [ROADMAP.md](../templates/ROADMAP.md) before implementation
- Participates in ceremonies: Kickoff, Step Review, and Retrospective
- Does **not** directly merge code or override quality gates

In one common setup, the Product Owner role is supported by ChatGPT for product shaping, user stories, and acceptance criteria.

### Tech Lead

The Tech Lead is responsible for _how_ the product is built.

The Tech Lead:

- Authors and maintains the [ARCHITECTURE.md](../templates/ARCHITECTURE.md) artifact
- Defines the [Domain Language Matrix](../templates/DOMAIN_LANGUAGE_MATRIX.md)
- Writes and refines briefs and prompts for AI agents
- Reviews roadmap quality and implementation for technical correctness and maintainability
- Reviews completed steps before they are tagged as done

In one common setup, the Tech Lead role is supported by ChatGPT for architecture thinking, roadmap shaping, and technical review.

### QA / Tester

The QA role validates that accepted output behaves correctly end‑to‑end.

The QA function (which may be performed by the Moderator on small teams):

- Authors and executes the [QA.md](../templates/QA.md) plan for each step
- Verifies that quality gates were met in practice
- Raises defects if accepted output later fails in testing

### Workbench

The Workbench is the human-operated development environment used by the Moderator.

The Workbench:

- Hosts the local clone of the repository (e.g., in VS Code)
- Runs builds, tests, linters, and manual UX checks
- Uses tools like GitHub Copilot for light‑to‑moderate code edits and debugging
- Is the final place where a step must pass before Tech Lead approval and tagging

---

## Default Tool Implementations

### Product Owner role — ChatGPT (default)

ChatGPT may be used to support the Product Owner role by:

- Drafting user stories and acceptance criteria
- Generating initial PRODUCT.md content from a brief
- Suggesting roadmap breakdowns and step boundaries

See: [prompts/product-owner-chatgpt.md](../prompts/product-owner-chatgpt.md)

### Tech Lead role — ChatGPT (default)

ChatGPT may be used to support the Tech Lead role by:

- Generating ARCHITECTURE.md drafts and alternatives
- Suggesting domain language terms and clarifying constraints
- Reviewing technical approaches and proposing implementation strategies

See: [prompts/tech-lead-chatgpt.md](../prompts/tech-lead-chatgpt.md)

### Development Team role — Claude (default)

Claude may be used to support the Development Team role by:

- Reviewing PRODUCT.md, ARCHITECTURE.md, and STEP.md for context
- Proposing and refining the [ROADMAP.md](../templates/ROADMAP.md)
- Generating code, tests, and documentation for a specific step
- Revising output based on Moderator and Tech Lead feedback

All output is moderated before acceptance.

See: [prompts/development-team-claude.md](../prompts/development-team-claude.md)

---

## Role Summary Table

| Role                   | Human or AI  | Primary artifacts                                 | Quality gate responsibility               |
| ---------------------- | ------------ | ------------------------------------------------- | ----------------------------------------- |
| Moderator              | Human        | REVIEW.md, QA.md, repo state                      | Accepts/rejects AI output and step status |
| Product Owner          | Human        | PRODUCT.md, parts of ROADMAP.md                   | Accepts/rejects step scope and intent     |
| Tech Lead              | Human        | ARCHITECTURE.md, ROADMAP.md, STEP.md              | Reviews technical quality and fit         |
| QA / Tester            | Human        | QA.md                                             | Validates end‑to‑end behaviour            |
| Workbench              | Human env.   | Local repo, build/test tooling                    | Executes builds/tests, manual checks      |
| Product Owner Agent    | AI (ChatGPT) | PRODUCT.md drafts, story and criteria suggestions | None — all output is moderated            |
| Tech Lead Agent        | AI (ChatGPT) | ARCHITECTURE.md drafts, technical suggestions     | None — all output is moderated            |
| Development Team Agent | AI (Claude)  | Code, tests, docs for each step                   | None — all output is moderated            |

---

MOD-W v1.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
