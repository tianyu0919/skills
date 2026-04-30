---

name: "requirement-manager"
description: "Manages requirements by creating specs in the sdd folder for new requirements, and recording changes for existing ones. Invoke when adding or modifying requirements."

---

# Requirement Manager

This skill helps manage requirement specifications in the `sdd` folder.

## When to Use This Skill

Use this skill when the user:

- Asks to add a new requirement
- Asks to modify or update an existing requirement
- Mentions creating a spec for a new feature

## How it Works

### 1. New Requirements

When adding a new requirement, create a new specification directory under `sdd/specs/<requirement-name>/`.
This directory must follow the SDD standard structure and include:

- `proposal.md` - Context, problem statement, and why this feature is needed.
- `design.md` - Technical architecture, data flow, and how it will be implemented.
- `spec.md` - The detailed product specification, including YAML Frontmatter and the Acceptance Checklist.
- `tasks.md` - The breakdown of tasks to implement the requirement.

_Note: The old_ _`checklist.md`_ _is now merged directly into_ _`spec.md`._

### 2. Modifying Existing Requirements

When modifying an existing requirement, do not overwrite the original specification. Instead, create a new change record under the existing requirement's `changes` directory: `sdd/specs/<existing-requirement-name>/changes/<change-name>/`.
This change directory must include:

- `proposal.md` - Why is this change needed?
- `design.md` - How does this change affect the current architecture?
- `spec.md` - The detailed specification of the changes (with Frontmatter & Checklist).
- `tasks.md` - The breakdown of tasks for the changes.

### 3. Updating the Global Registry

Whenever you create or modify a requirement, you MUST update the `sdd/project.md` file to reflect the new feature or status.

### 4. Task Status Management

- All newly created tasks in `tasks.md` and checklists in `spec.md` must use Markdown task lists and be unchecked by default (`- [ ]`).
- When a task is completed, update its status to checked (`- [x]`).
- When ALL tasks and checklists for a requirement are checked (`- [x]`), its status MUST be updated to `completed` in BOTH the `spec.md` YAML Frontmatter AND the global registry `sdd/project.md`.

### 5. Archiving Requirements

- DO NOT automatically archive (`archived`) a requirement just because it is completed. Completed requirements stay in the active `sdd/specs/` directory as active documentation of the current system.
- Only archive a requirement (move it to `sdd/archive/` and update `sdd/project.md`) if the user EXPLICITLY asks to archive it, or if the feature has been completely deprecated/replaced by a newer system.

### 6. Opening the Dashboard

If the user asks to see the dashboard, kanban board, or wants to visualize the requirements:
1. Run the `scripts/dashboard.js` script using the terminal tool:
   ```bash
   node .trae/skills/requirement-manager/scripts/dashboard.js
   ```
2. Set the command to run non-blocking (in the background).
3. Once the server starts, inform the user that they can view the dashboard by opening `http://localhost:3030` in their browser, or use the OpenPreview tool if available.
   *Note: Let the user know the dashboard features Real-Time Sync (SSE), Search/Filter, Interactive Details Modals (click cards to read markdown), Nested Subtasks, and i18n (EN/ZH).*

## Steps to Execute

1. **Understand the Requirement**: Clarify with the user what the requirement or change entails.
2. **Determine the Scope**: Decide if this is a completely new requirement or a change to an existing one.
3. **Create the Structure**: Generate the necessary directories and markdown files (`proposal.md`, `design.md`, `spec.md`, `tasks.md`) in the appropriate location within the `sdd/specs` folder. **MUST** read and use the exact templates provided in `references/` directory of this skill.
4. **Update Global Registry**: Add or update the entry in `sdd/project.md`.
5. **Populate Content**: Write the content of the files based on the user's description.
6. **Confirm with User**: Ask the user to review the generated specification files.
