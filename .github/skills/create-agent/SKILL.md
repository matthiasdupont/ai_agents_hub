---
name: create-agent
description: "Create or refine a focused VS Code custom agent. Use when adding an agent role, defining tool restrictions, delegation boundaries, or a structured subagent output."
argument-hint: "Describe the role, triggers, tools, constraints, and expected output"
---

# Create Agent

Create one workspace agent under `.github/agents/<name>.agent.md`.

## Procedure

1. Identify the single decision or responsibility owned by the agent.
2. Decide whether it is user-invocable, model-invocable, or both.
3. Select only the tool aliases required by that responsibility.
4. Write a discovery-oriented `description` containing concrete trigger terms.
5. Define its approach, explicit constraints, stopping condition, and output.
6. Check that its role does not duplicate an existing agent or belong in a
   repeatable skill instead.
7. Validate the YAML frontmatter and update `docs/architecture.md`.

## Required qualities

- One role per agent.
- No model pinning unless the role has a measured model requirement.
- Read-only roles must not receive edit or execute tools.
- Delegated outputs must separate evidence, conclusions, and unknowns.