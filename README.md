# 🚀 AI Agent Skills Collection

[中文](README_zh.md) | [English](README.md)

Welcome to the **AI Agent Skills Collection**! This repository serves as a centralized hub for custom skills designed to enhance the capabilities of AI coding assistants (such as Trae). 

Currently, the repository features our flagship skills, but it is designed to be highly expandable. More specialized skills will be added in the future to cover various aspects of the software development lifecycle.

---

## 🛠️ Available Skills

### 1. [Requirement Manager](./requirement-manager)
**Status**: Active | **Category**: Project Management & Architecture

The **Requirement Manager** is an intelligent AI Agent Skill built to enforce a "Specification-First (Software Design Document - SDD)" workflow. It ensures that standardized, predictable, and highly structured requirement documents are automatically generated before any code is written.

**Core Features:**
- **4-Stage Specification Framework**: Automatically generates `proposal.md`, `design.md`, `spec.md`, and `tasks.md`.
- **Global Project Registry**: Maintains an `sdd/project.md` file as a centralized index for all active and archived features.
- **Live Kanban Dashboard**: A built-in, zero-dependency local web server that visualizes your requirements as a live Kanban board, featuring:
  - Real-Time Sync (SSE)
  - Rich Details Modal (Markdown rendering)
  - Nested Subtasks
  - Instant Search & Filtering
  - i18n Support (English/Chinese)

[Read the full documentation for Requirement Manager ➔](./requirement-manager/README.md)

---

### 2. [Smart Requirement Manager](./smart-requirement-manager)
**Status**: Active | **Category**: Project Management & Architecture

The **Smart Requirement Manager** is an intelligent AI Agent Skill that combines **rigorous requirement interrogation (the "Grill")** with a **Specification-First (SDD)** workflow. It acts as both a rigorous Product Manager and a Systems Architect, ensuring that your vague or incomplete requirements are fully clarified before a single line of documentation or code is written.

**Core Features:**
- **The "Grill" Interrogation**: Analyzes your initial request and asks targeted questions to resolve missing details, edge cases, UI/UX flows, and technical constraints.
- **4-Stage Specification Framework**: After confirmation, it automatically generates `proposal.md`, `design.md`, `spec.md`, and `tasks.md`.
- **Machine-Readable Metadata**: Injects YAML Frontmatter into `spec.md`, enabling the AI Agent to instantly understand the impact radius and dependencies.
- **Global Project Registry**: Automatically maintains an `sdd/project.md` file as a centralized index for all active and archived features.
- **Zero Context Loss**: Keeps the AI focused during long coding sessions by relying on the highly detailed, clarified documents.
- **Live Kanban Dashboard**: A built-in, zero-dependency local web server that visualizes your requirements as a live Kanban board with real-time sync.

[Read the full documentation for Smart Requirement Manager ➔](./smart-requirement-manager/README.md)

---

## 🔮 Future Roadmap

As this repository grows, we plan to introduce more skills, such as:
- **Automated Testing Agents**: For generating and running test suites.
- **Code Review & Linting Assistants**: To enforce team coding standards.
- **Deployment Orchestrators**: To manage CI/CD pipelines seamlessly.