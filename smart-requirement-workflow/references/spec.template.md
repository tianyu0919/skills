---
id: "{{FEATURE_ID}}"
status: pending # [pending | draft | in_progress | completed | archived]
impact_radius:
  - "<module-or-path-1>"
  - "<module-or-path-2>"
dependencies:
  - "none"
---

# Specification: {{FEATURE_NAME}} (Specification)

## 1. Scope
*What are we building? (In Scope) What are we definitely not building? (Out of Scope)*
- **In Scope**: ...
- **Out of Scope**: ...

## 2. Functional Requirements

### ADDED
#### Requirement: [Requirement Name]
The system SHALL ...

##### Scenario: [Normal Case]
- **WHEN** [trigger condition]
- **THEN** [expected outcome]

##### Scenario: [Edge Case]
- **WHEN** [trigger condition]
- **THEN** [expected outcome]

#### Requirement: [Another Requirement Name]
The system SHALL ...

##### Scenario: [Case Name]
- **WHEN** [trigger condition]
- **THEN** [expected outcome]

### MODIFIED (if applicable)
#### Requirement: [Existing Requirement Name]
[Complete modified requirement with full context — cite which part changed and why]

##### Scenario: [Case Name]
- **WHEN** [trigger condition]
- **THEN** [expected outcome]

### REMOVED (if applicable)
#### Requirement: [Deprecated Requirement Name]
**Reason**: [Why removing]
**Migration**: [How existing usage is handled]