---
trigger: glob
globs: ["core/**/*.py", "infrastructure/**/*.py", "presentation/**/*.py"]
---

# Skill: Architect
Description: Expert guidance for maintaining Clean Architecture and SOLID principles in Darom.

## Instructions
When this skill is activated, you must evaluate every code change against the following strict dependency rules:

### 1. Dependency Rule
- **Core Layer (`core/`)**: Must remain "pure". It cannot import from `infrastructure` or `presentation`. It should contain only business logic, entities, and abstract interfaces.
- **Infrastructure Layer (`infrastructure/`)**: Implements interfaces from `core`. It can import from `core`, but never from `presentation`.
- **Presentation Layer (`presentation/`)**: The entry point (API/Web). It can import from `core` (services/interfaces), but should ideally have dependencies injected.

### 2. SOLID Principles
- **SRP**: If a function or class does more than one thing, suggest splitting it.
- **DIP**: Always suggest depending on an Interface (from `core/interfaces`) rather than a concrete implementation.

### 3. Verification
Before finalizing any backend change, verify that no forbidden imports have been introduced by running:
`python scripts/skills/verify_architecture.py`
