# DOMIAN_LANGUAGE.md

**Project:** {{PROJECT_NAME}}  
**Date:** {{DATE}}  
**Owner:** {{TECH_LEAD_NAME}}

---

## How to Use This Matrix

1. Before writing any prompt, include the relevant rows from this matrix in the **Domain Language** section of the prompt.
2. When the AI agent produces output, verify that it uses the terms in the **Term** column, not the **Avoid** column.
3. Add new rows whenever a step introduces a new concept. Update **Used in code as** and **Used in UI as** once the implementation is accepted.

---

## Terms

| Term | Definition | Used in code as | Used in UI as | Avoid | Notes |
| ---- | ---------- | --------------- | ------------- | ----- | ----- |
|      |            |                 |               |       |       |
|      |            |                 |               |       |       |
|      |            |                 |               |       |       |

---

## Principles

- **One term, one meaning.** A term must map to exactly one concept. If the same word means two things, rename one.
- **Consistent across layers.** The same term should be used in the UI, in code, and in prompts. Avoid synonyms unless they are captured in the Avoid column.
- **Reflect the user's language.** Prefer the vocabulary users themselves would use when describing their work.
- **Keep it current.** A stale matrix produces inconsistent AI output. Review and update after every step.

---

MOD-W v2.0.0 · Moderated AI Development Workflow · github.com/fpmcguire/moderated-ai-development-workflow
