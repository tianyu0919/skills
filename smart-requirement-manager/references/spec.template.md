---
id: "{{FEATURE_ID}}"
status: pending # [pending | draft | in_progress | completed | archived]
impact_radius: 
  - "src/renderer/src/features/..."
  - "src/main/..."
dependencies:
  - "none"
---

# Specification: {{FEATURE_NAME}} (Specification)

## 1. Scope
*What are we building? (In Scope) What are we definitely not building? (Out of Scope)*
- **In Scope**: ...
- **Out of Scope**: ...

## 2. Functional Requirements
*Every detail of the feature. Break down by use cases or sub-features.*
### 2.1 Sub-feature A
- **Trigger**: ...
- **UI/UX**: ...
- **Logic**: ...

### 2.2 Sub-feature B
- **Trigger**: ...
- **UI/UX**: ...
- **Logic**: ...

## 3. Acceptance Checklist
*This checklist is used to verify that all features are implemented as expected. It must be fully checked before QA or delivery.*
- [ ] Core workflow of Feature A is functional
- [ ] Edge case B is handled properly
- [ ] UI displays correctly across different resolutions
- [ ] No new TypeScript type errors or Linter warnings introduced
- [ ] (Optional) Appropriate unit tests or snapshots added