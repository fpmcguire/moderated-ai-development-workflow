# Using Moderated AI Development Workflow with Gemini

Gemini provides a unique ecosystem for MOD-W, offering specific tools like **Gems** for role separation and **NotebookLM** for persistence.

## Why Use Gemini for MOD-W?

- **Role-Based Gems:** Create dedicated "Gems" for the Product Owner, Tech Lead, and Dev Team using the prompts in `/prompts`.
- **NotebookLM for Traceability:** Act as a permanent "Project Archive." Upload your `PRODUCT.md` and `ARCHITECTURE.md` to ground the AI in your specific project constraints.
- **Google Workspace Integration:** Use the `@Google Drive` extension to pull directly from your "Source of Truth" templates.

## Implementation Strategy

1. **Configure Gems:** Use the standards in **[prompts/prompt-guidelines.md](./prompts/prompt-guidelines.md)** to set up your custom Gems.
2. **Persistence:** Upload your core docs to a NotebookLM instance for the project.
3. **Execution:** Follow the **Options → Ramifications → Mentorship** flow for every major handoff.

---

MOD-W v2.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
