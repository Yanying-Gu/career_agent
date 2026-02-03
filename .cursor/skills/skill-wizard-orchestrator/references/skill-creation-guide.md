# Skill Creation Runbook

- [Phase 1: Planning](#phase-1-planning)
- [Phase 2: Execution & Automation](#phase-2-execution--automation)
- [Phase 3: Design Principles](#phase-3-design-principles)

## Phase 1: Planning
*   Define Purpose: Identify the specific task the AI is repeating or struggling with.
*   Identify Resources: 
    *   Scripts: For fragile or deterministic tasks (e.g., `data_cleaning.py`).
    *   References: For large documentation or static data (e.g., `schema_definitions.md`).
    *   Assets: For output templates (e.g., `report_boilerplate.html`).

## Phase 2: Execution & Automation

### 1. Initialize
*   Manual CLI: `python career_agent/.cursor/skills/skill-creator/scripts/init_skill.py <name> --path career_agent/.cursor/skills/`
*   Agent Prompt: "Use skill-creator to initialize a new skill called '[name]' in 'career_agent/.cursor/skills/'. This skill will handle [purpose]."

### 2. Develop & Refactor
*   Manual CLI: *Manual file edits*
*   Agent Prompt: "Review the SKILL.md for '[name]'. Following the Progressive Disclosure principle, move the detailed [examples/docs/schemas] into a new file in the `references/` folder to keep the main skill lean."

### 3. Validate
*   Manual CLI: `python career_agent/.cursor/skills/skill-creator/scripts/quick_validate.py career_agent/.cursor/skills/<name>`
*   Agent Prompt: "Run the `quick_validate.py` script on my '[name]' folder. If there are any errors in the frontmatter or structure, please fix them."

### 4. Package
*   Manual CLI: `python career_agent/.cursor/skills/skill-creator/scripts/package_skill.py career_agent/.cursor/skills/<name>`
*   Agent Prompt: "Validate and package my '[name]' skill into a `.skill` file for distribution."

## Phase 3: Design Principles
*   Progressive Disclosure: Keep the core `SKILL.md` under 500 lines. Always move verbose details to the `references/` folder.
*   Triggering: Remember that the YAML `description` in `SKILL.md` is the only field used to trigger the skill. It must be clear and comprehensive.
*   Voice: Use the imperative mood for instructions (e.g., "Generate the report," not "The agent will generate").
*   Anatomy: Ensure the folder structure strictly follows: `SKILL.md`, `scripts/`, `references/`, and `assets/`.
