# Frequently Asked Questions

## General

**What is Moderated AI Development?**  
Moderated AI Development is a methodology framework for teams using AI models (such as ChatGPT and Claude) to assist in software development. MOD-W provides roles, ceremonies, artifacts, quality gates, and prompt templates to ensure AI output is always reviewed and accepted by a qualified human before it enters the product. See the [manifesto](manifesto.md).

**Is Moderated AI Development Workflow a replacement for Agile or Scrum?**  
No. Moderated AI Development Workflow is a complementary framework that can be layered on top of Agile, Scrum, Kanban, or any other delivery methodology. MOD-W focuses specifically on the AI-assisted development workflow within a team's existing process.

**Do I need to use a specific AI model?**  
No. Moderated AI Development Workflow is model-agnostic. The prompt templates provide versions for ChatGPT and Claude, but the principles apply to any AI model. Adapt the prompts to your chosen tool.

**Does Moderated AI Development Workflow work for solo developers?**  
Yes. A solo developer can hold multiple MOD-W roles (Product Owner, Tech Lead, Moderator). The key discipline is maintaining the separation of concerns: plan separately, generate separately, review separately.

---

## Methodology

**Why can't quality gates be waived?**  
Quality gates exist to ensure that AI-generated artifacts meet a known standard of correctness before they enter the product. Waiving a gate means accepting unverified AI output — the exact risk MOD-W is designed to prevent. If a gate cannot be met, the correct response is to adjust the step scope or retry the prompt, not to skip the gate. See [quality-gates.md](quality-gates.md).

**What if the AI agent produces output that partially meets the criteria?**  
The Moderator should document which criteria were met and which were not in REVIEW.md, then return the step to In Progress with specific guidance for the Tech Lead to refine the prompt. Partial acceptance is not permitted.

**How large should a step be?**  
A step should be small enough that a moderator can thoroughly review the AI output in a single sitting (typically 30–60 minutes). If a step feels too large, split it. If a step produces more than ~200 lines of code or a document longer than 2–3 pages, consider splitting it.

**Can we use AI to moderate AI output?**  
No. Moderation must be performed by a qualified human. Using one AI to evaluate another AI's output does not satisfy the MOD-W quality gate. The human moderator must understand and personally vouch for the accepted artifact.

---

## Tooling

**Which AI model should I use for development?**  
MOD-W recommends Claude for the Development Team Agent role (code generation) and ChatGPT for Product Owner and Tech Lead Agent roles (planning and architecture). This is based on practical experience but is not prescriptive — use what works best for your team.

**Should prompts be stored in the repository?**  
Yes. Prompts are first-class artifacts in MOD-W and should be stored alongside the artifacts they produce. This enables traceability, reproducibility, and team learning.

**What is a workbench?**  
The workbench is the environment where AI work sessions happen — typically a chat interface like ChatGPT or Claude.ai, or an IDE with AI integration. See [prompts/workbench-usage-guidelines.md](../prompts/workbench-usage-guidelines.md) for how to use it effectively.

---

## Community

**How do I share my experience with MOD-W?**  
Open an [Adoption Story](https://github.com/fpmcguire/moderated-ai-development/issues/new?template=adoption-story.md) issue. Your experience helps the community improve the methodology.

**How do I suggest a change to the methodology?**  
Open a [Method Improvement](https://github.com/fpmcguire/moderated-ai-development/issues/new?template=method-improvement.md) issue. See [CONTRIBUTING.md](../CONTRIBUTING.md) and [GOVERNANCE.md](../GOVERNANCE.md) for how decisions are made.

---

MOD-W v1.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development
