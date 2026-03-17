---
trigger: glob
globs: ["static/js/**/*.js", "static/css/**/*.css", "templates/**/*.html"]
---

# Skill: Frontend Master
Description: Ensures high-quality Vanilla JS and Reddit-inspired UI consistency.

## Instructions
When this skill is activated, you must follow these strict frontend standards:

### 1. The "Vanilla" Rule
- **No jQuery (`$`)**: Use `document.querySelector` or `document.getElementById`.
- **No Frameworks**: Stick to standard Web APIs and ES6 Modules.
- **No `var`**: Use `const` or `let` exclusively.

### 2. Design Language
- **Reddit-Style**: Aim for modular cards, clean typography, and a sticky, scrollable sidebar.
- **Responsiveness**: Use a mobile-first approach. Ensure touch targets are 44x44px.

### 3. State & Interactivity
- **Optimistic UI**: When a user votes or comments, update the DOM immediately before the `fetch` call completes.
- **WebSockets**: Ensure real-time components listen to the correct rooms defined in `Real-Time Architecture` docs.

### 4. Verification
Run the frontend linter before finishing:
`python scripts/skills/verify_frontend.py`
