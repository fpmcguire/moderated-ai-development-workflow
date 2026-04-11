# Quality Gates

Quality gates are explicit, non-negotiable checkpoints that AI-generated artifacts must pass before they are accepted. Gates are defined per step in [STEP.md](../templates/STEP.md) and evaluated in [REVIEW.md](../templates/REVIEW.md).

---

## Gate Levels

Moderated AI Development Workflow defines three levels of quality gate, applied according to the risk and complexity of the step.

### Level 1 — Baseline (all steps)

Every step must pass these criteria regardless of type:

- [ ] Output matches the scope defined in STEP.md
- [ ] Output uses domain language terms correctly (per [DOMAIN_LANGUAGE_MATRIX.md](../templates/DOMAIN_LANGUAGE_MATRIX.md))
- [ ] No hallucinated facts, APIs, libraries, or references
- [ ] No placeholders, TODOs, or stub implementations left unresolved
- [ ] No real credentials, personal data, or sensitive information included

### Level 2 — Code Quality (steps producing code)

In addition to Level 1:

- [ ] Code follows the project's established patterns and conventions (per ARCHITECTURE.md)
- [ ] All functions and classes are appropriately named using domain language
- [ ] Error handling is present and appropriate
- [ ] No obvious security vulnerabilities (e.g. injection, hardcoded secrets, unsafe deserialization)
- [ ] Code is testable — no hidden dependencies or untestable globals

### Level 3 — Completeness (steps producing a feature increment)

In addition to Levels 1 and 2:

- [ ] All acceptance criteria from STEP.md are met
- [ ] Unit tests are present and pass
- [ ] Integration with existing code does not break existing tests
- [ ] Documentation is updated if public interfaces changed

---

## Applying Gates

1. The Tech Lead specifies the gate level in STEP.md.
2. The Moderator evaluates each criterion in REVIEW.md.
3. Any failed criterion is documented with a reason.
4. A step may only be accepted if **all** criteria are met.

---

## Gate Waiver Policy

Quality gates **may not be waived**. If a gate criterion cannot be met, the team must:

1. Return the step to In Progress and retry with a refined prompt, **or**
2. Revise the acceptance criteria in STEP.md (requires Product Owner approval), **or**
3. Split the step into smaller steps that can each fully meet their gate criteria.

Bypassing a gate — even under time pressure — introduces unverified AI output into the product and violates the [Moderated AI Development Workflow Principles](principles.md).

---

MOD-W v2.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
