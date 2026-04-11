# MOD-W Prompting Guide: From "Vibe" to "Viable"

In the Moderated AI Development Workflow, prompting is a tool for **decision support, mentorship, and risk mitigation**. This guide ensures every role provides the transparency needed for high-integrity moderation.

## 1. The Strategic Prompting Flow

Every handoff between roles (e.g., Product Owner to Tech Lead) should follow this three-layer request:

### A. Options & Analysis

Never accept a single solution. Force the AI to act as a consultant:

- **Request:** "Provide three distinct implementation options (e.g., Minimal, Robust, Scalable)."
- **Why:** This prevents the model from defaulting to the most "frequent" (and often mediocre) training data solution.

### B. Impact & Ramifications

Before approving a plan, the Moderator must understand the cost:

- **Request:** "For the recommended option, list technical debt, security risks, and side effects on existing modules."
- **Why:** This flags "silent failures" and architectural drift for the human Moderator.

### C. The Mentorship Loop (The "Why")

Use the AI to level up the team and maintain high standards:

- **Request:** "Explain the design pattern used here. Why is this superior to [Alternative]? Treat this as a code review for a junior engineer."
- **Why:** This turns the workflow into a continuous learning engine.

---

## 2. Standard Answer Depths

MOD-W prompts support three standard depths to balance speed and rigor:

| Depth       | Use Case                         | Expected Output                          |
| :---------- | :------------------------------- | :--------------------------------------- |
| **Minimal** | Trivial fixes, UI tweaks         | Direct answer, code only, minimal prose. |
| **Options** | Standard features, refactors     | Multiple approaches + trade-off matrix.  |
| **Full**    | Critical logic, new architecture | Deep-dive explanations and mentorship.   |

---

## 3. The "Red-Team" Quality Gate

Used by the **Moderator** before final approval of a Step:

> "Analyze this implementation as a cynical Senior Architect. Find three reasons why this might fail in production or lead to a regression. Be specific and merciless."

---

MOD-W v2.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
