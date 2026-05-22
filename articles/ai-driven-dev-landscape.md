# AI-Assisted & Automated Product and Code Production Workflows - April 12, 2026

## Tools, Agents, and Methodologies — April 2026 Reference

---

## Overview

The landscape of AI-driven software development has undergone a step-change since 2024. What began as IDE autocompletion has rapidly evolved into a spectrum spanning **spec-driven methodologies** (where human-authored specifications become the source of truth for AI-generated code), **agentic IDEs** (full development environments where AI autonomously plans, edits, tests, and deploys across multiple files), **autonomous coding agents** (cloud-hosted workers that operate independently on tasks for hours or days), and **no-code/low-code AI builders** (platforms that generate full-stack apps from a single natural-language prompt). Teams at Goldman Sachs, Anthropic, and Amazon have all reported deploying AI agents that handle substantial portions of their software development lifecycle.[^1][^2][^3]

The underlying paradigm shift is the move from **"vibe coding"** (ad-hoc, prompt-and-pray) to **"viable coding"** — structured, spec-anchored workflows where AI is a disciplined participant rather than an ad-hoc assistant. This report organizes the landscape into four categories and provides a comprehensive reference table.[^4][^5]

---

## The Four Layers of AI-Driven Development

### 1. Methodologies & Frameworks

Structured approaches that define _how_ humans and AI collaborate — covering workflow phases, artifact standards, and role definitions. These are tool-agnostic processes.

### 2. Spec-Driven Development (SDD) Tools & Frameworks

Tools and frameworks built specifically to operationalize the spec-first philosophy — turning requirements into structured specs, plans, tasks, and finally generated code with human gates at each phase, or into lighter-weight spec/change workflows.[^6][^7]

### 3. Agentic IDEs & Coding Assistants

Full-featured development environments or extensions where an AI agent can autonomously read files, edit code across a repository, run terminal commands, and iterate on results — with the human reviewing diffs rather than writing every line.[^23][^25][^31][^34]

### 4. AI App Builders & Autonomous Agents

Cloud-hosted agents and browser-based platforms that take a high-level prompt (or spec) and produce a deployable full-stack application or execute a complete engineering task end-to-end.[^42][^45][^47][^52][^58]

---

## Comprehensive Reference Table

| #   | Tool / Methodology                            | Category                             | Key Features                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Surface / Delivery                                   | Pricing (Apr 2026)       | URL                                                                                                                      |
| --- | --------------------------------------------- | ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------- | ------------------------ | ------------------------------------------------------------------------------------------------------------------------ |
| 1   | **SDD (Spec-Driven Development)**             | Methodology                          | 4-phase lifecycle: Specify → Plan → Task → Implement; spec-as-source-of-truth; human review gates; eliminates ad-hoc “vibe coding”; parallel agent execution on non-overlapping tasks.[^6][^7][^8]                                                                                                                                                                                                                                                                                                                                                                             | Framework (tool-agnostic)                            | Free (methodology)       | [Wikipedia](https://en.wikipedia.org/wiki/Spec-driven_development)                                                       |
| 2   | **Moderated AI Development Workflow (MOD-W)** | Methodology                          | Role-based SDD workflow with Product Owner, Tech Lead, Development Team, and human Moderator; intentional multi-model diversity as a cross-validation quality mechanism; explicit HITL quality gates; artifact-driven (PRODUCT, ARCHITECTURE, ROADMAP, STEP, REVIEW, QA, DOMAIN_LANGUAGE, AGENTS); optimized for maintainability and traceability over raw speed.[^9]                                                                                                                                                                                                          | Framework (tool-agnostic) + templates + prompt packs | Free / Open Source       | [github.com/fpmcguire/moderated-ai-development-workflow](https://github.com/fpmcguire/moderated-ai-development-workflow) |
| 3   | **BMAD Method**                               | Methodology                          | “Breakthrough Method for Agile AI-Driven Development”; two broad phases (planning + context-engineered development); multiple role-based agents; PRD → Architecture → Story → Code → QA pipeline; artifact-centric delivery.[^5][^10][^11]                                                                                                                                                                                                                                                                                                                                     | Framework / CLI installer                            | Free / Open Source       | [github.com/bmad-code-org/BMAD-METHOD](https://github.com/bmad-code-org/BMAD-METHOD)                                     |
| 4   | **GitHub Spec Kit**                           | SDD Tool                             | Open-source CLI + slash-command workflow; 4 commands: `/specify`, `/plan`, `/tasks`, `/implement`; bootstraps SDD scaffolding in AI coding assistants; artifacts committed to workspace.[^7][^12]                                                                                                                                                                                                                                                                                                                                                                              | CLI + workspace templates                            | Free / Open Source       | [developer.microsoft.com](https://developer.microsoft.com/blog/spec-driven-development-spec-kit)                         |
| 5   | **OpenSpec**                                  | **SDD Tool / Spec-Driven Framework** | Lightweight, portable spec-driven framework for AI coding assistants; current behavior stored in `openspec/specs/`; proposed work organized in `openspec/changes/`; each change can include proposal, design, tasks, and spec deltas; standard OPSX workflow is fluid and iterative rather than rigidly phased; `openspec init` can install skills and commands for supported assistants; default core profile includes `propose`, `explore`, `apply`, and `archive`, with expanded workflows such as `verify`, `sync`, and `onboard` available.[^81][^82][^83][^84][^85][^86] | CLI + generated assistant integrations / skills      | Free / Open Source       | [github.com/Fission-AI/OpenSpec](https://github.com/Fission-AI/OpenSpec)                                                 |
| 6   | **Kiro**                                      | SDD Tool + Agentic IDE               | AWS-built spec-driven IDE; Requirements → Design Doc → Task List workflow; autonomous agent hooks; MCP support; persistent context; learns from PRs and feedback.[^4][^13][^14][^15]                                                                                                                                                                                                                                                                                                                                                                                           | Desktop IDE (VS Code-based fork)                     | Free tier + paid tiers   | [kiro.dev](https://kiro.dev)                                                                                             |
| 7   | **Tessl**                                     | SDD Tool / Platform                  | “Spec-as-source” paradigm; generated code linked back to specs; spec registry; deterministic conformance tests; intended to reduce API hallucinations and improve reliability.[^16][^17][^18]                                                                                                                                                                                                                                                                                                                                                                                  | SaaS platform + CLI                                  | Freemium                 | [tessl.io](https://tessl.io)                                                                                             |
| 8   | **Cursor**                                    | Agentic IDE                          | VS Code fork rebuilt around AI; Composer mode; autonomous Agent Mode; Mission Control; predictive autocomplete; visual editing.[^19][^20][^21][^22]                                                                                                                                                                                                                                                                                                                                                                                                                            | Desktop IDE                                          | Free tier + paid tiers   | [cursor.com](https://cursor.com)                                                                                         |
| 9   | **Claude Code**                               | Agentic Coding Agent                 | Terminal agent; reads and writes files, runs shell commands, performs web tasks, uses subagents, supports hooks and checkpoints; available with editor integrations.[^23][^24]                                                                                                                                                                                                                                                                                                                                                                                                 | CLI + VS Code + JetBrains                            | API / subscription-based | [claude.ai/code](https://claude.ai/code)                                                                                 |
| 10  | **GitHub Copilot**                            | Agentic IDE Extension                | Agent Mode; Next Edit Suggestions; Copilot Workspace; MCP support; multi-model support.[^25][^26][^27]                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | IDE extension                                        | Free tier + paid tiers   | [github.com/features/copilot](https://github.com/features/copilot)                                                       |
| 11  | **Windsurf (Codeium)**                        | Agentic IDE                          | Cascade multi-file agent; terminal execution; iterative testing; automatic RAG indexing; multi-model support.[^28][^29][^30]                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Desktop IDE + plugins                                | Free tier + paid tiers   | [windsurf.com](https://windsurf.com)                                                                                     |
| 12  | **Amazon Q Developer**                        | Agentic IDE Extension                | AWS-native coding assistant; autonomous feature implementation, refactoring, test generation, reviews, and infrastructure generation.[^31][^32][^33]                                                                                                                                                                                                                                                                                                                                                                                                                           | IDE extension + CLI                                  | Free tier + paid tiers   | [aws.amazon.com/q/developer](https://aws.amazon.com/q/developer)                                                         |
| 13  | **Gemini Code Assist**                        | Agentic IDE Extension                | Agent Mode; large-context codebase awareness; GCP, Firebase, and BigQuery integration; CLI workflows.[^34][^35][^36][^37]                                                                                                                                                                                                                                                                                                                                                                                                                                                      | IDE extension + CLI                                  | Free tier + paid tiers   | [developers.google.com/gemini-code-assist](https://developers.google.com/gemini-code-assist/docs/overview)               |
| 14  | **Google Antigravity**                        | Agentic IDE                          | Manager view for multi-agent orchestration; artifact-based verification; inline plan feedback; agent-first environment.[^38][^39][^41]                                                                                                                                                                                                                                                                                                                                                                                                                                         | Desktop IDE                                          | Public preview           | [antigravity.google](https://antigravity.google)                                                                         |
| 15  | **OpenAI Codex**                              | Autonomous Agent + Platform          | Multi-agent coding platform; isolated sandboxes; reusable skills; CLI, editor, desktop, and CI/CD integrations.[^42][^43][^44]                                                                                                                                                                                                                                                                                                                                                                                                                                                 | SaaS + CLI + extensions                              | Subscription / API       | [platform.openai.com/codex](https://platform.openai.com/codex)                                                           |
| 16  | **Devin**                                     | Autonomous Agent                     | Autonomous software engineer for planning, coding, debugging, testing, and deployment; strong fit for well-scoped engineering tasks.[^1][^2][^45][^46]                                                                                                                                                                                                                                                                                                                                                                                                                         | SaaS                                                 | Paid tiers               | [devin.ai](https://devin.ai)                                                                                             |
| 17  | **Replit Agent**                              | AI App Builder / Cloud IDE           | Long autonomous sessions; self-healing loops; built-in DB and deploy; collaborative cloud environment.[^47][^48][^49][^50]                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Browser / SaaS                                       | Free tier + paid tiers   | [replit.com](https://replit.com)                                                                                         |
| 18  | **Bolt.new**                                  | AI App Builder                       | Full-stack generation from prompt; browser runtime; GitHub export; Figma and image input.[^51][^52][^53]                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Browser / SaaS                                       | Free tier + paid tiers   | [bolt.new](https://bolt.new)                                                                                             |
| 19  | **Vercel v0**                                 | AI UI Builder                        | UI-focused generation from text or image mockups; instant preview; one-click deploy; strong component-level iteration.[^54][^55][^56][^57]                                                                                                                                                                                                                                                                                                                                                                                                                                     | Browser / SaaS                                       | Free tier + paid tiers   | [v0.dev](https://v0.dev)                                                                                                 |
| 20  | **Lovable**                                   | AI App Builder                       | Full-stack builder with Plan Mode, Agent Mode, visual edits, GitHub sync, and Supabase integration.[^58][^59][^60]                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Browser / SaaS                                       | Free tier + paid tiers   | [lovable.dev](https://lovable.dev)                                                                                       |
| 21  | **Firebase Studio (Project IDX)**             | Cloud IDE + AI Builder               | Browser-based full-stack dev environment; Gemini integration; broad framework support and browser-hosted development stack.[^61][^62]                                                                                                                                                                                                                                                                                                                                                                                                                                          | Browser / SaaS                                       | Free                     | [firebase.studio](https://firebase.studio)                                                                               |
| 22  | **Aider**                                     | Agentic CLI Tool                     | Open-source terminal pair programmer; git-native; multi-model; architect mode; automated lint and test loops.[^63][^64][^65]                                                                                                                                                                                                                                                                                                                                                                                                                                                   | CLI / terminal                                       | Free (API costs)         | [aider.chat](https://aider.chat)                                                                                         |
| 23  | **Continue.dev**                              | IDE Extension (Open Source)          | Open-source AI code agent; chat, edit, and agent modes; bring-your-own-model; diff-view edits; PR checks.[^66][^67][^68][^69]                                                                                                                                                                                                                                                                                                                                                                                                                                                  | IDE extension                                        | Free / Open Source       | [continue.dev](https://continue.dev)                                                                                     |
| 24  | **Tabnine**                                   | Enterprise AI Coding Assistant       | Privacy-first positioning; on-prem, VPC, and air-gapped deployment options; governance-heavy enterprise controls.[^70][^71][^72]                                                                                                                                                                                                                                                                                                                                                                                                                                               | IDE extension + on-prem server                       | Free tier + paid tiers   | [tabnine.com](https://www.tabnine.com)                                                                                   |
| 25  | **Sweep AI**                                  | Agentic Git Bot + IDE Plugin         | Converts labeled issues into pull requests; code search; GitHub-first workflow; plugin support.[^73][^74][^75]                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | GitHub App + IDE plugin                              | Free tier + paid tiers   | [sweep.dev](https://sweep.dev)                                                                                           |

---

## How the Categories Relate

Understanding where each tool sits in the workflow helps select the right combination:

```text
Idea / Product Brief
       ↓
[Methodology] SDD / MOD-W / BMAD  ←→  defines workflow structure, governance, roles, and review discipline
       ↓
[SDD Tool / Spec Framework] Spec Kit / OpenSpec / Kiro / Tessl  ←→  structures specs, changes, plans, tasks, and implementation context
       ↓
[Agentic IDE] Cursor / Claude Code / Windsurf / Copilot / Gemini Code Assist  ←→  implements task-by-task across the codebase
       ↓
[Autonomous Agent] Devin / Codex / Replit  ←→  handles full-session, unattended work
       ↓
[App Builder] Lovable / Bolt / v0  ←→  rapid full-stack prototyping
```

A mature team might use **MOD-W** as the governance methodology, **OpenSpec** or **Spec Kit** for structuring requirements and change proposals, **Cursor** or **Claude Code** for implementation, and **Devin** or **Codex** for parallelized unattended execution of well-scoped tasks.[^9][^12][^81][^82]

---

## Methodology / Framework Comparison: SDD vs. MOD-W vs. BMAD vs. OpenSpec

These four approaches are related, but they serve different team profiles and priorities:

| Dimension             | SDD                                         | MOD-W                                                                     | BMAD                                                   | OpenSpec                                                                                          |
| --------------------- | ------------------------------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------ | ------------------------------------------------------------------------------------------------- |
| **Primary focus**     | Spec-as-source-of-truth                     | Quality, traceability, human governance                                   | Agile velocity with AI agents                          | Lightweight, portable spec workflow for AI coding assistants                                      |
| **Type**              | Methodology / philosophy                    | Moderated workflow methodology                                            | Multi-agent methodology                                | Spec-driven framework / tooling layer                                                             |
| **Role structure**    | None defined                                | 4 roles + human Moderator                                                 | 8 AI agent roles + human                               | No required role model                                                                            |
| **Model diversity**   | Not prescribed                              | Core design principle                                                     | Team choice                                            | Tool-agnostic; not prescribed                                                                     |
| **Human-in-the-loop** | At phase gates                              | At every explicit quality gate                                            | Lighter-touch oversight                                | Human-guided, but less ceremonial                                                                 |
| **Workflow style**    | Usually phased                              | Moderated step lifecycle                                                  | Agile planning-to-delivery pipeline                    | Fluid, iterative, non-rigid                                                                       |
| **Artifact set**      | Spec, Plan, Tasks                           | PRODUCT, ARCHITECTURE, ROADMAP, STEP, REVIEW, QA, DOMAIN_LANGUAGE, AGENTS | PRD, Architecture, Stories, QA artifacts               | `openspec/specs/` plus per-change proposal, design, tasks, and spec deltas in `openspec/changes/` |
| **Best for**          | Any team adopting spec-first AI development | Teams prioritizing maintainability and governance                         | Teams prioritizing throughput with role specialization | Teams wanting a portable, low-ceremony, brownfield-friendly SDD workflow                          |
| **Tool integrations** | Many                                        | Kiro, Spec Kit, role-model pairings                                       | Cursor, Claude Code, others                            | Many supported assistants via generated commands and skills                                       |
| **License**           | N/A                                         | Open Source                                                               | Open Source                                            | Open Source                                                                                       |

OpenSpec’s official docs make two things especially clear: it separates current truth from proposed change by storing them in different directory trees, and it explicitly supports revising artifacts during the work rather than forcing a rigid one-way phase sequence.[^83][^84][^85][^86]

---

## OpenSpec vs. Spec Kit vs. MOD-W in practical terms

These three are related, but they operate at different layers:

| Dimension            | GitHub Spec Kit                      | OpenSpec                                                        | MOD-W                                                                  |
| -------------------- | ------------------------------------ | --------------------------------------------------------------- | ---------------------------------------------------------------------- |
| **Core nature**      | SDD scaffolding workflow             | Portable repository-local spec framework                        | Governance and moderation workflow                                     |
| **Default motion**   | Specify → Plan → Tasks → Implement   | Propose / Explore / Apply / Archive                             | Moderator-led step lifecycle                                           |
| **Rigidity**         | More phase-shaped                    | More fluid                                                      | More governed                                                          |
| **Primary strength** | Clear phase scaffolding              | Flexible change-centric spec management                         | Human-reviewed cross-validation                                        |
| **Role model**       | Minimal                              | Minimal                                                         | Explicit role separation                                               |
| **Best fit**         | Teams wanting guided spec-first flow | Teams wanting flexible, tool-agnostic, change-folder-driven SDD | Teams wanting strong HITL discipline and model-diverse quality control |

A practical way to think about them is:

- **SDD** is the broad philosophy.
- **Spec Kit** is a guided implementation of that philosophy.
- **OpenSpec** is a lightweight, flexible spec framework that lives directly in the repo.
- **MOD-W** is a moderation and governance layer that can wrap spec-first tooling.[^8][^9][^12][^81]

---

## Key Differentiators by Use Case

| Use Case                          | Best Fit Tools                                         |
| --------------------------------- | ------------------------------------------------------ |
| Solo developer, rapid MVP         | Bolt.new, Lovable, Replit Agent, Cursor                |
| Spec-first, team discipline       | Kiro, GitHub Spec Kit, OpenSpec, MOD-W, BMAD           |
| Quality & traceability focus      | MOD-W + OpenSpec, MOD-W + Spec Kit, MOD-W + Kiro       |
| Brownfield change management      | OpenSpec, Claude Code, Cursor, Aider                   |
| Enterprise compliance & privacy   | Tabnine, Amazon Q Developer, GitHub Copilot Enterprise |
| Full autonomy, long-running tasks | Devin, OpenAI Codex, Claude Code (headless)            |
| AWS-native projects               | Amazon Q Developer, Kiro                               |
| GCP / Firebase projects           | Gemini Code Assist, Firebase Studio                    |
| Open-source / self-hosted         | Aider, Continue.dev, BMAD, MOD-W, OpenSpec, Sweep AI   |
| UI-first generation               | Vercel v0, Lovable                                     |
| JetBrains ecosystem               | Sweep AI, Windsurf plugin, Continue.dev, Tabnine       |

OpenSpec fits naturally in both the “spec-first” and the “brownfield change management” rows because its current model is centered on keeping stable specs separate from proposed change folders until those changes are reviewed and archived.[^83][^84][^85]

---

## Emerging Trends to Watch (2026)

**Spec-as-source is gaining traction.** Tessl’s approach — where the spec file is the primary artifact and code is a generated byproduct — represents one far-reaching extension of SDD. OpenSpec reflects the same broad trend through its explicit `specs/` source-of-truth model and separate `changes/` structure, while MOD-W aligns with it by emphasizing artifact-first discipline and human review.[^7][^9][^16][^17][^83][^84]

**Multi-model cross-validation as a quality pattern.** MOD-W’s core insight — deliberately assigning different AI models to different roles so their biases cross-check one another — is a pattern likely to spread as teams mature beyond single-model pipelines.[^9]

**Fluid artifact evolution is replacing rigid one-pass workflows.** OpenSpec explicitly presents OPSX as a fluid, iterative workflow in which commands are actions you can take when needed, not phases you are forced through in lockstep.[^84][^86]

**MCP and tool portability are becoming standard expectations.** Teams increasingly expect the same underlying workflow to work across multiple assistants and environments rather than being locked to a single IDE or vendor.[^26][^36][^78][^83]

**Repository-local spec layers are becoming more important.** Instead of keeping intent in transient chat history, teams are moving toward storing working agreements, change proposals, task decomposition, and behavioral specs directly in versioned project directories.[^7][^80][^82][^83]

**Agent orchestration dashboards are becoming first-class workflow primitives.** Antigravity’s manager-view concept and Cursor’s Mission Control both push toward multi-agent coordination as a native operating mode rather than a workaround.[^20][^38][^39]

---

## Bottom-line Positioning

A useful mental model for the 2026 landscape is:

- **SDD** defines the philosophy.
- **OpenSpec**, **Spec Kit**, **Kiro**, and **Tessl** operationalize spec-first work in different ways.
- **MOD-W** adds governance, role separation, and HITL moderation on top of spec-driven development.
- **Cursor**, **Claude Code**, **Copilot**, **Gemini Code Assist**, and similar tools execute the implementation layer.
- **Codex**, **Devin**, and **Replit Agent** push further toward unattended autonomy.
- **Lovable**, **Bolt**, and **v0** optimize for rapid generation and product prototyping.

Within that map, **OpenSpec** sits between pure SDD philosophy and productized spec tools: lighter than Kiro, less phase-rigid than Spec Kit, and less governance-heavy than MOD-W.[^9][^12][^81][^82][^84]

---

## References

[^1]: [Goldman Sachs autonomous coder pilot marks major AI milestone](https://www.cnbc.com/2025/07/11/goldman-sachs-autonomous-coder-pilot-marks-major-ai-milestone.html)

[^2]: [Devin's 2025 Performance Review: Learnings From 18 Months](https://cognition.ai/blog/devin-annual-performance-review-2025)

[^3]: [Enabling Claude Code to work more autonomously](https://www.anthropic.com/news/enabling-claude-code-to-work-more-autonomously)

[^4]: [Amazon targets vibe-coding chaos with new Kiro AI software development tool](https://www.geekwire.com/2025/amazon-targets-vibe-coding-chaos-with-new-kiro-ai-software-development-tool/)

[^5]: [What is the BMAD Method? A Simple Guide to AI-Driven Development](https://devlabs.angelhack.com/blog/bmad-method/)

[^6]: [What is Spec-Driven Development (SDD) and How to Implement It?](https://apidog.com/blog/spec-driven-development-sdd/)

[^7]: [From Code to Contract in the Age of AI Coding Assistants](https://arxiv.org/html/2602.00180v1)

[^8]: [Spec-driven development - Wikipedia](https://en.wikipedia.org/wiki/Spec-driven_development)

[^9]: [Moderated AI Development Workflow (MOD-W) README](https://github.com/fpmcguire/moderated-ai-development-workflow/blob/main/README.md)

[^10]: [The BMAD Method: A Framework for Spec Oriented AI-Driven Development](https://recruit.group.gmo/engineer/jisedai/blog/the-bmad-method-a-framework-for-spec-oriented-ai-driven-development/)

[^11]: [BMAD-METHOD getting started](https://github.com/bmad-code-org/BMAD-METHOD/blob/main/docs/tutorials/getting-started.md)

[^12]: [Diving Into Spec-Driven Development With GitHub Spec Kit](https://developer.microsoft.com/blog/spec-driven-development-spec-kit)

[^13]: [AWS puts Kiro and other AI agents to work on truly autonomous software development](https://siliconangle.com/2025/12/02/aws-puts-ai-agents-work-truly-autonomous-software-development/)

[^14]: [Accelerate Amazon Connect AI agent development with Kiro](https://aws.amazon.com/blogs/contact-center/accelerate-amazon-connect-ai-agent-development-with-kiro/)

[^15]: [Kiro FAQ](https://kiro.dev/faq/)

[^16]: [Tessl launches spec-driven development tools for reliable AI coding](https://tessl.io/blog/tessl-launches-spec-driven-framework-and-registry/)

[^17]: [Tessl](https://www.tessl.io)

[^18]: [Understanding Spec-Driven Development: Kiro, Spec Kit, Tessl](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html)

[^19]: [Cursor AI: A Comprehensive 2026 Review](https://createaiagent.net/tools/cursor/)

[^20]: [Cursor IDE in 2026: What It Is, How It Works, and Who It's For](https://techjacksolutions.com/ai/ai-development/cursor-ide-what-it-is/)

[^21]: [Cursor AI Review 2026: Honest Verdict After Daily Use](https://www.nxcode.io/resources/news/cursor-review-2026)

[^22]: [Cursor](https://cursor.com)

[^23]: [Claude Code](https://claude.ai/code)

[^24]: [Claude Code Agent Architecture](https://www.zenml.io/llmops-database/claude-code-agent-architecture-single-threaded-master-loop-for-autonomous-coding)

[^25]: [GitHub Copilot Introduces Agent Mode and Next Edit Suggestions](https://github.com/newsroom/press-releases/agent-mode)

[^26]: [Agent mode 101: All about GitHub Copilot's powerful mode](https://github.blog/ai-and-ml/github-copilot/agent-mode-101-all-about-github-copilots-powerful-mode/)

[^27]: [GitHub Copilot Evolves - Agent Mode](https://devops.com/github-copilot-evolves-agent-mode-and-multi-model-support-transform-devops-workflows-2/)

[^28]: [Windsurf review 2025](<https://skywork.ai/skypage/en/Windsurf-(Formerly-Codeium)-Review-2025:-The-Agentic-IDE-Changing-the-Game/1973911680657846272>)

[^29]: [Windsurf review 2026](https://pinklime.io/blog/windsurf-codeium-review-2026)

[^30]: [Windsurf: The Enterprise AI IDE](https://www.latent.space/p/windsurf)

[^31]: [Amazon Q Developer announces a new agentic coding experience in the IDE](https://aws.amazon.com/about-aws/whats-new/2025/05/amazon-q-developer-agentic-coding-experience-ide/)

[^32]: [Amazon Q Developer](https://aws.amazon.com/q/developer/)

[^33]: [AWS re:Invent 2025 Announces Amazon Q Developer](https://www.cloudthat.com/resources/blog/aws-reinvent-2025-announces-amazon-q-developer-transforms-cloud-development/)

[^34]: [Gemini Code Assist updates July 2025](https://blog.google/innovation-and-ai/technology/developers-tools/gemini-code-assist-updates-july-2025/)

[^35]: [Gemini Code Assist updates from Google I/O 2025](https://blog.google/innovation-and-ai/technology/developers-tools/gemini-code-assist-updates-google-io-2025/)

[^36]: [Google Gemini Code Assist Agent Mode: Complete 2025 Guide](https://www.digitalapplied.com/blog/google-gemini-code-assist-agent-mode-guide)

[^37]: [Gemini Code Assist overview](https://developers.google.com/gemini-code-assist/docs/overview)

[^38]: [Google Antigravity - Wikipedia](https://en.wikipedia.org/wiki/Google_Antigravity)

[^39]: [Build with Google Antigravity, our new agentic development platform](https://developers.googleblog.com/build-with-google-antigravity-our-new-agentic-development-platform/)

[^40]: [AI Coding Tools in 2026 - A Complete List and Comparison](https://blogs.emorphis.com/ai-coding-tools-comparison-guide/)

[^41]: [Google Antigravity](https://antigravity.google)

[^42]: [OpenAI Codex App: A Guide to Multi-Agent AI Coding](https://intuitionlabs.ai/articles/openai-codex-app-ai-coding-agents)

[^43]: [OpenAI for Developers in 2025](https://developers.openai.com/blog/openai-for-developers-2025/)

[^44]: [OpenAI Codex for developers in VS Code, terminal, and CI/CD](https://www.heise.de/news/OpenAI-Codex-fuer-Entwickler-Coding-Agenten-in-VS-Code-Terminal-und-CI-CD-11212049.html)

[^45]: [Cognition AI – Devin, your Autonomous Software Engineer](https://stepmark.ai/2025/01/08/company-spotlight-cognition-ai-devin-your-autonomous-software-engineer/)

[^46]: [Devin AI - Wikipedia](https://en.wikipedia.org/wiki/Devin_AI)

[^47]: [Replit Agent 4: Replit Just Changed Everything](https://atalupadhyay.wordpress.com/2026/03/19/replit-agent-4-replit-just-changed-everything/)

[^48]: [Replit Review 2026: Complete AI Development Platform Test](https://hackceleration.com/replit-review/)

[^49]: [Replit Review 2026: Agent 3, $3B Valuation](https://www.taskade.com/blog/replit-review)

[^50]: [Best AI Coding Assistants 2026: Tools for Developers](https://replit.com/discover/best-ai-coding-assistant)

[^51]: [Bolt.new AI: The Full-Stack App Builder That Codes Itself](https://mindlabssys.com/blog/decoding-bolt-new-the-ai-that-builds-your-full-stack-app-while-you-watch/)

[^52]: [Bolt.new AI Builder: 2026 Review of Features, Pricing, and Alternatives](https://www.banani.co/blog/bolt-new-ai-review-and-alternatives)

[^53]: [Bolt.new AI Walkthrough: Pricing, Features, and Alternatives](https://uxpilot.ai/blogs/bolt-new-ai)

[^54]: [Vercel's v0 AI: The Easiest Way to Build Web Apps](https://habr.com/en/articles/863844/)

[^55]: [Vercel v0 and the future of AI-powered UI generation](https://blog.logrocket.com/vercel-v0-ai-powered-ui-generation/)

[^56]: [AI UI Generator: How Businesses Can Leverage Vercel's v0](https://www.baytechconsulting.com/blog/ai-ui-generator-how-businesses-can-leverage-vercels-v0-dev)

[^57]: [Vercel v0](https://dev.to/philip_zhang_854092d88473/vercel-v0-harnessing-ai-for-faster-smarter-ui-creation-29dk)

[^58]: [Lovable AI Review](https://trickle.so/blog/lovable-ai-review)

[^59]: [The Complete Guide to Building Apps with AI (2026)](https://muz.li/blog/lovable-for-designers-the-complete-guide-to-building-apps-with-ai-2026/)

[^60]: [What is Lovable AI?](https://uibakery.io/blog/what-is-lovable-ai)

[^61]: [Google IDX / Firebase Studio guide](https://www.ruh.ai/blogs/google-idx-firebase-studio-guide)

[^62]: [Project IDX is now part of Firebase Studio](https://firebase.google.com/docs/studio/idx-is-firebase-studio)

[^63]: [Aider Review — AI Pair Programming in Your Terminal](https://www.goodvibecode.com/tools/aider)

[^64]: [Open-Source AI Software Craft - Aider](https://oss-ai-swe.org/aider/)

[^65]: [Aider](https://aider.chat)

[^66]: [Continue.dev: Open-Source AI Code Agent Guide](https://betterstack.com/community/guides/ai/continue-dev-ai/)

[^67]: [Introducing the AI-powered programming tool - Continue.dev](https://2coffee.dev/en/articles/introducing-the-ai-powered-programming-tool-continue-dev)

[^68]: [Continue - open-source AI code agent](https://marketplace.visualstudio.com/items?itemName=Continue.continue)

[^69]: [Continue.dev](https://continue.dev)

[^70]: [Tabnine](https://www.tabnine.com)

[^71]: [Tabnine overview](https://www.eesel.ai/blog/tabnine-overview)

[^72]: [Tabnine at NVIDIA GTC 2025](https://www.tabnine.com/blog/nvidia-gtc-2025-recap/)

[^73]: [Sweep: AI-Powered Tool in 2026](https://altern.ai/tool/sweep)

[^74]: [Sweep AI Deep Dive](https://skywork.ai/skypage/en/sweep-ai-development-guide/1976898964182593536)

[^75]: [Sweep AI GitHub](https://github.com/sweepai)

[^76]: [Can Software Engineering Agents Self-Evolve on the Fly?](https://arxiv.org/abs/2511.13646)

[^77]: [Live-SWE-agent: Can Software Engineering Agents Self-Evolve on the Fly?](https://www.youtube.com/watch?v=zlSpQvLfPuI)

[^78]: [Claude Code: KI-Coding-Assistent von Anthropic im Detail](https://www.mindtwo.de/blog/claude-code-ai-coding-assistent)

[^79]: [Top AI Coding Tools for Developers & Businesses in 2026](https://www.mol-tech.us/blog/top-ai-coding-tools-businesses-2026)

[^80]: [How Spec-Driven Development Brings Structure to AI-Assisted Software Engineering](https://xbsoftware.com/blog/spec-driven-development-ai-assisted-software-engineering/)

[^81]: [OpenSpec repository](https://github.com/Fission-AI/OpenSpec)

[^82]: [OpenSpec getting started](https://github.com/Fission-AI/OpenSpec/blob/main/docs/getting-started.md)

[^83]: [OpenSpec supported tools](https://github.com/Fission-AI/OpenSpec/blob/main/docs/supported-tools.md)

[^84]: [OpenSpec concepts](https://github.com/Fission-AI/OpenSpec/blob/main/docs/concepts.md)

[^85]: [OpenSpec OPSX workflow](https://github.com/Fission-AI/OpenSpec/blob/main/docs/opsx.md)

[^86]: [OpenSpec workflows](https://github.com/Fission-AI/OpenSpec/blob/main/docs/workflows.md)

---

MOD-W v3.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
