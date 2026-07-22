# Prototype — {{PROJECT_NAME}}

**Status:** Research artifact. **Non-authoritative.**

---

This folder contains a clickable prototype produced by the **Designer + Prototyper** role (Claude Design) during the Project Kickoff Prototype Ceremony.

## What this is

A working demonstration that the design works under realistic conditions. The prototype simulates the product's primary workflows, demonstrates every screen in `DESIGN-SPEC.md` scope, and exists as evidence the design is buildable.

## What this is NOT

- **Not production code.** Do not import from this folder into `src/`.
- **Not architecturally canonical.** Patterns here are research output. The authoritative architecture lives in `mod-w/ARCHITECTURE.md`, authored by the Tech Lead.
- **Not a Reference Implementation by default.** A Reference Implementation status is granted only when the Tech Lead explicitly disposes of a specific prototype component in a `STEP-XX.md §"Reference Implementation"` block.

## How this folder is used downstream

1. The Tech Lead (Codex) reads this folder during Architecture Definition as one of the kickoff inputs.
2. The Tech Lead may reference specific files here in `STEP-XX.md` as a Reference Implementation with one of three dispositions: `Adopt as-is`, `Adopt with modifications`, or `Reject`.
3. The Development Team reads dispositions in `STEP-XX.md` and proceeds accordingly. The Dev Team does **not** read this folder directly.

## Lifecycle

- **Created:** During the Prototype Ceremony.
- **Frozen:** At the Architecture Handoff. Once `ARCHITECTURE.md` is approved, this folder is read-only.
- **Retained:** For the life of the project, as historical context.

---

MOD-W v4.0.0
