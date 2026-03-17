# Cursor Rules (Darom)

Rules in `.cursor/rules/` provide persistent context for the AI. Same structure as mapsai; project-specific paths and AI stack (Gemini/Grok, core/infrastructure/presentation).

## Rule files

| File | Applies to | Purpose |
|------|------------|---------|
| `general.instructions.md` | All | Standards, folder structure, Python/JS/HTML/CSS, DB, AI (Gemini/Grok), security |
| `operational.mdc` | All | Prime Directive, planning phase, execution, refactoring |
| `python.mdc` | `**/*.py` | FastAPI, clean architecture (darom/ root), services, DI |
| `app_architecture.mdc` | `core/**`, `infrastructure/**`, `presentation/**` | Layer boundaries, forbidden imports, DI |
| `frontend.mdc` | `**/*.html`, `**/*.css`, `**/*.js`, `**/*.ts` | Jinja2, vanilla JS, CSS, templates/ & static/ |
| `markdown.mdc` | `**/*.md`, `**/*.rst` | Docs structure, Mermaid palette, API docs |
| `langchain_python.mdc` | `**/*.py` | LangChain agents, vector stores, service layer (darom-only) |

## Workflows

`.cursor/workflows/` holds reference workflows (synced from `.agent/workflows/`): code_style_dry, documentation_mermaid, fastapi_routing, frontend_backend_architecture, testing_guidelines, plus darom-specific (fastapi_async_optimization, frontend_mobile_optimization, langchain_guidelines).

## Activation

- **Always:** `general.instructions.md`, `operational.mdc`
- **By glob:** Python, app_architecture, frontend, markdown, langchain_python apply when matching files are in context.
