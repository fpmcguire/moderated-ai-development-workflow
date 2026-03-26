# Domain Language

Shared domain language is one of the highest-leverage investments a team using Moderated AI Development Workflow can make. When the team, the codebase, and the AI agents all use the same vocabulary, prompts produce more accurate output and reviews are more efficient.

---

## What is Domain Language?

Domain language is the specific vocabulary of your product and its problem space. It includes:

- **Entity names** — the core objects in your system (e.g. `SavedView`, `Dashboard`, `Widget`)
- **Action names** — the verbs that describe what the system does (e.g. `pin`, `share`, `restore`)
- **State names** — the possible states of entities (e.g. `draft`, `published`, `archived`)
- **Role names** — the users and actors in the system (e.g. `viewer`, `editor`, `administrator`)
- **Boundary terms** — where your system begins and ends (e.g. `integration`, `export`, `webhook`)

---

## The Domain Language Matrix

The Domain Language Matrix is a table that captures agreed terms and their usage. See the template at [templates/DOMAIN_LANGUAGE_MATRIX.md](../templates/DOMAIN_LANGUAGE_MATRIX.md).

Each entry in the matrix records:

| Column          | Purpose                               |
| --------------- | ------------------------------------- |
| Term            | The canonical word or phrase          |
| Definition      | What it means in this product         |
| Used in code as | The exact identifier(s) used in code  |
| Used in UI as   | How it appears to users               |
| Avoid           | Terms that should NOT be used instead |
| Notes           | Any disambiguation or context         |

---

## Embedding Domain Language in Prompts

Every prompt sent to an AI agent should include the relevant portion of the Domain Language Matrix. This ensures AI output uses team-agreed vocabulary consistently.

Example pattern (from [prompts/development-team-claude.md](../prompts/development-team-claude.md)):

```
## Domain Language
The following terms must be used consistently in all output:
- SavedView: a user-defined configuration of filters and column visibility saved for reuse
- pin: the action of marking a SavedView as always visible in the sidebar
- ...
```

---

## Maintaining Domain Language

- Domain language is established during the [Project Kickoff ceremony](ceremonies.md).
- New terms are added to the matrix whenever a step introduces a new concept.
- Changes to existing terms require Tech Lead approval and a CHANGELOG entry.
- The matrix is a living artifact — keep it up to date as the product evolves.

---

MOD-W v1.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development
