# Copilot Instructions for MAID

This repository contains the **Moderated AI Development** methodology framework — a structured approach to using AI models (such as ChatGPT and Claude) in software development under human moderation.

## Project Context

- This is a documentation and methodology repository, not a software project.
- Files are primarily Markdown.
- The methodology is structured around **roles**, **ceremonies**, **artifacts**, **quality gates**, and a **step lifecycle**.
- Key terms are defined in [docs/glossary.md](../docs/glossary.md) and [docs/domain-language.md](../docs/domain-language.md).

## Conventions

- Use sentence case for headings (e.g. `## Step lifecycle` not `## Step Lifecycle`) unless it is a proper noun or acronym.
- Keep language concise and practitioner-focused — the audience is software development teams adopting AI tooling.
- Templates use ALL_CAPS filenames (e.g. `STEP.md`, `REVIEW.md`).
- Prompts are organised by AI model target (ChatGPT vs Claude).

## When Editing Templates

- Preserve the placeholder comment style: `<!-- description of expected content -->`.
- Do not remove existing section headings from templates unless explicitly asked.

## When Editing Docs

- Cross-link related documents using relative paths (e.g. `[Roles](roles.md)`).
- If you add a new term, add it to the glossary.

## When Editing Prompts

- Never include real credentials, API keys, or personal data in prompt examples.
- Mark placeholders clearly: `{{PLACEHOLDER}}`.
