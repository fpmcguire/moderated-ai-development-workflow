# Role-Tooling-Matrix

This matrix suggests tools and models for each Moderated AI Development Workflow role. They are examples, not requirements.

| Role                       | Primary focus            | Example tools          | What they validate                                           |
| -------------------------- | ------------------------ | ---------------------- | ------------------------------------------------------------ |
| Product Owner              | Value, scope, acceptance | ChatGPT or Perplexity  | Right thing to build                                         |
| Tech Lead                  | Architecture, risks      | ChatGPT                | Sound way to build it                                        |
| Development Team (chatbot) | Implementation, tests    | Claude (claude.ai)     | Correct, scoped execution — conversational, plan-first       |
| Development Team (CLI)     | Implementation, tests    | Claude Code            | Correct, scoped execution — direct repo edits, no copy-paste |
| Workbench                  | Build, test, debug       | Local IDE + Copilot    | All outputs work as intended                                 |
| Moderator                  | Alignment, gates         | Local IDE + Perplexity | All outputs aligned enough to proceed                        |

---

## Choosing between Claude chatbot and Claude Code

| Signal              | Prefer chatbot                       | Prefer Claude Code                 |
| ------------------- | ------------------------------------ | ---------------------------------- |
| Step type           | Planning, discussion, early revision | Implementation, multi-file changes |
| Context size        | Small — a few files pasted           | Large — whole repo available       |
| Copy-paste overhead | Acceptable                           | A bottleneck                       |
| Mid-step switch     | —                                    | Commit repo first, then switch     |

Both interfaces use the same underlying model and the same role rules. The Moderator may use both on the same project or the same Step.

**Active Step handoff:**

- **Claude chatbot** — Moderator attaches or pastes `STEP-XX.md` directly at session start.
- **Claude Code** — Moderator states the file path at session start, e.g. `The current Step is apps/my-app/mod-w/STEP-02.md`

---

MOD-W v2.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
