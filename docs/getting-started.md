# Getting Started with MOD-W

New to MOD-W? Start here.

---

## 1. Understand the methodology

Read these three documents in order:

1. [`docs/manifesto.md`](manifesto.md) — why MOD-W exists and its core beliefs.
2. [`docs/roles.md`](roles.md) — who does what (Moderator, Product Owner, Designer + Prototyper, Tech Lead, Development Team, QA).
3. [`docs/step-lifecycle.md`](step-lifecycle.md) — how a step moves from idea to accepted, tagged output.

---

## 2. Set up your project

1. Copy the templates from [`/templates`](../templates/) into your project's `mod-w/` folder.
2. Run the **Project Kickoff** ceremonies to produce approved planning artifacts — this is iterative work, not a fill-in-the-blanks exercise:
   - **1a. Product Definition** — iterate with the Product Owner SubAgent until `PRODUCT.md` is Moderator-approved.
   - **1b. Prototype Ceremony (optional, v4)** — when the project has visual, interaction, chart, or real-time risk, iterate with Claude Design until `DESIGN-SPEC.md`, `prototype/`, and `ARCHITECTURE-NOTES.md` are Moderator-approved.
   - **1c. Architecture Definition** — iterate with the Codex Tech Lead session until `ARCHITECTURE.md` is Moderator-approved. If the Prototype Ceremony ran, Codex performs the Architecture Handoff from all four kickoff inputs. Tech Lead then generates `ROADMAP.md`, `CLAUDE.md`, and `AGENTS.md`.
   - See [`docs/ceremonies.md`](ceremonies.md) for the full gated process.
3. Place `CLAUDE.md` and `AGENTS.md` at your repo root.
4. Create your first `STEP-01.md` using the [`STEP-XX.md` template](../templates/STEP-XX.md).

---

## 3. Run your first step

Follow the [`docs/step-lifecycle.md`](step-lifecycle.md) end-to-end for your first feature or change. The [example project](../examples/frontend-saved-views/) shows a complete worked example.

---

## 4. Reference docs

| What you need         | Where to find it                                        |
| --------------------- | ------------------------------------------------------- |
| Artifact definitions  | [`docs/artifacts.md`](artifacts.md)                     |
| Quality gates         | [`docs/quality-gates.md`](quality-gates.md)             |
| Moderator checklist   | [`docs/moderator-checklist.md`](moderator-checklist.md) |
| Domain language guide | [`docs/domain-language.md`](domain-language.md)         |
| Ceremonies            | [`docs/ceremonies.md`](ceremonies.md)                   |
| Tool integrations     | [`docs/integrations/`](integrations/)                   |
| FAQ                   | [`docs/faq.md`](faq.md)                                 |

---

MOD-W v4.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
