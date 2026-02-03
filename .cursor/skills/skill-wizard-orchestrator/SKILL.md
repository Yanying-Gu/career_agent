---
name: skill-wizard-orchestrator
description: "Comprehensive orchestrator for creating, refactoring, and packaging Cursor skills. Triggers when the user expresses intent to: (1) create a new skill, (2) update/refine an existing skill, (3) refactor instructions for token efficiency, or (4) package a skill for distribution. Follows the custom runbook protocol and utilizes the skill-creator toolkit."
---

# Skill Wizard Orchestrator

Guide the user through the skill development lifecycle using the custom runbook and the `skill-creator` toolkit.

## Operating Protocol

1.  **Source of Truth**: Read and strictly adhere to the phases defined in `references/skill-creation-guide.md`.
2.  **Toolkit**: Execute the scripts in `career_agent/.cursor/skills/skill-creator/scripts/` for deterministic tasks.
3.  **Sequential Interaction**: Walk the user through each phase. Confirm completion of the current phase before proposing the next.
4.  **Imperative Actions**: Provide clear instructions and execute commands using the imperative mood.
