# Trae Skill: Smart Requirement Manager

[English](README.md) | [中文](README_zh.md)

Smart Requirement Manager is an intelligent AI Agent Skill that combines **rigorous requirement interrogation (the "Grill")** with **Specification-First (SDD)** workflow. It acts as both a rigorous Product Manager and a Systems Architect, ensuring that your vague or incomplete requirements are fully clarified before a single line of documentation or code is written.

## ✨ Core Features

- **The "Grill" Interrogation**: Analyzes your initial request and asks targeted questions to resolve missing details, edge cases, UI/UX flows, and technical constraints.
- **4-Stage Specification Framework**: After confirmation, it automatically generates `proposal.md`, `design.md`, `spec.md`, and `tasks.md`.
- **Machine-Readable Metadata**: Injects YAML Frontmatter into `spec.md`, enabling the AI Agent to instantly understand the impact radius and dependencies.
- **Global Project Registry**: Automatically maintains an `sdd/project.md` file as a centralized index for all active and archived features.
- **Zero Context Loss**: Keeps the AI focused during long coding sessions by relying on the highly detailed, clarified documents.

## 🚀 How to Use (Workflow)

You can trigger the Smart Requirement Manager skill by making requests like:
- "Use smart-requirement-manager to add a new login feature."
- "I have a new idea for a shopping cart, let's use smart-requirement-manager."

### The 3-Phase Execution

1. **Phase 1: Interrogation (The "Grill")**
   - The AI **will not** immediately write the spec.
   - **Context Gathering**: The AI will first consult the codebase to understand the current architecture, data models, and constraints.
   - **One Question at a Time**: The AI will NEVER bombard you with a list of questions. It will ask exactly ONE specific, piercing question at a time.
   - You answer the question, and the AI iterates based on your answer and the codebase context, digging into edge cases until all decision branches are resolved.
2. **Phase 2: Alignment and Confirmation**
   - The AI summarizes the finalized, detailed requirements based on your answers.
   - It asks for your final confirmation before proceeding.
3. **Phase 3: Specification Generation**
   - Once confirmed, the AI generates the complete SDD structure (`proposal.md`, `design.md`, `spec.md`, `tasks.md`) in the `sdd/specs/` directory and updates the global registry.

## 📂 Directory Structure & Conventions

This skill manages the workflow through the `sdd` folder located in the root directory of your project.

### 1. New Requirements
Created under `sdd/specs/<requirement-name>/` containing:
- **`proposal.md`**: Context, current pain points, feature value proposition.
- **`design.md`**: Technical architecture, data models, data flow.
- **`spec.md`**: Detailed product specifications, YAML Frontmatter, and an Acceptance Checklist.
- **`tasks.md`**: Executable task board.

### 2. Modifying Existing Requirements
Created as a change record: `sdd/specs/<existing-requirement-name>/changes/<change-name>/` containing the same four core files to clearly track the motivation and implementation details of the change.

## 📌 Task Status & Lifecycle Management

- **Task Tracking**: All tasks and checklists use Markdown task lists (`- [ ]`).
- **Status Updates**: Completed tasks are checked (`- [x]`).
- **Feature Closure**: When all tasks are completed, the status in `spec.md` and `sdd/project.md` is updated to `completed`.
- **Archiving**: Features are only moved to `sdd/archive/` if explicitly requested or completely deprecated.

## 📊 Live Kanban Dashboard

Smart Requirement Manager includes a built-in, zero-dependency Node.js script to visualize your requirements as a live Kanban board.

### ✨ Dashboard Features
- **Real-Time Sync (SSE)**: Automatically syncs Markdown file changes.
- **Rich Details Modal**: Click cards to read `proposal`, `design`, `spec`, and `tasks`.
- **Nested Subtasks**: Optimizations and changes are visually nested.
- **Instant Search**: Real-time filtering.
- **i18n Support**: English and Chinese interfaces.

Simply ask the AI:
> "Open the requirements dashboard"

The AI will automatically start the background server and provide a preview link (**http://localhost:3030**).
