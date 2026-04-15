# Moderated AI Development Workflow Principles

These principles elaborate on the values in the [Moderated AI Development Workflow Manifesto](manifesto.md) and guide day-to-day practice.

## 1. Humans own the outcome

Every artifact — code, documentation, architecture, tests — must be understood and accepted by a human before it is considered done. "The AI wrote it" is never an acceptable explanation for a defect.

## 2. One step at a time

Work proceeds in discrete, bounded steps. Each step has a defined scope, a single AI agent assignment, and a quality gate. Steps are not combined or skipped to save time.

## 3. Prompts are artifacts

Every prompt sent to an AI model is written down, stored, and reviewed. Prompts are not throwaway interactions — they are engineering decisions that affect output quality.

## 4. Domain language drives prompts

Before writing prompts, the team establishes and agrees on domain language. This vocabulary is embedded in every prompt and template to ensure AI output uses the team's own terms consistently.

## 5. Quality gates are non-negotiable

Each step ends with a quality gate. Gates may not be waived. If output does not meet the gate criteria, the step is retried or escalated.

## 6. Roles are clear and respected

Moderated AI Development Workflow defines specific roles for humans and AI agents. Role boundaries are respected — a product owner does not do tech lead work, and an AI agent does not make scope decisions.

## 7. The moderator is a skilled practitioner

Moderating AI output requires deep expertise. The moderator must be able to evaluate correctness, identify hallucinations, and make judgement calls. This is not a junior task.

## 8. Transparency is built in

All AI interactions, moderation decisions, and quality gate outcomes are recorded. Nothing is hidden. The team can always trace how an artifact came to be.

## 9. The process improves continuously

Teams are expected to reflect on Moderated AI Development Workflow ceremonies and adapt the methodology to their context. Feedback is shared with the community via adoption stories and method improvement proposals.

## 10. Security and privacy are first-class concerns

No real credentials, personal data, or sensitive business information is ever included in a prompt. Teams review their AI provider's data policies before use.

---

MOD-W v2.1.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
