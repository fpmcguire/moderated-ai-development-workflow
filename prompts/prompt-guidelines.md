# MOD-W Prompting Guide: From "Vibe" to "Viable"

In the Moderated AI Development Workflow, prompting is a tool for structured thinking, decision support, review quality, and learning.

This guide helps the Moderator get clearer, more trustworthy output from each role.

---

## 1. Core Prompting Pattern

For non-trivial work, prefer a three-part request structure.

### A. Options and analysis

Ask for more than one viable path when the decision is meaningful.

Example requests:

- "Give me 3 implementation options: Minimal, Balanced, and Scalable."
- "Compare 2 roadmap slicing approaches and recommend one."
- "Show me the trade-offs before recommending a direction."

Use this when:

- architecture choices matter
- roadmap slicing is unclear
- the task has real trade-offs

Do not force multiple options for trivial edits.

### B. Impact and ramifications

Before approving a plan, understand the cost and risk.

Example requests:

- "For the recommended option, list technical debt risks, side effects, and likely future pain points."
- "What could this break?"
- "What hidden complexity am I accepting with this choice?"

Use this to surface:

- technical debt
- architectural drift
- coupling
- test gaps
- UX or workflow regressions

### C. The mentorship loop

Use the model to explain the reasoning behind the recommendation.

Example requests:

- "Explain why this pattern is a better fit than the alternative."
- "Teach this as if you are reviewing a junior engineer's plan."
- "What principle is driving this recommendation?"

Use this when:

- you want learning value
- you want to test whether the recommendation is well-reasoned
- you need stronger review transparency

---

## 2. Standard Answer Depths

MOD-W supports three standard answer depths.

| Depth       | Best for                                                    | Expected output                                          |
| ----------- | ----------------------------------------------------------- | -------------------------------------------------------- |
| **minimal** | small fixes, direct rewrites, straightforward reviews       | concise answer, one direct recommendation                |
| **options** | roadmap shaping, design choices, standard feature work      | 2–3 viable paths with trade-offs and recommendation      |
| **full**    | architecture, critical logic, teaching, high-risk decisions | detailed reasoning, explanation, and structured guidance |

### Suggested defaults

Use these defaults unless the Moderator wants something different:

- **Product Owner**: `options`
- **Tech Lead**: `options`
- **Development Team**:
  - `minimal` for implementation
  - `options` for planning
- **Review / critique passes**: `minimal`

---

## 3. Red-Team Review Prompt

Use this before approving a Step or implementation when you want a sharper critique.

Example:

> Analyze this implementation as a skeptical senior architect.  
> Find three reasons it might fail in production, drift from the intended architecture, or cause regressions.  
> Be specific and concrete.

This is useful for:

- pre-merge review
- risk discovery
- checking for blind spots
- strengthening Moderator confidence

---

## 4. Good Moderator Prompt Habits

- identify the role clearly
- provide only the relevant artifact excerpts
- name the active Step explicitly
- specify the desired answer depth when it matters
- ask for acceptance-check mapping during reviews
- ask for scope boundaries explicitly when shaping a Step

Good example:

> You are the Tech Lead.  
> Here are excerpts from `ARCHITECTURE.md`, `DOMAIN_LANGUAGE.md`, and `STEP-03.md`.  
> Answer at `options` depth.  
> Tell me whether this Step is too large, propose a tighter version if needed, and list the likely files affected.

---

## 5. Keep the Workflow Honest

Use prompts to reinforce MOD-W discipline:

- ask whether the Step is too large
- ask what is out of scope
- ask what could break
- ask how acceptance checks will be verified
- ask whether naming matches `DOMAIN_LANGUAGE.md`
- ask whether the implementation drifted from `PRODUCT.md` or `ARCHITECTURE.md`

These questions help the Moderator stay in control.

---

MOD-W v2.1.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
