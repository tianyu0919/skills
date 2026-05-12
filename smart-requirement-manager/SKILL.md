---
name: "smart-requirement-manager"
description: "Interrogates user to clarify vague requirements, then generates SDD specs, and manages requirement state. Invoke when adding or modifying requirements."
version: "1.0.0"
author: "tianyu0919"
tags:
  - requirements
  - sdd
  - specification
  - project-management
  - documentation
  - kanban
  - dashboard
category: "project-management"
---

# Smart Requirement Manager

This skill combines rigorous requirement gathering (the "Grill") with specification generation and management in the `sdd` folder. It ensures that vague or incomplete user requirements are fully clarified before any specification document is written.

## When to Use This Skill

Use this skill when the user:
- Proposes a new requirement or feature.
- Asks to add a new requirement.
- Asks to modify or update an existing requirement.

## Workflow

### Phase 1: Interrogation (The "Grill")
1. When the user proposes a requirement, DO NOT immediately write the spec.
2. **Context Gathering**: ALWAYS use search tools to consult the codebase first. Understand the current architecture, data models, and constraints related to the user's request.
3. Act as a rigorous, unrelenting Product Manager and Systems Architect.
4. **One Question at a Time**: NEVER bombard the user with a list of questions. You MUST ask exactly ONE piercing, specific question at a time.
5. Wait for the user's answer. Based on their answer and the codebase context, formulate the next logical question.
6. **Relentless Probe**: Dig deep into edge cases, error handling, UI/UX flows, backwards compatibility, and technical constraints.
7. **Resolve the Decision Tree**: Fully resolve one branch of the feature before moving to the next. Continue this back-and-forth iteration until the requirement is crystal clear and bulletproof.

### Phase 2: Alignment and Confirmation
1. Summarize the finalized, detailed requirements based on the user's answers.
2. Ask the user for final confirmation (e.g., "Are we aligned on these details? Should I proceed to generate the specification?").

### Phase 3: Specification Generation & Management
1. **Understand the Requirement**: Based on Phase 1 and 2, you have a clear understanding.
2. **Determine the Scope**: Decide if this is a completely new requirement or a change to an existing one.
3. **Create the Structure**: Generate the necessary directories and markdown files (`proposal.md`, `design.md`, `spec.md`, `tasks.md`) in the appropriate location within the `sdd/specs` folder. **MUST** read and use the exact templates provided in `references/` directory of this skill.
    *   **New Requirements**: Create a new specification directory under `sdd/specs/<requirement-name>/`.
    *   **Modifying Existing Requirements**: Create a new change record under the existing requirement's `changes` directory: `sdd/specs/<existing-requirement-name>/changes/<change-name>/`.
4. **Update Global Registry**: Add or update the entry in `sdd/project.md` to reflect the new feature or status.
5. **Populate Content**: Write the content of the files based on the clarified requirements. Ensure the `spec.md` includes YAML Frontmatter and the Acceptance Checklist.
6. **Confirm with User**: Ask the user to review the generated specification files.

### Task Status Management
- All newly created tasks in `tasks.md` and checklists in `spec.md` must use Markdown task lists and be unchecked by default (`- [ ]`).
- When a task is completed, update its status to checked (`- [x]`).
- When ALL tasks and checklists for a requirement are checked (`- [x]`), its status MUST be updated to `completed` in BOTH the `spec.md` YAML Frontmatter AND the global registry `sdd/project.md`.

### Archiving Requirements
- DO NOT automatically archive (`archived`) a requirement just because it is completed. Completed requirements stay in the active `sdd/specs/` directory as active documentation of the current system.
- Only archive a requirement (move it to `sdd/archive/` and update `sdd/project.md`) if the user EXPLICITLY asks to archive it, or if the feature has been completely deprecated/replaced by a newer system.

### Opening the Dashboard
If the user asks to see the dashboard, kanban board, or wants to visualize the requirements:
1. Run the `scripts/dashboard.js` script using the terminal tool:
   ```bash
   node smart-requirement-manager/scripts/dashboard.js
   ```
2. Set the command to run non-blocking (in the background).
3. Once the server starts, inform the user that they can view the dashboard by opening `http://localhost:3030` in their browser, or use the OpenPreview tool if available.
   *Note: Let the user know the dashboard features Real-Time Sync (SSE), Search/Filter, Interactive Details Modals (click cards to read markdown), Nested Subtasks, and i18n (EN/ZH).*
