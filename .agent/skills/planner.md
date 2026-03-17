---
trigger: glob
globs: "**/*"
---

# Skill: Planner
Description: Generates the mandatory "PROPOSED EDIT PLAN" for complex changes.

## Instructions
When this skill is activated, you must generate a structured plan before making any edits to files over 300 lines or when handling multi-file refactors.

### Template Format
You must output your plan using the following exact structure:

```markdown
## PROPOSED EDIT PLAN
Working with: [filename]
Total planned edits: [number]

### GOAL
[Description of what we are trying to achieve]

### EDIT SEQUENCE
1. [Conceptual Change Name]
   - **Why**: [Purpose of change]
   - **Where**: [Function/Class/Line range]
   - **What**: [Brief technical description]

2. [Next Change...]
...

### Verification
- [ ] Run `pytest tests/...`
- [ ] Run `python scripts/skills/verify_architecture.py`
```

### Protocol
1.  **Stop**: After presenting the plan, you must **WAIT** for user confirmation before executing.
2.  **Iterate**: After each edit, report progress: `✅ Completed edit X of Y`.
