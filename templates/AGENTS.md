This is placeholder content for the (Codex) AGENTS.md template. 
Please replace this with the actual content for the (Codex) AGENTS.md template that will be used by Tech Lead to generate 
the actual (Codex) AGENTS.md file.

Codex will be used as the agent for the Tech Lead role when reviewing the (Claude or Claude Code) Development Team's implementation of each step added to the project's local repository. 
This template should define the specific prompts, context, and guidelines for how Codex will review and generate code, tests, and documentation based on 
the PRODUCT.md, ARCHITECTURE.md, DOMAIN_LANGUAGE.md, ROADMAP.md, and STEP.md files.
The Tech Lead, using ChatGPT, will first generate the ARCHITECTURE.md and DOMAIN_LANGUAGE.md, and then generate the (Codex) AGENTS.md.
The Moderator will need to manually paste the relevant context from the above files into ARCHITECTURE.md, DOMAIN_LANGUAGE.md, andthe (Codex) AGENTS.md template
and place the completed AGENTS.md in the root of the repository.
Only after generating (Codex) AGENTS.md, the Tech Lead agent (Codex) will generate the ROADMAP.md and STEP.md files for each step in the roadmap, which will then be implemented by the Development Team agent (Claude).

This AGENTS.md template will be used to specify the exact instructions for the Codex AGENTS.md file, including:
   - The Tech Lead role and responsibilities for reviewing the Development Team's implementation of each step
   - Which files and context to provide as input
   - The expected files, format, and style of the output (ROADMAP.md, STEP.md, code files, test files, documentation)
   - Any specific conventions or patterns to follow in the generated code (templates)
   - How to handle edge cases or uncertainties in the implementation
   - The level of detail and explanation to include in the output (e.g. comments, rationale)