# Roles in Moderated AI Development Workflow

Moderated AI Development Workflow defines a small set of core roles with clear boundaries and accountability. Some roles may be supported or implemented by AI tools, but the role names remain the same regardless of tool choice.

---

## Human Roles

### Moderator

The Moderator is the primary human-in-the-loop operator of Moderated AI Development Workflow.

The Moderator:

- Orchestrates handoffs between roles and artifacts
- Works in the **Workbench** (e.g., VS Code + Copilot) to build, run, test, debug, and fine‑tune changes
- Reviews each step's AI output against the quality gate criteria
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

- Iteratively cross-validates the [PRODUCT.md](../templates/PRODUCT.md) artifact with the Product Owner to clarify intent and constraints
- Authors and maintains the [ARCHITECTURE.md](../templates/ARCHITECTURE.md) artifact
- Authors and maintains the [ROADMAP.md](../templates/ROADMAP.md) artifact
- Defines the [Domain Language Matrix](../templates/DOMAIN_LANGUAGE_MATRIX.md)
- Writes and refines briefs and prompts for AI agents
- Reviews roadmap quality and implementation for technical correctness and maintainability
- Reviews completed steps before they are tagged as done
- Revises output based on Moderator and Product Owner feedback until quality gates are met
- Generates the project-specific `CLAUDE.md` from `ARCHITECTURE.md` and the `CLAUDE.md` template

In one common setup, the Tech Lead role is supported by ChatGPT for architecture thinking, roadmap shaping, and technical review.

### Designer

The Designer is responsible for the visual and interaction design of the product.

The Designer:

- Receives `PRODUCT.md`, `ROADMAP.md`, the Domain Language Matrix, and visual assets (reference images, brand tokens, style descriptions) from the Moderator
- Produces and maintains the `DESIGN-SPEC.md` artifact: colour palette, typography, spacing, component library, screen layouts, interaction patterns, and a Component–Roadmap Map
- Maps every UI component and design decision to the Roadmap Step in which it is first introduced
- Reviews and revises `DESIGN-SPEC.md` based on Product Owner and Moderator feedback until the spec is approved
- Hands the approved `DESIGN-SPEC.md` to the Development Team as a guide for UI implementation
- Does **not** write code or make product scope decisions

In one common setup, the Designer role is supported by Claude for spec generation, visual system definition, and component mapping.

### Development Team

The Development Team is responsible for executing the roadmap steps to build the product.

- Iteratively reviews the [ARCHITECTURE.md](../templates/ARCHITECTURE.md) and [ROADMAP.md](../templates/ROADMAP.md) artifacts with the Tech Lead to understand context and constraints
- Executes the implementation of each step, including code, tests, and documentation
- Revises output based on Moderator and Tech Lead feedback until quality gates are met
- Does **not** directly merge code or override quality gates

**Supported interfaces:**

| Interface                  | Prompt / Config                                      | Best for                                                                    |
| -------------------------- | ---------------------------------------------------- | --------------------------------------------------------------------------- |
| Claude chatbot (claude.ai) | `development-team-claude.md` pasted at session start | Planning, discussion, iterative revision with conversational back-and-forth |
| Claude Code (CLI)          | `CLAUDE.md` in repo root, read automatically         | File writing, multi-file changes, direct repo edits without copy-paste      |

Both interfaces use the same underlying model and the same role rules. The Moderator may switch between them within a single Step provided the repo is committed before switching so Claude Code reads current state. The active `STEP-XX.md` is provided by the Moderator at session start — attached or pasted in the chatbot, or stated as a file path in Claude Code.

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
- Generating the project-specific `CLAUDE.md` from `ARCHITECTURE.md` and the `CLAUDE.md` template

See: [prompts/tech-lead-chatgpt.md](../prompts/tech-lead-chatgpt.md)

### Designer role — Gemini (default)

Gemini may be used to support the Designer role by:

- Analysing `PRODUCT.md`, `ROADMAP.md`, and visual assets to derive a coherent design direction
- Producing `DESIGN-SPEC.md` with colour palette, typography, component library, screen layouts, and interaction patterns
- Mapping UI components to Roadmap Steps so the Development Team knows what to build and when
- Revising the spec based on Product Owner and Moderator feedback

All output is moderated before acceptance.

See: [prompts/designer-gemini.md](../prompts/designer-gemini.md)

### Development Team role — Claude (default)

Claude may be used to support the Development Team role by:

- Reviewing PRODUCT.md, ARCHITECTURE.md, and STEP.md for context
- Proposing and refining the [ROADMAP.md](../templates/ROADMAP.md)
- Generating code, tests, and documentation for a specific step
- Revising output based on Moderator and Tech Lead feedback

All output is moderated before acceptance.

**Two interfaces are supported:**

- **Claude chatbot (claude.ai)** — paste `development-team-claude.md` at the start of a new thread. The Moderator attaches or pastes the active `STEP-XX.md` at session start.
- **Claude Code (CLI)** — place the generated `CLAUDE.md` at the repo root; it is read automatically at session start. The Moderator states the active Step as a file path at session start.

Both interfaces may be used on the same project or the same Step. Commit the repo before switching interfaces.

See: [prompts/development-team-claude.md](../prompts/development-team-claude.md)  
See: [prompts/CLAUDE.md](../prompts/CLAUDE.md) (Claude Code template)

---

## Role Summary Table

| Role                             | Human or AI      | Primary artifacts                                        | Quality gate responsibility               |
| -------------------------------- | ---------------- | -------------------------------------------------------- | ----------------------------------------- |
| Moderator                        | Human            | REVIEW.md, QA.md, repo state                             | Accepts/rejects AI output and step status |
| Product Owner                    | Human            | PRODUCT.md, parts of ROADMAP.md                          | Accepts/rejects step scope and intent     |
| Tech Lead                        | Human            | ARCHITECTURE.md, ROADMAP.md, STEP.md, CLAUDE.md          | Reviews technical quality and fit         |
| QA / Tester                      | Human            | QA.md                                                    | Validates end‑to‑end behaviour            |
| Workbench                        | Human env.       | Local repo, build/test tooling                           | Executes builds/tests, manual checks      |
| Product Owner Agent              | AI (ChatGPT)     | PRODUCT.md drafts, story and criteria suggestions        | None — all output is moderated            |
| Tech Lead Agent                  | AI (ChatGPT)     | ARCHITECTURE.md drafts, technical suggestions, CLAUDE.md | None — all output is moderated            |
| Designer                         | Human            | DESIGN-SPEC.md                                           | Reviews visual quality and fit            |
| Designer Agent                   | AI (Gemini)      | DESIGN-SPEC.md drafts, component mapping                 | None — all output is moderated            |
| Development Team Agent (chatbot) | AI (Claude)      | Code, tests, docs for each step                          | None — all output is moderated            |
| Development Team Agent (CLI)     | AI (Claude Code) | Code, tests, docs for each step                          | None — all output is moderated            |

---

MOD-W v2.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
