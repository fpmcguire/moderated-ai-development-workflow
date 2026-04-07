# Glossary

This glossary defines the core terms used in the Moderated AI Development Workflow methodology. For product-specific domain terms, see the [Domain Language Matrix](../templates/DOMAIN_LANGUAGE_MATRIX.md) for each project.

---

**AI agent**  
An AI model (such as ChatGPT or Claude) assigned a specific role in the Moderated AI Development Workflow process. AI agents generate artifacts that are always moderated by a human before acceptance. See [roles.md](roles.md).

**AI work session**  
A ceremony in which the Tech Lead submits prompts to an AI agent to generate step artifacts. See [ceremonies.md](ceremonies.md).

**Artifact**  
Any document, file, or record produced during a Moderated AI Development Workflow step or project. Artifacts include PRODUCT.md, ARCHITECTURE.md, STEP.md, REVIEW.md, and QA.md. See [artifacts.md](artifacts.md).

**Ceremony**  
A structured, time-boxed event in the Moderated AI Development Workflow process. Ceremonies include Kickoff, Step Planning, AI Work Session, Step Review, QA Verification, and Retrospective. See [ceremonies.md](ceremonies.md).

**Domain language**  
The agreed vocabulary of a product and its problem space, captured in the Domain Language Matrix and embedded in all AI prompts. See [domain-language.md](domain-language.md).

**Domain Language Matrix**  
A table that records canonical domain terms, their definitions, their code identifiers, and terms to avoid. See [templates/DOMAIN_LANGUAGE_MATRIX.md](../templates/DOMAIN_LANGUAGE_MATRIX.md).

**Hallucination**  
AI-generated content that is factually incorrect, references non-existent APIs or libraries, or invents information. A key target of the moderation quality gate.

**Moderator**  
The human responsible for reviewing AI-generated artifacts against quality gate criteria before accepting them. See [roles.md](roles.md).

**Prompt**  
The instruction given to an AI agent to generate a specific artifact. Prompts are written, stored, and reviewed as first-class engineering artifacts. See [principles.md](principles.md).

**Quality gate**  
An explicit checklist of criteria that AI-generated artifacts must satisfy before acceptance. Gates are defined in STEP.md and evaluated in REVIEW.md. See [quality-gates.md](quality-gates.md).

**ROADMAP.md**  
A project-level artifact listing all planned steps, their order, and their current status. See [templates/ROADMAP.md](../templates/ROADMAP.md).

**Step**  
The fundamental unit of work in MOD-W. A step is a bounded, reviewable slice of AI-assisted development with a defined scope, quality gate, and lifecycle. See [step-lifecycle.md](step-lifecycle.md).

**STEP.md**  
An artifact that defines a single step: its scope, inputs, expected outputs, acceptance criteria, assigned AI agent, and quality gate level. See [templates/STEP.md](../templates/STEP.md).

**Tech Lead**  
The human responsible for technical architecture, prompt authoring, and moderation of AI output. See [roles.md](roles.md).

**Workbench**  
The environment in which AI work sessions are conducted — typically a web-based chat interface (e.g. ChatGPT, Claude.ai) or an IDE with AI integration. See [prompts/workbench-usage-guidelines.md](../prompts/workbench-usage-guidelines.md).

---

MOD-W v1.1.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
