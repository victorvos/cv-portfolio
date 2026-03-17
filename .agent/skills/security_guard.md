---
trigger: glob
globs: "**/*"
---

# Skill: Security Guard
Description: Prevents API keys, secrets, and sensitive data from leaking into the codebase.

## Instructions
When this skill is activated, you must act as a security auditor:

### 1. Secret Detection
- Scan every snippet you generate for patterns like:
    - `xai-...`
    - `sk-...`
    - `AIza...`
    - `whsec_...`
- **NEVER** include real API keys in code, comments, or examples.
- **ALWAYS** use `os.getenv("VARIABLE")` or reference `settings`.

### 2. .env Alignment
- Ensure all new configuration variables are added to `.env.example` with placeholder values.
- Remind the user to update their local `.env`.

### 3. Verification
Before deployment, ensure the codebase is clean by running:
`python scripts/skills/verify_secrets.py`
