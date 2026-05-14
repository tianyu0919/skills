---
name: "smart-requirement-workflow"
description: "Interrogates user to clarify vague requirements, then generates SDD specs, guides implementation, and verifies completion. Full lifecycle from requirement gathering to verified delivery. Invoke when adding, modifying, or implementing requirements."
version: "2.0.0"
author: "tianyu0919"
tags:
  - requirements
  - sdd
  - specification
  - project-management
  - documentation
  - kanban
  - dashboard
  - implementation
  - verification
category: "project-management"
---

# Smart Requirement Workflow

This skill combines rigorous requirement gathering (the "Grill") with specification generation, implementation guidance, and verification — all managed under the `sdd` folder. It ensures that vague or incomplete user requirements are fully clarified before any specification document is written, and that implementation stays on track through to verified completion.

## When to Use This Skill

Use this skill when the user:
- Proposes a new requirement or feature.
- Asks to add a new requirement.
- Asks to modify or update an existing requirement.
- Wants to implement a previously specified requirement.

## Workflow

### Phase 1: Interrogation (The "Grill")

1. When the user proposes a requirement, **DO NOT** immediately write the spec.
2. **Context Gathering**: ALWAYS use search tools to consult the codebase first. Understand the current architecture, data models, constraints, and affected modules related to the user's request.
3. Act as a rigorous, unrelenting Product Manager and Systems Architect.
4. **One Question at a Time**: NEVER bombard the user with a list of questions. You MUST ask exactly ONE piercing, specific question at a time.
5. Wait for the user's answer. Based on their answer and the codebase context, formulate the next logical question.
6. **Relentless Probe**: Dig deep into edge cases, error handling, UI/UX flows, backwards compatibility, breaking changes, and technical constraints.
7. **Resolve the Decision Tree**: Fully resolve one branch of the feature before moving to the next. Continue this back-and-forth iteration until the requirement is crystal clear and bulletproof.

### Phase 2: Alignment and Confirmation

1. Summarize the finalized, detailed requirements based on the user's answers.
2. Ask the user for final confirmation (e.g., "Are we aligned on these details? Should I proceed to generate the specification?").

### Phase 3: Specification Generation & Management

#### Step 1: Check for Existing Specs

Before creating new files:
1. List `sdd/specs/` to find directories matching the current intent.
2. If a match exists and has unchecked tasks → **resume** from where it left off (skip to Phase 4).
3. If a match exists and is fully completed (`status: completed`) → decide if a new spec is needed or if a new `changes/` entry under the existing spec suffices.
4. If no match → proceed to Step 2.

#### Step 2: Determine the Scope

Decide if this is a completely new requirement or a change to an existing one.

#### Step 3: Create the Structure

Generate the necessary directories and markdown files in the appropriate location within the `sdd/specs` folder. **MUST** read and use the exact templates provided in `references/` directory of this skill.

- **New Requirements**: Create a new specification directory under `sdd/specs/<requirement-name>/`. Use a **verb-led slug** for the name (e.g., `add-user-login`, `migrate-auth-to-jwt`, `refactor-payment-flow`).
  ```
  sdd/specs/<requirement-name>/
  ├── proposal.md       # Context, pain points, value proposition, alternatives, success metrics
  ├── design.md         # Technical architecture, data models, interfaces, data flow, error handling
  ├── spec.md           # YAML Frontmatter, scope, functional requirements (SHALL/Scenario)
  ├── tasks.md          # Ordered task board with explicit dependencies and parallel markers
  └── checklist.md      # Standalone verification criteria
  ```

- **Modifying Existing Requirements**: Create a new change record under the existing requirement's `changes` directory. Use a verb-led slug for the change name.
  ```
  sdd/specs/<existing-requirement-name>/changes/<change-name>/
  ├── proposal.md
  ├── design.md
  ├── spec.md
  ├── tasks.md
  └── checklist.md
  ```

#### Step 4: Write `spec.md`

In addition to the template structure, for functional requirements use the **SHALL/Scenario** format to ensure testability:

```markdown
## N. Functional Requirements

### ADDED
#### Requirement: [Name]
The system SHALL ...

##### Scenario: [Case Name]
- **WHEN** [trigger condition]
- **THEN** [expected outcome]

### MODIFIED (if applicable)
#### Requirement: [Name]
[Complete modified requirement with context]

### REMOVED (if applicable)
#### Requirement: [Name]
**Reason**: [Why removing]
**Migration**: [How to handle existing usage]
```

#### Step 5: Write `tasks.md`

In addition to the template structure, **always** include a `# Task Dependencies` section:

```markdown
# Task Dependencies
- [Task 2] depends on [Task 1]
- [Task 3] and [Task 4] can run in parallel
```

Principles:
- Each task should deliver verifiable progress.
- Include validation steps (tests, linting) where appropriate.
- Mark parallelizable tasks explicitly.
- Do NOT over-design or over-estimate scope.

#### Step 6: Write `checklist.md`

Create a standalone verification checklist. Each item must be objectively verifiable:

```markdown
# Verification Checklist

- [ ] [Concrete and testable criterion 1]
- [ ] [Concrete and testable criterion 2]
- [ ] Unit tests pass
- [ ] No TypeScript errors
- [ ] No linting warnings
- [ ] Manual smoke test on target platform passes
```

#### Step 7: Update Global Registry

Add or update the entry in `sdd/project.md` to reflect the new feature, status, and dependencies.

#### Step 8: Confirm with User

Present the generated files to the user for review. Do NOT proceed to implementation until explicit approval is given.

---

### Phase 4: Implementation

1. Work through `tasks.md` in order, respecting the declared dependencies.
2. Check off each task and subtask as it is completed (`- [x]`).
3. For tasks marked as parallelizable with no inter-dependencies, work on them concurrently when possible.
4. If a task reveals new requirements or unforeseen complexity, pause and update `spec.md`, `tasks.md`, and `checklist.md` before continuing.
5. Update the status in `spec.md` YAML Frontmatter as progress is made (e.g., `draft` → `in_progress`).

---

### Phase 5: Verification

1. Go through every item in `checklist.md`.
2. For each item, verify the criterion is met (run tests, inspect code, manual testing, etc.).
3. Check off passing items (`- [x]`).
4. If any item fails:
   - Add a new task to `tasks.md` to address it.
   - Implement the fix (Phase 4).
   - Re-verify (Phase 5).
5. When ALL items in `checklist.md` AND all tasks in `tasks.md` are checked (`- [x]`), update the requirement status to `completed` in BOTH the `spec.md` YAML Frontmatter AND the global registry `sdd/project.md`.

---

## Guardrails

- **No code in Phase 1–3.** Spec documents only. Do not implement anything before explicit user approval.
- **No rollback of unrelated changes.** The workspace may contain other people's work — leave it alone.
- **Favor minimal implementations.** Add complexity only when the spec requires it.
- **Spec documents use the same language as user communication.** Follow the language of the user's latest message.
- **Do not delete spec documents after completion.** They serve as the historical record and living documentation of the system.
- **Always consult the codebase before writing specs.** Specs written without understanding the existing system are worse than no specs at all.

---

## Task Status Management

- All newly created tasks in `tasks.md` and checklists in both `spec.md` and `checklist.md` must use Markdown task lists and be unchecked by default (`- [ ]`).
- When a task is completed, update its status to checked (`- [x]`).
- When ALL tasks and checklists for a requirement are checked (`- [x]`), its status MUST be updated to `completed` in BOTH the `spec.md` YAML Frontmatter AND the global registry `sdd/project.md`.

## Archiving Requirements

- **DO NOT** automatically archive (`archived`) a requirement just because it is completed. Completed requirements stay in the active `sdd/specs/` directory as active documentation of the current system.
- Only archive a requirement (move it to `sdd/archive/` and update `sdd/project.md`) if the user EXPLICITLY asks to archive it, or if the feature has been completely deprecated/replaced by a newer system.

## Opening the Dashboard

If the user asks to see the dashboard, kanban board, or wants to visualize the requirements:
1. Run the `scripts/dashboard.js` script using the terminal tool:
   ```bash
   node smart-requirement-workflow/scripts/dashboard.js
   ```
2. Set the command to run non-blocking (in the background).
3. Once the server starts, inform the user that they can view the dashboard by opening `http://localhost:3030` in their browser, or use the OpenPreview tool if available.
   *Note: Let the user know the dashboard features Real-Time Sync (SSE), Search/Filter, Interactive Details Modals (click cards to read markdown), Nested Subtasks, and i18n (EN/ZH).*