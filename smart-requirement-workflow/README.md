# Trae Skill: Smart Requirement Workflow

[English](README.md) | [中文](README_zh.md)

Smart Requirement Workflow is an intelligent AI Agent Skill that combines **rigorous requirement interrogation (the "Grill")** with a full **Specification-First (SDD)** workflow — from requirement gathering through to verified implementation. It acts as both a rigorous Product Manager and a Systems Architect, ensuring that your vague or incomplete requirements are fully clarified before a single line of documentation or code is written, and that implementation stays on track through to verified completion.

## ✨ Core Features

- **The "Grill" Interrogation** (Phase 1): Analyzes your initial request and asks **one targeted question at a time** to resolve missing details, edge cases, UI/UX flows, and technical constraints — all informed by live codebase context.
- **Check for Existing Specs** (Phase 3): Before creating new specs, scans `sdd/specs/` for matching work that can be resumed or extended, preventing duplicate effort.
- **5-Stage Specification Framework** (Phase 3): After confirmation, automatically generates 5 core documents:
  - `proposal.md` — context, pain points, value proposition, alternatives, success metrics
  - `design.md` — technical architecture, data models, interfaces, data flow, error handling
  - `spec.md` — YAML Frontmatter, scope, **SHALL/Scenario** functional requirements
  - `tasks.md` — ordered task board with **explicit dependencies** and parallel markers
  - `checklist.md` — standalone verification criteria (objectively verifiable)
- **SHALL/Scenario Requirement Format**: Structured requirements with `The system SHALL … / WHEN … THEN …` scenarios for built-in testability and clarity.
- **Implementation Guidance** (Phase 4): Tasks are executed in dependency order, with parallel markers for concurrent work. Mid-implementation discoveries feed back into spec updates.
- **Independent Verification** (Phase 5): A dedicated verification phase using the standalone `checklist.md`, with a fix-retry loop until every item passes.
- **Guardrails**: Explicit guardrails prevent premature coding, protect unrelated work, and enforce minimal implementations.
- **Machine-Readable Metadata**: Injects YAML Frontmatter into `spec.md` (status, impact radius, dependencies), enabling the AI Agent to instantly understand the impact radius and dependencies.
- **Global Project Registry**: Automatically maintains an `sdd/project.md` file as a centralized index for all active and archived features.
- **Zero Context Loss**: Keeps the AI focused during long coding sessions by relying on the highly detailed, clarified documents.

## 🚀 How to Use (Workflow)

You can trigger the Smart Requirement Workflow skill by making requests like:
- "Use smart-requirement-workflow to add a new login feature."
- "I have a new idea for a shopping cart, let's use smart-requirement-workflow."
- "Implement the feature we specified last week."

### The 5-Phase Execution

1. **Phase 1: Interrogation (The "Grill")**
   - The AI **will not** immediately write the spec.
   - **Context Gathering**: The AI will first consult the codebase to understand the current architecture, data models, and constraints.
   - **One Question at a Time**: The AI will NEVER bombard you with a list of questions. It will ask exactly ONE specific, piercing question at a time.
   - You answer the question, and the AI iterates based on your answer and the codebase context, digging into edge cases until all decision branches are resolved.
2. **Phase 2: Alignment and Confirmation**
   - The AI summarizes the finalized, detailed requirements based on your answers.
   - It asks for your final confirmation before proceeding.
3. **Phase 3: Specification Generation**
   - Checks for existing matching specs to avoid duplicates.
   - Once confirmed, the AI generates the complete SDD structure (`proposal.md`, `design.md`, `spec.md`, `tasks.md`, `checklist.md`) in the `sdd/specs/` directory, updates the global registry, and presents the documents for review.
   - **No code is written until you explicitly approve.**
4. **Phase 4: Implementation**
   - The AI works through `tasks.md` in dependency order, checking off completed tasks.
   - Parallelizable tasks are executed concurrently.
   - If new requirements emerge during implementation, specs are updated before continuing.
5. **Phase 5: Verification**
   - Every item in `checklist.md` is verified against the actual implementation.
   - Failing items trigger a fix-retry loop until all pass.
   - When all tasks and checklists are complete, the status is updated to `completed`.

## 📂 Directory Structure & Conventions

This skill manages the workflow through the `sdd` folder located in the root directory of your project.

### 1. New Requirements
Created under `sdd/specs/<requirement-name>/` using a **verb-led slug** (e.g., `add-user-login`, `migrate-auth-to-jwt`), containing:
- **`proposal.md`**: Context, current pain points, feature value proposition, alternatives considered, success metrics.
- **`design.md`**: Technical architecture, data models, interfaces, data flow, error handling strategies.
- **`spec.md`**: YAML Frontmatter, scope, **SHALL/Scenario** functional requirements (ADDED/MODIFIED/REMOVED).
- **`tasks.md`**: Executable task board ordered by phase, with explicit `# Task Dependencies` and parallel markers.
- **`checklist.md`**: Standalone verification criteria — objectively verifiable items across functional, code quality, testing, and non-functional categories.

### 2. Modifying Existing Requirements
Created as a change record: `sdd/specs/<existing-requirement-name>/changes/<change-name>/` containing the same five core files to clearly track the motivation and implementation details of the change.

## 📌 Task Status & Lifecycle Management

- **Task Tracking**: All tasks and checklists use Markdown task lists (`- [ ]`).
- **Status Updates**: Completed tasks are checked (`- [x]`).
- **Feature Closure**: When all tasks AND all checklist items are completed, the status in `spec.md` YAML Frontmatter and `sdd/project.md` is updated to `completed`.
- **Archiving**: Features are only moved to `sdd/archive/` if explicitly requested or completely deprecated. Completed features remain in `sdd/specs/` as living documentation.

## 🛡️ Guardrails

- **No code before approval**: Specification documents only during Phases 1–3.
- **Leave unrelated code alone**: The workspace may contain other people's work.
- **Minimal implementations**: Add complexity only when the spec requires it.
- **Language consistency**: Spec documents follow the user's language.
- **Codebase-aware specs**: Always consult the existing system before writing.

## 📊 Live Kanban Dashboard

Smart Requirement Workflow includes a built-in, zero-dependency Node.js script to visualize your requirements as a live Kanban board.

### ✨ Dashboard Features
- **Real-Time Sync (SSE)**: Automatically syncs Markdown file changes.
- **Rich Details Modal**: Click cards to read `proposal`, `design`, `spec`, `tasks`, and `checklist`.
- **Nested Subtasks**: Optimizations and changes are visually nested.
- **Instant Search**: Real-time filtering by name, dependencies, or subtasks.
- **i18n Support**: English and Chinese interfaces.

Simply ask the AI:
> "Open the requirements dashboard"

The AI will automatically start the background server and provide a preview link (**http://localhost:3030**).