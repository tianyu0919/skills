# Trae Skill: Requirement Manager

[English](README.md) | [中文](README_zh.md)

Requirement Manager is an intelligent AI Agent Skill designed for AI-assisted programming. It is built to enforce a "Specification-First (SDD)" workflow, ensuring that standardized, predictable, and highly structured requirement documents are automatically generated before any code is written.

## ✨ Core Features

- **4-Stage Specification Framework**: Automatically generates `proposal.md`, `design.md`, `spec.md`, and `tasks.md`.
- **Machine-Readable Metadata**: Injects YAML Frontmatter into `spec.md`, enabling the AI Agent to instantly understand the impact radius and dependencies.
- **Global Project Registry**: Automatically maintains an `sdd/project.md` file as a centralized index for all active and archived features.
- **Zero Context Loss**: By utilizing a standardized document structure, it keeps the AI focused during long coding sessions, effectively preventing architectural drift.

## 📂 Directory Structure & Conventions

This skill manages the workflow through the `sdd` folder located in the root directory of your project.

### 1. New Requirements
When adding a new requirement, a directory will be created under `sdd/specs/<requirement-name>/`. Each directory must follow the SDD standard structure and contain these four core files:

- **`proposal.md`**: Context, current pain points, feature value proposition, alternative considerations, and success metrics.
- **`design.md`**: Technical architecture, data models, interface definitions, data flow, and error-handling strategies.
- **`spec.md`**: Detailed product specifications containing YAML Frontmatter (for status, impact radius, and dependencies), feature details, and an Acceptance Checklist.
- **`tasks.md`**: Breaks down the requirement into an executable, atomic task board grouped by phases (e.g., scaffolding, core logic, UI interaction).

### 2. Modifying Existing Requirements
When modifying an existing requirement, the original specification is **not** overwritten. Instead, a new change record is created under the existing requirement's `changes` directory:
`sdd/specs/<existing-requirement-name>/changes/<change-name>/`

The change directory must also contain the four core files (`proposal.md`, `design.md`, `spec.md`, `tasks.md`) to clearly track the motivation and implementation details of the change.

## 🛠 Installation Guide

Run the following command in your project's root directory to install the skill automatically:

```bash
npx skills add https://github.com/tianyu0919/skills --skills requirement-manager
```

## 🚀 How to Use (Workflow)

You can trigger the Requirement Manager skill by making requests like:
- "Add a new requirement: ..."
- "Modify existing feature: ..."
- "Create a requirement document for the new feature..."

### Execution Steps

1. **Understand**: The AI clarifies the specific details of the requirement or change with you.
2. **Scope**: Determines whether this is an entirely new requirement or a modification to an existing feature.
3. **Generate Structure**: The AI reads the templates from this skill's `references/` directory and generates the corresponding four Markdown files in the `sdd/specs/` directory.
4. **Update Registry**: Adds or updates the feature's entry in the global `sdd/project.md`.
5. **Populate Content**: The AI automatically writes the specific content of the four documents based on your description.
6. **User Confirmation**: The AI asks you to review the generated specification documents before proceeding to the development phase.

## 📌 Task Status & Lifecycle Management

- **Task Tracking**: All tasks and acceptance checklists in `tasks.md` and `spec.md` default to incomplete Markdown task lists (`- [ ]`).
- **Status Updates**: When a task is finished, the AI updates it to completed (`- [x]`).
- **Feature Closure**: When all tasks and checklists for a requirement are completed (`- [x]`), the status in both the `spec.md` YAML Frontmatter and the `sdd/project.md` registry must be updated to `completed`.
- **Archiving Rules**:
  - **Do NOT** archive (`archived`) a requirement simply because it is completed. Completed requirements should remain in the active `sdd/specs/` directory as live documentation of the current system architecture.
  - **ONLY** move a feature to the `sdd/archive/` directory and update the global registry if you **explicitly request** to archive it, or if the feature has been completely deprecated/replaced by a newer system.

## 📊 Live Kanban Dashboard

Requirement Manager includes a built-in, zero-dependency Node.js script to visualize your requirements as a live Kanban board.

### ✨ Dashboard Features
- **Real-Time Sync (SSE)**: Automatically and instantly syncs any Markdown file changes to the board without manual refreshing.
- **Rich Details Modal**: Click on any requirement card to read its full `proposal`, `design`, `spec`, and `tasks` parsed as beautiful Markdown directly in the browser.
- **Nested Subtasks**: Optimizations and changes are visually nested under their parent requirements.
- **Instant Search**: Real-time filtering by requirement name, dependencies, or subtasks.
- **i18n Support**: Seamless toggle between English and Chinese interfaces.

You don't need to run any commands manually! Simply ask the AI:

> "Open the requirements dashboard"
> or
> "Show me the kanban board"

The AI will automatically start the background server and provide you with a preview link (typically **http://localhost:3030** ).
