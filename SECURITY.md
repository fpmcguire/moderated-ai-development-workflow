# Security Policy

## Scope

This repository contains methodology documentation, templates, and prompts — not executable software. As such, the primary security concerns relate to:

- **Prompt injection risks** in AI prompt templates
- **Sensitive data leakage** in example files or templates
- **Misleading guidance** that could lead practitioners to expose secrets to AI models

## Reporting a Concern

If you discover content in this repository that:

- Could lead users to inadvertently share sensitive information with AI models
- Contains prompt patterns that could be exploited for harmful purposes
- Includes any other security-relevant issue

Please open a [GitHub Security Advisory](../../security/advisories/new) rather than a public issue. Alternatively, contact the maintainers directly via GitHub.

## AI Model Usage Guidance

When using the prompts and templates in this repository:

1. **Never include real credentials, secrets, API keys, or personal data** in prompts sent to AI models.
2. **Review your organisation's AI usage policy** before sending proprietary code or architecture details to any AI model.
3. **Treat AI model outputs as untrusted input** — always have a human moderator review AI-generated content before merging.
4. **Be mindful of data residency requirements** — check whether the AI model you are using stores or trains on your input.

## Supported Versions

This methodology framework does not have versioned releases in the traditional software sense. See [CHANGELOG.md](CHANGELOG.md) for the history of changes.

---

MOD-W v1.0.0 · Moderated AI Development Workflow · github.com/fpmcguire/moderated-ai-development-workflow
