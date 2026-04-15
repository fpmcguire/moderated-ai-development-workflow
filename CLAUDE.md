# CLAUDE.md

> Instructions for Claude Code working in the `moderated-ai-development-workflow` repository.
> This file is repository-specific and is intended to guide direct local edits.

## Purpose

This repository contains the MOD-W methodology itself: documentation, templates, prompts, examples, and supporting project files.

Use this file as the working agreement for editing this repository safely and consistently.

## Working Style

- Edit files directly when the requested change is clear.
- Keep changes minimal and scoped to the request.
- Preserve terminology and internal consistency across docs, templates, prompts, and examples.
- Do not make broad repo-wide rewrites unless explicitly asked.
- Do not rename or move canonical files unless explicitly asked.
- When a change has ripple effects, note the affected files.

## Source of Truth

When relevant, use these in order:

1. the user’s current request
2. canonical docs in `docs/`
3. root guidance files such as `CLAUDE.md` and `AGENTS.md`
4. templates in `templates/`
5. prompts in `prompts/`
6. examples and supporting files

If files conflict, preserve the current canon and highlight the inconsistency.

## What to Prioritize

Prioritize quality and consistency in:

- MOD-W terminology
- role definitions
- template correctness
- prompt correctness
- internal links and references
- naming consistency for canonical artifacts
- alignment between docs, templates, prompts, and examples

## Editing Rules

- Read only the files relevant to the task.
- Prefer small diffs over rewrites.
- Preserve useful existing content unless there is a clear reason to replace it.
- Keep Markdown clear, structured, and easy to scan.
- Keep copy/paste templates clean and practical.
- For template files, preserve placeholders intentionally.
- For project-specific files, remove template placeholders and make content concrete.

## When to Ask Before Editing

Ask before proceeding only when:

- the request is ambiguous
- multiple files conflict in a way that changes meaning
- the change would alter core methodology semantics
- the change implies a broad structural rewrite, rename, or move

Otherwise, make the edit directly.

## Output Expectations

After making changes, summarize:

- which files were changed
- what changed in each file
- any follow-up inconsistencies noticed but not changed

## Notes

This file is for working in the MOD-W repository itself.
It is not a project template and does not need to simulate MOD-W roles unless explicitly requested.
