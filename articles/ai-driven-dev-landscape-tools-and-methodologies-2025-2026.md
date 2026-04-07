# AI-Assisted & Automated Product and Code Production Workflow s

## Tools, Agents, and Methodologies — March 2026 Reference

---

## Overview

The landscape of AI-driven software development has undergone a step-change since 2024. What began as IDE autocompletion has rapidly evolved into a spectrum spanning **spec-driven methodologies** (where human-authored specifications become the source of truth for AI-generated code), **agentic IDEs** (full development environments where AI autonomously plans, edits, tests, and deploys across multiple files), **autonomous coding agents** (cloud-hosted workers that operate independently on tasks for hours or days), and **no-code/low-code AI builders** (platforms that generate full-stack apps from a single natural-language prompt). Teams at Goldman Sachs, Anthropic, and Amazon have all reported deploying AI agents that handle substantial portions of their software development lifecycle.[^1][^2][^3]

The underlying paradigm shift is the move from **"vibe coding"** (ad-hoc, prompt-and-pray) to **"viable coding"** — structured, spec-anchored workflows where AI is a disciplined participant rather than an ad-hoc assistant. This report organizes the landscape into four categories and provides a comprehensive reference table.[^4][^5]

---

## The Four Layers of AI-Driven Development

### 1. Methodologies & Frameworks

Structured approaches that define _how_ humans and AI collaborate — covering workflow phases, artifact standards, and role definitions. These are tool-agnostic processes.

### 2. Spec-Driven Development (SDD) Tools

Tools built specifically to operationalize the spec-first philosophy — turning requirements into structured specs, plans, tasks, and finally generated code with human gates at each phase.

### 3. Agentic IDEs & Coding Assistants

Full-featured development environments or extensions where an AI agent can autonomously read files, edit code across a repository, run terminal commands, and iterate on results — with the human reviewing diffs rather than writing every line.

### 4. AI App Builders & Autonomous Agents

Cloud-hosted agents and browser-based platforms that take a high-level prompt (or spec) and produce a deployable full-stack application or execute a complete engineering task end-to-end.

---

## Comprehensive Reference Table

| #   | Tool / Methodology                            | Category                       | Key Features                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Surface / Delivery                                                                         | Pricing (Mar 2026)                                                      | URL                                                                                                                      |
| --- | --------------------------------------------- | ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| 1   | **SDD (Spec-Driven Development)**             | Methodology                    | 4-phase lifecycle: Specify → Plan → Task → Implement; spec-as-source-of-truth; human review gates; eliminates "vibe coding" chaos; reduces mid-sprint pivots by ~40%[^6]; parallel agent execution on non-overlapping tasks[^7]                                                                                                                                                                                                                                                                                                                                           | Framework (tool-agnostic)                                                                  | Free (methodology)                                                      | [Wikipedia](https://en.wikipedia.org/wiki/Spec-driven_development)[^8]                                                   |
| 2   | **Moderated AI Development Workflow (MOD-W)** | Methodology                    | Role-based SDD workflow with 4 roles: Product Owner (Perplexity), Tech Lead (ChatGPT), Dev Team (Claude), and human Moderator; intentional multi-model diversity as a cross-validation quality mechanism; 8-step Step lifecycle with explicit human quality gates at every phase; artifact-driven (PRODUCT.md, ARCHITECTURE.md, ROADMAP.md, STEP.md, REVIEW.md, QA.md, DOMAIN_LANGUAGE_MATRIX.md, AGENTS.md); native integration profiles for Kiro and GitHub Spec Kit; optimizes for maintainability and traceability over raw speed; prompt packs per role included[^9] | Framework (tool-agnostic) + templates + prompt packs                                       | Free / Open Source (consulting available)                               | [github.com/fpmcguire/moderated-ai-development-workflow](https://github.com/fpmcguire/moderated-ai-development-workflow) |
| 3   | **BMAD Method**                               | Methodology                    | "Breakthrough Method for Agile AI-Driven Development"; 2-phase (Agentic Planning + Context-Engineered Dev); 8 role-based AI agents (Analyst, PM, Architect, Scrum Master, PO, Developer, QA, Orchestrator); PRD → Architecture → Story → Code → QA pipeline; all artifacts versioned[^5][^10]                                                                                                                                                                                                                                                                             | Framework / CLI installer (`npx bmad-method install`) — works in Cursor, Claude Code, etc. | Free / Open Source                                                      | [github.com/bmad-code-org/BMAD-METHOD](https://github.com/bmad-code-org/BMAD-METHOD)[^11]                                |
| 4   | **GitHub Spec Kit**                           | SDD Tool                       | Open-source CLI + slash-command workflow; 4 commands: `/specify`, `/plan`, `/tasks`, `/implement`; bootstraps SDD scaffolding in any AI coding assistant; supports multiple Figma mock directions per spec; all artifacts committed to workspace[^12][^7]                                                                                                                                                                                                                                                                                                                 | CLI + workspace templates (VS Code, Claude Code, Cursor)                                   | Free / Open Source                                                      | [developer.microsoft.com](https://developer.microsoft.com/blog/spec-driven-development-spec-kit)[^12]                    |
| 5   | **Kiro**                                      | SDD Tool + Agentic IDE         | AWS-built spec-driven IDE; Requirements → Design Doc → Task List workflow; autonomous agent hooks (run on file save); MCP support; multimodal agent chat; persistent context across sessions; learns from PRs and feedback; CloudWatch log analysis; 4 pricing tiers; launched July 2025[^4][^13][^14]                                                                                                                                                                                                                                                                    | Desktop IDE (VS Code-based fork); macOS, Windows, Linux                                    | Free (50 credits/mo), Pro $20/mo, Pro+ $40/mo, Power $200/mo[^15]       | [kiro.dev](https://kiro.dev)                                                                                             |
| 6   | **Tessl**                                     | SDD Tool / Platform            | "Spec-as-source" paradigm — code is generated from specs, marked `// GENERATED FROM SPEC - DO NOT EDIT`; Tessl Framework (spec authoring + vibe-specs); Tessl Spec Registry with 10,000+ pre-built library specs; deterministic conformance tests; prevents API hallucinations[^16][^17][^18]                                                                                                                                                                                                                                                                             | SaaS platform + CLI (Framework in closed beta, Registry in open beta)                      | Freemium (registry free)                                                | [tessl.io](https://tessl.io)[^17]                                                                                        |
| 7   | **Cursor**                                    | Agentic IDE                    | VS Code fork rebuilt around AI; Composer mode for multi-file edits from a single prompt; autonomous Agent Mode (terminal, browser, subagents); Mission Control for parallel agent workflows; Tab predictive autocomplete (Supermaven-powered); Visual Editor for drag-and-drop UI edits; $1B ARR in 2025[^19][^20][^21]                                                                                                                                                                                                                                                   | Desktop IDE (standalone); macOS, Windows, Linux                                            | Free tier; Pro $20/mo; Business $40/mo                                  | [cursor.com](https://cursor.com)[^22]                                                                                    |
| 8   | **Claude Code**                               | Agentic Coding Agent           | Anthropic terminal agent; single-threaded master loop architecture; reads/writes files, runs bash, web search; subagents for parallel tasks; hooks for automation; checkpoints (rewind with `/rewind`); native VS Code + JetBrains extensions; MCP support (85% context savings); 95% of Claude Code's own codebase written by Claude Code[^23][^3][^24]                                                                                                                                                                                                                  | CLI (terminal); VS Code extension; JetBrains plugin                                        | Pay-per-token via Anthropic API; included in Claude Pro/Team/Enterprise | [claude.ai/code](https://claude.ai/code)[^23]                                                                            |
| 9   | **GitHub Copilot**                            | Agentic IDE Extension          | Most widely deployed AI coding assistant; Agent Mode (Feb 2025): multi-step, self-healing, error-fixing agentic loop; Next Edit Suggestions (tab to apply); Copilot Workspace (brainstorm → code); MCP support; multi-model (GPT, Claude, Gemini); Copilot for GitHub (code review agent)[^25][^26][^27]                                                                                                                                                                                                                                                                  | IDE Extension (VS Code, Visual Studio, JetBrains, Neovim, etc.)                            | Free tier (2k completions); Pro $10/mo; Business $19/user/mo            | [github.com/features/copilot](https://github.com/features/copilot)[^25]                                                  |
| 10  | **Windsurf (Codeium)**                        | Agentic IDE                    | VS Code fork by Codeium; Cascade agentic core — multi-file edits, terminal execution, iterative testing; Supercomplete (predicts next several edits); automatic RAG codebase indexing (no manual tagging); proprietary SWE-1.5 model (~950 tok/s); image-to-code; multi-model (Claude, GPT, Gemini, SWE-1.5)[^28][^29][^30]                                                                                                                                                                                                                                               | Desktop IDE (standalone) + VS Code/JetBrains plugin                                        | Free tier; Pro $15/mo                                                   | [windsurf.com](https://windsurf.com)[^29]                                                                                |
| 11  | **Amazon Q Developer**                        | Agentic IDE Extension          | AWS-native AI coding assistant (evolved from CodeWhisperer); agentic coding experience: autonomous feature implementation, refactoring, test writing, code reviews; multi-step task execution with transparent reasoning; AWS infrastructure code generation (CDK, CloudFormation, Terraform); highest SWE-Bench scores among major assistants[^31][^32][^33]                                                                                                                                                                                                             | IDE Extension (VS Code, JetBrains, Visual Studio, Eclipse); CLI                            | Free tier; Pro $19/user/mo                                              | [aws.amazon.com/q/developer](https://aws.amazon.com/q/developer)[^32]                                                    |
| 12  | **Gemini Code Assist**                        | Agentic IDE Extension          | Google's AI coding assistant; Agent Mode: autonomous multi-file planning and execution; 180K free completions/month (90× Copilot's free tier); MCP support (Oct 2025); codebase-aware via Gemini's large context window; GCP/Firebase/BigQuery deep integration; Gemini CLI for terminal workflows; powered by Gemini 2.5[^34][^35][^36]                                                                                                                                                                                                                                  | IDE Extension (VS Code, JetBrains); CLI                                                    | Free (180K completions/mo); Standard $19/user/mo; Enterprise negotiated | [cloud.google.com/gemini/code-assist](https://cloud.google.com/gemini/code-assist)[^37]                                  |
| 13  | **Google Antigravity**                        | Agentic IDE                    | Google's agent-first IDE announced Nov 2025 alongside Gemini 3; Editor view (VS Code-like) + Manager view (multi-agent orchestration dashboard); artifact-based verification (task lists, screenshots, browser recordings); Google Doc-style inline feedback on agent plans; knowledge base for agent learning; powered by Gemini 3.1 Pro + Claude + GPT[^38][^39][^40]                                                                                                                                                                                                   | Desktop IDE; macOS, Windows, Linux (public preview, free for individuals)                  | Free (public preview)                                                   | [antigravity.google](https://antigravity.google)[^41]                                                                    |
| 14  | **OpenAI Codex**                              | Autonomous Agent + Platform    | Multi-agent coding platform; GPT-5.3-Codex (most capable agentic model, Mar 2026); cloud-isolated sandboxes; parallel agent task execution; "Skills" system for reusable workflows; CLI + VS Code extension + desktop app + CI/CD integration; GitHub PR creation; context compaction for long-horizon work[^42][^43][^44]                                                                                                                                                                                                                                                | SaaS (web app + desktop app); CLI; VS Code extension; API                                  | Included in ChatGPT Plus/Pro; API pay-per-token                         | [platform.openai.com/codex](https://platform.openai.com/codex)[^42]                                                      |
| 15  | **Devin**                                     | Autonomous Agent               | First commercially deployed "AI software engineer" (Cognition AI); full-stack autonomous: plans, codes, debugs, tests, deploys; learns from PRs and human feedback; 4× faster at problem solving YoY; 67% PR merge rate (up from 34%)[^2]; best for clear-requirement tasks (4–8 hr junior engineer work); infinitely parallelizable[^45][^46]                                                                                                                                                                                                                            | SaaS (web interface + Slack integration)                                                   | Personal/Team/Enterprise tiers                                          | [devin.ai](https://devin.ai)[^45]                                                                                        |
| 16  | **Replit Agent**                              | AI App Builder / Cloud IDE     | Agent 4 (Mar 2026); 200-min autonomous sessions; self-healing loops (agent finds and fixes its own bugs); Design Mode, Fast Build Mode, Plan Mode; App Testing (browser-based); multi-language (50+); built-in PostgreSQL; Figma/Lovable import; real-time multiplayer collaboration; one-click deploy[^47][^48][^49]                                                                                                                                                                                                                                                     | SaaS / Browser-based cloud IDE                                                             | Free tier; Core $25/mo; Teams from $40/user/mo                          | [replit.com](https://replit.com)[^50]                                                                                    |
| 17  | **Bolt.new**                                  | AI App Builder                 | Full-stack generation from a single prompt (React + Tailwind + Node.js + PostgreSQL + Prisma ORM); powered by StackBlitz WebContainers (runs in-browser, zero setup); Claude AI agent for complex projects; iterative prompt refinement; full source code ownership; GitHub export; Figma import; image-to-app[^51][^52][^53]                                                                                                                                                                                                                                             | SaaS / Browser                                                                             | Free tier; Pro $20/mo; Teams $40/mo                                     | [bolt.new](https://bolt.new)[^52]                                                                                        |
| 18  | **Vercel v0**                                 | AI UI Builder                  | UI-focused code generation from text or image mockups; generates React + Tailwind CSS + shadcn/ui components; multiple variations per prompt; supports Vue, Svelte, HTML/CSS, MUI, Chakra; Figma integration; instant preview and iteration; one-click deploy to Vercel[^54][^55][^56]                                                                                                                                                                                                                                                                                    | SaaS / Browser                                                                             | Free tier; Pro $20/mo                                                   | [v0.dev](https://v0.dev)[^57]                                                                                            |
| 19  | **Lovable**                                   | AI App Builder                 | Full-stack AI builder ("superhuman full-stack engineer"); React + Tailwind + Vite frontend; Supabase backend (auth, PostgreSQL, storage); Plan Mode (review before build); Chat Mode + Agent Mode; Visual Edits (click to modify UI); Figma import; bidirectional GitHub sync; Stripe integration; Prompt Queue (50-prompt batch)[^58][^59][^60]                                                                                                                                                                                                                          | SaaS / Browser                                                                             | Free (5 msgs/day); Starter $25/mo; Pro $30/mo                           | [lovable.dev](https://lovable.dev)[^58]                                                                                  |
| 20  | **Firebase Studio (Project IDX)**             | Cloud IDE + AI Builder         | Google's cloud-based full-stack development environment; Gemini AI integration; browser-based Linux VM; supports Flutter, React, Angular, Vue, Next.js, Go, Python; Android/iOS emulation in-browser; real-time collaboration; rebranded from Project IDX 2024; agentic prototype-to-deploy workflow[^61][^62]                                                                                                                                                                                                                                                            | SaaS / Browser                                                                             | Free                                                                    | [firebase.studio](https://firebase.studio)[^62]                                                                          |
| 21  | **Aider**                                     | Agentic CLI Tool               | Open-source AI pair programmer in your terminal; git-native (auto-commits with descriptive messages); repository map for full codebase context; 100+ languages; 50+ LLMs (Claude, GPT, DeepSeek, local via Ollama); Architect Mode (plan then implement); voice coding; automated linting/testing[^63][^64][^65]                                                                                                                                                                                                                                                          | CLI / Terminal (open source, Apache 2.0)                                                   | Free (pay only LLM API costs)                                           | [aider.chat](https://aider.chat)[^65]                                                                                    |
| 22  | **Continue.dev**                              | IDE Extension (Open Source)    | Open-source AI code agent for VS Code and JetBrains; Chat, Autocomplete, Edit, and Agent modes; bring-your-own model (OpenAI, Anthropic, Gemini, local via Ollama); automatic workspace context gathering (no manual file tagging); diff-view for all AI edits; PR quality checks as custom agents; Apache 2.0[^66][^67][^68]                                                                                                                                                                                                                                             | IDE Extension (VS Code, JetBrains)                                                         | Free / Open Source                                                      | [continue.dev](https://continue.dev)[^69]                                                                                |
| 23  | **Tabnine**                                   | Enterprise AI Coding Assistant | Privacy-first enterprise focus; Enterprise Context Engine (learns org's architecture, standards, legacy systems); on-premise / VPC / air-gapped deployment options; zero data retention; IP indemnification; multi-model; governance/compliance-grade; 70+ languages; eliminates senior-engineer bottlenecks in code review[^70][^71][^72]                                                                                                                                                                                                                                | IDE Extension (VS Code, JetBrains, Eclipse, etc.); on-prem server                          | Starter free; Pro $39/mo; Enterprise custom                             | [tabnine.com](https://tabnine.com)[^70]                                                                                  |
| 24  | **Sweep AI**                                  | Agentic Git Bot + IDE Plugin   | AI junior developer for GitHub; converts "Sweep:" labeled issues into automated PRs; custom code search (lexical + vector); JetBrains plugin with next-edit autocomplete (unique feature); supports Python, JS/TS, Java, Go, C#, Rust, C++; hosted or self-hosted[^73][^74][^75]                                                                                                                                                                                                                                                                                          | GitHub App + JetBrains Plugin                                                              | Free tier; Pro $480/seat/yr                                             | [sweep.dev](https://sweep.dev)[^75]                                                                                      |

---

## How the Categories Relate

Understanding where each tool sits in the workflow helps select the right combination:

```
Idea / Product Brief
       ↓
[Methodology] SDD / Moderated AI Development Workflow (MOD-W) / BMAD  ←→  defines the workflow structure, roles, and governance
       ↓
[SDD Tool] Spec Kit / Kiro / Tessl  ←→  generates Spec → Plan → Tasks
       ↓
[Agentic IDE] Cursor / Claude Code / Windsurf  ←→  implements task-by-task
       ↓
[Autonomous Agent] Devin / Codex / Replit  ←→  handles full-session, unattended work
       ↓
[App Builder] Lovable / Bolt / v0  ←→  rapid full-stack prototyping
```

A mature team might use **Moderated AI Development Workflow (MOD-W)** as the governance methodology, **Kiro** or **Spec Kit** to generate specs, **Cursor** or **Claude Code** for implementation, and **Devin** or **OpenAI Codex** for parallelized, unattended execution of well-defined tickets.

---

## Methodology Comparison: SDD vs. Moderated AI Development Workflow (MOD-W) vs. BMAD

These three methodologies are related but serve different team profiles and priorities:

| Dimension             | SDD                     | Moderated AI Development Workflow (MOD-W)        | BMAD                                 |
| --------------------- | ----------------------- | ------------------------------------------------ | ------------------------------------ |
| **Primary focus**     | Spec-as-source-of-truth | Quality, traceability, human governance          | Agile velocity with AI agents        |
| **Role structure**    | None defined            | 4 roles, human Moderator required                | 8 AI agent roles + human             |
| **Model diversity**   | Not prescribed          | Core design principle (different model per role) | Single model or team's choice        |
| **Human-in-the-loop** | At phase gates          | At every quality gate (explicit HITL)            | Lighter-touch oversight              |
| **Automation level**  | Medium                  | Intentionally moderate                           | High                                 |
| **Artifact set**      | Spec, Plan, Tasks       | PRODUCT, ARCHITECTURE, ROADMAP, STEP, REVIEW, QA | PRD, Architecture, Stories           |
| **Best for**          | Any team adopting AI    | Teams prioritizing maintainability over speed    | Teams prioritizing delivery velocity |
| **Tool integrations** | Kiro, Spec Kit, Cursor  | Kiro, Spec Kit (governance wrapper)              | Cursor, Claude Code, any             |
| **License**           | N/A (concept)           | Open Source                                      | Open Source                          |

---

## Key Differentiators by Use Case

| Use Case                          | Best Fit Tools                                                                                           |
| --------------------------------- | -------------------------------------------------------------------------------------------------------- |
| Solo developer, rapid MVP         | Bolt.new, Lovable, Replit Agent, Cursor                                                                  |
| Spec-first, team discipline       | Kiro, GitHub Spec Kit, Moderated AI Development Workflow (MOD-W) , BMAD                                  |
| Quality & traceability focus      | Moderated AI Development Workflow (MOD-W) + Kiro or Moderated AI Development Workflow (MOD-W) + Spec Kit |
| Enterprise compliance & privacy   | Tabnine (on-prem), Amazon Q Developer, GitHub Copilot Enterprise                                         |
| Full autonomy, long-running tasks | Devin, OpenAI Codex, Claude Code (headless)                                                              |
| AWS-native projects               | Amazon Q Developer, Kiro                                                                                 |
| GCP / Firebase projects           | Gemini Code Assist, Firebase Studio                                                                      |
| Open-source / self-hosted         | Aider, Continue.dev, BMAD Method, Moderated AI Development Workflow (MOD-W), Sweep AI                    |
| UI-first generation               | Vercel v0, Lovable (Visual Edits mode)                                                                   |
| JetBrains ecosystem               | Sweep AI, Windsurf plugin, Continue.dev, Tabnine                                                         |

---

## Emerging Trends to Watch (2026)

**Spec-as-source is gaining traction.** Tessl's approach — where the spec file is the primary artifact and code is a generated byproduct — represents the furthest extension of SDD. Academic research confirms that human-refined specs reduce LLM-generated code errors by up to 50%. Moderated AI Development Workflow (MOD-W)'s artifact-first discipline aligns with this direction while keeping a human firmly in control of what gets accepted.[^7][^9]

**Multi-model cross-validation as a quality pattern.** Moderated AI Developmen (MOD-W)'s core insight — that deliberately assigning different AI models to different roles exploits their divergent biases for quality checking — is a pattern likely to spread. As organizations mature their AI-driven workflows, single-model pipelines will increasingly be seen as a risk rather than a simplification.

**Self-evolving agents.** Princeton's Live-SWE-agent (Nov 2025) demonstrated an agent that autonomously modifies its own scaffold and toolset during runtime, achieving a 77.4% solve rate on SWE-bench Verified without test-time scaling. This points toward agents that improve themselves task-by-task.[^76][^77]

**MCP (Model Context Protocol) as the integration standard.** Anthropic's MCP has been adopted by Gemini Code Assist (Oct 2025), GitHub Copilot, Kiro, and Claude Code as the standard way to connect agents to external tools, databases, and APIs — enabling truly composable agentic workflows.[^26][^78][^36]

**Agent orchestration dashboards.** Both Google Antigravity (Manager view) and Cursor (Mission Control) have introduced multi-agent parallel execution dashboards, treating concurrent agent sessions as a first-class workflow primitive.[^20][^38]

**Productivity benchmarks.** Development teams using AI-driven workflows report 20–40% faster delivery on well-scoped tasks. SDD specifically reduces overall delivery time by 12–15% by eliminating clarification loops and rewrites. Goldman Sachs projects 3–4× productivity enhancement with Devin.[^79][^80][^1]

---

## References

1. [Goldman Sachs autonomous coder pilot marks major AI ...](https://www.cnbc.com/2025/07/11/goldman-sachs-autonomous-coder-pilot-marks-major-ai-milestone.html) - Devin, an AI software developer, from a startup called Cognition Labs, which is valued at nearly $4 ...

2. [Devin's 2025 Performance Review: Learnings From 18 ...](https://cognition.ai/blog/devin-annual-performance-review-2025) - At this point, Devin's well past due for a performance review - just like any human engineer. How we...

3. [Anthropic's NEW Claude Code Review Agent (Full Open ...](https://www.youtube.com/watch?v=nItsfXwujjg) - They've replaced the human code reviewers with AI agents and they've just open sourced their tooling...

4. [Amazon targets vibe-coding chaos with new 'Kiro' AI ...](https://www.geekwire.com/2025/amazon-targets-vibe-coding-chaos-with-new-kiro-ai-software-development-tool/) - Amazon has launched Kiro, a new AI software development tool that uses autonomous agents to generate...

5. [What is the BMad Method? A Simple Guide to AI-Driven ...](https://devlabs.angelhack.com/blog/bmad-method/) - BMAD, the Breakthrough Method for Agile AI-Driven Development, turns AI from a one-off code helper i...

6. [What is Spec-Driven Development (SDD) and How to Implement It?](https://apidog.com/blog/spec-driven-development-sdd/) - Complete guide on Spec-Driven Development (SDD) covering specification-first workflow, core componen...

7. [From Code to Contract in the Age of AI Coding Assistants](https://arxiv.org/html/2602.00180v1) - What AI-assisted SDD tools add is assistance in generating code from those specs, accelerating the p...

8. [Spec-driven development - Wikipedia](https://en.wikipedia.org/wiki/Spec-driven_development)

9. [README.md](https://github.com/fpmcguire/moderated-ai-development-workflow/blob/main/README.md)

10. [The BMAD Method: A Framework for Spec Oriented AI- ...](https://recruit.group.gmo/engineer/jisedai/blog/the-bmad-method-a-framework-for-spec-oriented-ai-driven-development/) - The BMAD Method is a universal framework for AI agent-driven development. ... BMAD's unique approach...

11. [BMAD-METHOD/docs/tutorials/getting-started.md at main](https://github.com/bmad-code-org/BMAD-METHOD/blob/main/docs/tutorials/getting-started.md) - Breakthrough Method for Agile Ai Driven Development - BMAD-METHOD/docs/tutorials/getting-started.md ...

12. [Diving Into Spec-Driven Development With GitHub Spec Kit](https://developer.microsoft.com/blog/spec-driven-development-spec-kit) - GitHub Spec Kit brings a new approach to AI-based software development ... GitHub Spec Kit is our ap...

13. [AWS puts Kiro and other AI agents to work on truly ...](https://siliconangle.com/2025/12/02/aws-puts-ai-agents-work-truly-autonomous-software-development/) - UPDATED 11:00 EDT / DECEMBER 02 2025. AI. AWS puts Kiro and other AI agents to work on truly autonom...

14. [Accelerate Amazon Connect AI agent development with Kiro](https://aws.amazon.com/blogs/contact-center/accelerate-amazon-connect-ai-agent-development-with-kiro/) - Introduction Building Amazon Connect AI agents presents developers with a familiar challenge: tight ...

15. [Frequently Asked Questions - Kiro](https://kiro.dev/faq/) - Find answers to frequently asked questions about Kiro, including pricing, features, privacy, enterpr...

16. [Tessl launches spec-driven development tools for reliable ...](https://tessl.io/blog/tessl-launches-spec-driven-framework-and-registry/) - AI coding tools are unreliable. Tessl's answer is spec-driven development, capturing intent in struc...

17. [Code written by AI, powered by your specs | Tessl.io](https://www.tessl.io) - Tessl’s AI native development platform delivers secure, high-quality, and auto-maintained code — all...

18. [Understanding Spec-Driven-Development: Kiro, spec-kit ...](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html) - An effective SDD tool would at the very least have to provide flexibility for a few different core w...

19. [Cursor AI: A Comprehensive 2026 Review](https://createaiagent.net/tools/cursor/) - The major breakthrough of late 2025 was the Composer mode. This interface allows developers to descr...

20. [Cursor IDE in 2026: What It Is, How It Works, and Who It's For](https://techjacksolutions.com/ai/ai-development/cursor-ide-what-it-is/) - Cursor IDE is an AI-native code editor built on VS Code with autonomous agents and multi-file editin...

21. [Cursor AI Review 2026: Honest Verdict After Daily Use](https://www.nxcode.io/resources/news/cursor-review-2026) - Unlike GitHub Copilot (which adds AI to VS Code), Cursor rebuilt the editor around AI. Every feature...

22. [Cursor: The best way to code with AI](https://cursor.com) - It's a demonstration of Cursor's IDE showing AI-powered coding assistance features. The interface is...

23. [Enabling Claude Code to work more autonomously](https://www.anthropic.com/news/enabling-claude-code-to-work-more-autonomously) - Introducing Claude Code upgrades: native VS Code extension, terminal UX updates, and checkpoints for...

24. [Claude Code Agent Architecture: Single-Threaded Master ...](https://www.zenml.io/llmops-database/claude-code-agent-architecture-single-threaded-master-loop-for-autonomous-coding) - Anthropic's Claude Code represents a significant production deployment of LLM-based autonomous agent...

25. [GitHub Copilot Introduces Agent Mode and Next Edit ...](https://github.com/newsroom/press-releases/agent-mode) - GitHub Copilot Introduces Agent Mode and Next Edit Suggestions to Boost Productivity of Every Organi...

26. [Agent mode 101: All about GitHub Copilot's powerful mode](https://github.blog/ai-and-ml/github-copilot/agent-mode-101-all-about-github-copilots-powerful-mode/) - GitHub Copilot agent mode is an autonomous and agentic real-time, synchronous collaborator that perf...

27. [Best of 2025: GitHub Copilot Evolves - Agent Mode](https://devops.com/github-copilot-evolves-agent-mode-and-multi-model-support-transform-devops-workflows-2/) - GitHub Copilot adds Agent Mode with MCP support to all VS Code users, bringing agentic capabilities ...

28. [Windsurf (Formerly Codeium) Review 2025: The Agentic IDE ...](<https://skywork.ai/skypage/en/Windsurf-(Formerly-Codeium)-Review-2025:-The-Agentic-IDE-Changing-the-Game/1973911680657846272>) - Experience the future of coding with Windsurf, an evolved agentic IDE that enhances developer effici...

29. [Windsurf (Codeium) Review 2026: AI Coding Agent Worth Switching ...](https://pinklime.io/blog/windsurf-codeium-review-2026) - An honest, in-depth Windsurf review for 2026 — formerly Codeium. Features, Cascade agent, pricing, a...

30. [Windsurf: The Enterprise AI IDE - with Varun and Anshul of ...](https://www.latent.space/p/windsurf) - Future of Agentic Coding, building boring enterprise integrations, and growing to 1M users

31. [Amazon Q Developer announces a new agentic coding ...](https://aws.amazon.com/about-aws/whats-new/2025/05/amazon-q-developer-agentic-coding-experience-ide/) - The new experience redefines how you write, modify, and maintain code by leveraging natural language...

32. [Amazon Q Developer - code generation assistant](https://aws.amazon.com/q/developer/) - Amazon Q Developer helps you get the most from your data to easily build analytics, AI/ML, and gener...

33. [AWS re:Invent 2025 Announces Amazon Q Developer ...](https://www.cloudthat.com/resources/blog/aws-reinvent-2025-announces-amazon-q-developer-transforms-cloud-development/) - Key Capabilities Unveiled at re:Invent · Intelligent Code Generation and Optimization · Automated Cl...

34. [Gemini Code Assist's June 2025 updates: Agent Mode ...](https://blog.google/innovation-and-ai/technology/developers-tools/gemini-code-assist-updates-july-2025/) - The new agent mode acts as an AI pair programmer to analyze your entire codebase and implement new f...

35. [Gemini Code Assist: Updates from Google I/O 2025](https://blog.google/innovation-and-ai/technology/developers-tools/gemini-code-assist-updates-google-io-2025/) - Gemini Code Assist for individuals and for GitHub are now generally available and powered by Gemini ...

36. [Google Gemini Code Assist Agent Mode: Complete 2025 Guide](https://www.digitalapplied.com/blog/google-gemini-code-assist-agent-mode-guide) - The October 2025 update marks a significant architectural shift for Gemini Code Assist. Google is mi...

37. [Gemini Code Assist overview](https://developers.google.com/gemini-code-assist/docs/overview) - Gemini Code Assist offers AI-powered assistance to help your development team build, deploy, and ope...

38. [Google Antigravity - Wikipedia](https://en.wikipedia.org/wiki/Google_Antigravity)

39. [Build with Google Antigravity, our new agentic ...](https://developers.googleblog.com/build-with-google-antigravity-our-new-agentic-development-platform/) - Google Antigravity: The agentic development platform that lets agents autonomously plan, execute, an...

40. [AI Coding Tools in 2026 - A Complete List and Comparison ...](https://blogs.emorphis.com/ai-coding-tools-comparison-guide/) - Explore the top AI coding tools in 2026 with a comparison covering features, use cases, insights, an...

41. [Google Antigravity](https://antigravity.google) - Google Antigravity is built for user trust, whether you're a professional developer working in a lar...

42. [OpenAI Codex App: A Guide to Multi-Agent AI Coding | IntuitionLabs](https://intuitionlabs.ai/articles/openai-codex-app-ai-coding-agents) - An in-depth analysis of the OpenAI Codex app, a command center for AI coding agents. Learn how it en...

43. [OpenAI for Developers in 2025](https://developers.openai.com/blog/openai-for-developers-2025/) - The open-source Codex CLI (GitHub) brought agent-style coding directly into local environments, enab...

44. [OpenAI Codex für Entwickler – Coding-Agenten in VS ...](https://www.heise.de/news/OpenAI-Codex-fuer-Entwickler-Coding-Agenten-in-VS-Code-Terminal-und-CI-CD-11212049.html) - Die Agenten-Plattform unterstützt Entwicklerinnen und Entwickler dabei, ihre Entwicklungsprozesse zu...

45. [Cognition AI – Devin, your Autonomous Software Engineer](https://stepmark.ai/2025/01/08/company-spotlight-cognition-ai-devin-your-autonomous-software-engineer/) - Devin.ai is an autonomous artificial intelligence developed by Cognition AI to perform software engi...

46. [Devin AI](https://en.wikipedia.org/wiki/Devin_AI) - Devin AI is an artificial intelligence-powered software development tool created by Cognition Labs. ...

47. [Replit Agent 4: Replit Just Changed Everything | atal upadhyay](https://atalupadhyay.wordpress.com/2026/03/19/replit-agent-4-replit-just-changed-everything/) - An AI agent that can see and control your entire environment — code, database, deployment, design, d...

48. [Replit Review 2026: Complete AI Development Platform Test](https://hackceleration.com/replit-review/) - In-depth Replit test: Agent 3 autonomous AI coding, 50+ languages, cloud IDE, real-time collaboratio...

49. [Replit Review 2026: Agent 3, $3B Valuation (Pros & Cons)](https://www.taskade.com/blog/replit-review) - TL;DR: Replit ($25-100/mo) is a powerful cloud IDE with Agent 3 autonomous coding, valued at $3B. Bu...

50. [Best AI Coding Assistants 2026: Tools for Developers](https://replit.com/discover/best-ai-coding-assistant) - Best AI coding assistants of 2026 compared. See how tools like Replit, Cursor, and Copilot automate ...

51. [Bolt.new AI: The Full-Stack App Builder That Codes Itself](https://mindlabssys.com/blog/decoding-bolt-new-the-ai-that-builds-your-full-stack-app-while-you-watch/) - This is the core feature. Your only job is to describe the app you want – you don't need code words ...

52. [Bolt.new AI Builder: 2026 Review of Features, Pricing, and ...](https://www.banani.co/blog/bolt-new-ai-review-and-alternatives) - It accepts inputs as text, images, Figma files, and GitHub repositories, then scaffolds a full-stack...

53. [Bolt.new AI Walkthrough: Pricing, Features, and Alternatives](https://uxpilot.ai/blogs/bolt-new-ai) - Bolt.new is an AI-powered app builder that generates complete websites, web apps, and mobile apps fr...

54. [Vercel's V0 AI: The Easiest Way to Build Web Apps](https://habr.com/en/articles/863844/) - Code Generation from Mockups: You can upload design mockups, which V0 then translates into code. Fig...

55. [Vercel v0 and the future of AI-powered UI generation](https://blog.logrocket.com/vercel-v0-ai-powered-ui-generation/) - Vercel v0 is a powerful tool for rapidly prototyping various UI elements that generates code based o...

56. [AI UI Generator How Businesses Can Leverage Vercel's v0 ...](https://www.baytechconsulting.com/blog/ai-ui-generator-how-businesses-can-leverage-vercels-v0-dev) - It allows users to generate code for user interfaces through natural-language prompts. Whether you'r...

57. [Vercel v0: Harnessing AI for Faster, Smarter UI Creation](https://dev.to/philip_zhang_854092d88473/vercel-v0-harnessing-ai-for-faster-smarter-ui-creation-29dk) - Vercel v0 revolutionizes UI development by combining AI with human creativity. Its ability to genera...

58. [Lovable AI Review: The Good, Bad & Pricing Explained ...](https://trickle.so/blog/lovable-ai-review) - Lovable AI stands out with an impressive 4.7-star rating and claims to build apps 20 times faster th...

59. [The Complete Guide to Building Apps with AI (2026)](https://muz.li/blog/lovable-for-designers-the-complete-guide-to-building-apps-with-ai-2026/) - Lovable launched Figma Import in January 2025, built in partnership with Builder.io. It let you impo...

60. [What is Lovable AI? A Deep Dive into the Builder](https://uibakery.io/blog/what-is-lovable-ai) - Lovable AI is a full-stack AI application development platform that generates real, editable source ...

61. [Google IDX (Firebase Studio) Guide: Cloud Dev Environment](https://www.ruh.ai/blogs/google-idx-firebase-studio-guide) - Complete guide to Google IDX: the cloud-based, AI-powered dev environment. Learn features, setup, pr...

62. [Project IDX is now part of Firebase Studio - Google](https://firebase.google.com/docs/studio/idx-is-firebase-studio) - We're excited to announce that Project IDX is now part of Firebase Studio. Firebase Studio is an age...

63. [Aider Review — AI Pair Programming in Your Terminal](https://www.goodvibecode.com/tools/aider) - Aider is an open-source AI pair programming tool that works directly in your terminal. Created by Pa...

64. [Open-Source AI Software Craft - Aider](https://oss-ai-swe.org/aider/) - Aider is an AI-powered pair programmer that runs in your terminal. It allows you to code with a larg...

65. [Aider - AI Pair Programming in Your Terminal](https://aider.chat) - AI pair programming in your terminal. Aider lets you pair program with LLMs to start a new project o...

66. [Continue.dev: Open-Source AI Code Agent Guide](https://betterstack.com/community/guides/ai/continue-dev-ai/) - Learn how Continue.dev transforms your development workflow with AI-powered code reviews, full-proje...

67. [Introducing the AI-powered programming tool - Continue.dev](https://2coffee.dev/en/articles/introducing-the-ai-powered-programming-tool-continue-dev) - Continue.dev is a leading open-source AI coding assistant for developers. You can connect and use an...

68. [Continue - open-source AI code agent](https://marketplace.visualstudio.com/items?itemName=Continue.continue) - VS Code Agent. Agent to work on development tasks together with AI. agent. VS Code Chat. Chat to ask...

69. [Continue.dev](https://continue.dev) - Quality control for your software factory. Source-controlled AI checks on every pull request. Standa...

70. [Tabnine AI Code Assistant | Smarter AI Coding Agents. Total ...](https://www.tabnine.com) - Tabnine is the AI code assistant that accelerates and simplifies software development while keeping ...

71. [Tabnine overview: A deep dive into the AI coding assistant ...](https://www.eesel.ai/blog/tabnine-overview) - Get a complete Tabnine overview, exploring its key features, pricing, and how this AI coding assista...

72. [Tabnine at NVIDIA GTC 2025: Enterprise-Ready AI for ...](https://www.tabnine.com/blog/nvidia-gtc-2025-recap/) - Introducing Llama 3.3 and Qwen 2.5, plus a game-changing capability that lets you integrate any LLM ...

73. [Sweep: AI-Powered Tool in 2026 - Altern](https://altern.ai/tool/sweep) - Sweep is an intelligent open-source AI assistant that automates typical developer tasks by reading y...

74. [Sweep AI Deep Dive: Your Guide to the Future of AI- ...](https://skywork.ai/skypage/en/sweep-ai-development-guide/1976898964182593536) - Unlock the future of coding with Sweep AI, your AI Junior Developer! Automate coding tasks seamlessl...

75. [Sweep AI](https://github.com/sweepai) - Sweep: AI Autocomplete & Coding Agent Sweep is a world-class AI coding agent and autocomplete built ...

76. [Can Software Engineering Agents Self-Evolve on the Fly?](https://arxiv.org/abs/2511.13646) - by CS Xia · 2025 · Cited by 18 — In this paper, we propose Live-SWE-agent, the first live software a...

77. [Live-SWE-agent: Can Software Engineering Agents Self-Evolve on the Fly? (Nov 2025)](https://www.youtube.com/watch?v=zlSpQvLfPuI) - Title: Live-SWE-agent: Can Software Engineering Agents Self-Evolve on the Fly? (Nov 2025)
    Link: http...

78. [Claude Code: KI-Coding-Assistent von Anthropic im Detail](https://www.mindtwo.de/blog/claude-code-ai-coding-assistent) - Claude Code ist ein agentic Coding-Tool, das direkt in Ihrem Terminal läuft und von Anthropic entwic...

79. [Top AI Coding Tools for Developers & Businesses in 2026](https://www.mol-tech.us/blog/top-ai-coding-tools-businesses-2026) - AI-Powered Code Generation. Tools like Cursor, GitHub Copilot, and Claude Code generate code, refact...

80. [How Spec-Driven Development Brings Structure to AI- ...](https://xbsoftware.com/blog/spec-driven-development-ai-assisted-software-engineering/) - Discover how Spec-Driven Development helps teams manage AI code generation with clear specifications...

---

MOD-W v1.1.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
