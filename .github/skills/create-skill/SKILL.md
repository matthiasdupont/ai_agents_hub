---
name: create-skill
description: "Create or refine a reusable agent skill. Use for a repeatable multi-step workflow that needs procedures, scripts, references, templates, or other bundled resources."
argument-hint: "Describe the workflow, triggers, inputs, outputs, and resources"
---

# Create Skill

Create one workspace skill under `.github/skills/<skill-name>/`.

## Procedure

1. Confirm the request is a repeatable workflow, not a permanent rule, persona,
   or one-step prompt.
2. Choose a lowercase kebab-case name and use it for both the folder and the
   frontmatter `name`.
3. Put discovery triggers, inputs, outputs, and the ordered procedure in
   `SKILL.md`.
4. Put executable automation in `scripts/`, detailed knowledge in
   `references/`, and reusable files in `assets/` only when needed.
5. Link resources from `SKILL.md` with relative `./` paths and keep references
   one level deep.
6. Include validation and failure-handling steps in the procedure.
7. Validate frontmatter, links, and scripts; then update
   `docs/architecture.md`.

## Required qualities

- The description says both what the skill does and when to use it.
- The workflow is self-contained and has an observable completion condition.
- `SKILL.md` stays below 500 lines; large details use progressive loading.
- Scripts are deterministic, non-interactive where possible, and documented.