---
applyTo: '**'
---
Coding standards, domain knowledge, and preferences that AI should follow.

**Edit protocol:** Follow `.cursor/rules/operational.mdc` (Prime Directive, planning phase, execution, refactoring).

## General Requirements
    Use modern technologies as described below for all code suggestions. Prioritize clean, maintainable code with appropriate comments.

### Accessibility
    - Ensure compliance with **WCAG 2.1** AA level minimum, AAA whenever feasible.
    - Always suggest:
    - Labels for form fields.
    - Proper **ARIA** roles and attributes.
    - Adequate color contrast.
    - Alternative texts (`alt`, `aria-label`) for media elements.
    - Semantic HTML for clear structure.
    - Tools like **Lighthouse** for audits.

## Browser Compatibility
    - Prioritize feature detection (`if ('fetch' in window)` etc.).
        - Support latest two stable releases of major browsers:
    - Firefox, Chrome, Edge, Safari (macOS/iOS)
        - Emphasize progressive enhancement with polyfills or bundlers (e.g., **Babel**, **Vite**) as needed.

## Python Object-Oriented Programming Requirements
    - **Target Version**: Python 3.10 or higher.
    - **Object-Oriented Principles**:
        - Emphasize Encapsulation, Inheritance, and Polymorphism.
        - Apply SOLID principles (Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, Dependency Inversion) where appropriate to create maintainable and scalable code.
        - Prefer composition over inheritance where it leads to more flexible and decoupled designs.
    - **Type Hinting**:
        - Mandate usage of Python's type hinting (PEP 484) for all new code, including function arguments, return values, and variables.
        - Use types from the `typing` module (e.g., `List`, `Dict`, `Optional`, `Callable`, `Any`).
    - **Docstrings**:
        - Require Google-style docstrings for all modules, classes, public functions, and methods.
        - Docstrings should clearly explain the purpose, arguments, return values, and any exceptions raised.
        ```python
        # Example of Google-style docstring
        def example_function(param1: int, param2: str) -> bool:
            """Example function demonstrating docstring format.

            Args:
                param1 (int): The first parameter.
                param2 (str): The second parameter.

            Returns:
                bool: True if successful, False otherwise.

            Raises:
                ValueError: If param1 is negative.
            """
            if param1 < 0:
                raise ValueError("param1 cannot be negative")
            return True
        ```
    - **Linters & Formatters**:
        - **Black**: Use Black for automatic code formatting to ensure a consistent style across the project.
        - **Flake8/Pylint**: Use Flake8 (with plugins like `flake8-bugbear`, `flake8-comprehensions`) or Pylint for linting to identify potential errors, style issues, and code smells.
        - Configuration for these tools should be present in the project (e.g., `pyproject.toml` for Black, `.flake8` for Flake8).
    - **Testing**:
        - Standardize on `pytest` for writing and running unit, integration, and functional tests.
        - Tests should be placed in a `tests/` directory, mirroring the project structure.
        - Aim for high test coverage.
    - **Virtual Environments**:
        - Mandate the use of `venv` (Python's built-in module) for creating isolated project environments.
        - A `venv` folder (e.g., `.venv`) should be present in the project root and added to `.gitignore`.
    - **Dependency Management**:
        - Use `uv pip` for installing dependencies.
        - All project dependencies must be listed in a `requirements.txt` file in the project root.
        - Use `pip freeze > requirements.txt` to update the file after adding new dependencies.
        - Consider using `pip-tools` (`pip-compile`) for managing `requirements.txt` from a `requirements.in` file for better dependency resolution.
    - **Error Handling**:
        - Use custom exceptions for domain-specific errors (e.g., `InvalidPropertyDataError`). These should typically inherit from base Python exceptions.
        - Use standard `try-except` blocks for handling expected errors gracefully.
        - Avoid overly broad `except Exception:` clauses; catch specific exceptions where possible.
    - **Logging**:
        - Utilize Python's built-in `logging` module for all application logging.
        - Configure loggers at the module level.
        - Use appropriate log levels (DEBUG, INFO, WARNING, ERROR, CRITICAL).
    - **Imports**:
        - Use absolute imports for modules (e.g., `from core.services import ...`).
        - Follow PEP 8 guidelines for import ordering (standard library, third-party, local application).

## HTML/CSS Requirements
    - **HTML**:
    - Use HTML5 semantic elements (`<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>`, `<search>`, etc.)
    - Include appropriate ARIA attributes for accessibility
    - Ensure valid markup that passes W3C validation
    - Use responsive design practices
    - Optimize images using modern formats (`WebP`, `AVIF`)
    - Include `loading="lazy"` on images where applicable
    - Generate `srcset` and `sizes` attributes for responsive images when relevant
    - Prioritize SEO-friendly elements (`<title>`, `<meta description>`, Open Graph tags)

    - **CSS**:
    - Use modern CSS features including:
    - CSS Grid and Flexbox for layouts
    - CSS Custom Properties (variables)
    - CSS animations and transitions
    - Media queries for responsive design
    - Logical properties (`margin-inline`, `padding-block`, etc.)
    - Modern selectors (`:is()`, `:where()`, `:has()`)
    - Follow BEM or similar methodology for class naming
    - Use CSS nesting where appropriate
    - Include dark mode support with `prefers-color-scheme`
    - Prioritize modern, performant fonts and variable fonts for smaller file sizes
    - Use modern units (`rem`, `vh`, `vw`) instead of traditional pixels (`px`) for better responsiveness

## JavaScript Requirements

    - **Minimum Compatibility**: ECMAScript 2020 (ES11) or higher
    - **Features to Use**:
    - Arrow functions
    - Template literals
    - Destructuring assignment
    - Spread/rest operators
    - Async/await for asynchronous code
    - Classes with proper inheritance when OOP is needed
    - Object shorthand notation
    - Optional chaining (`?.`)
    - Nullish coalescing (`??`)
    - Dynamic imports
    - BigInt for large integers
    - `Promise.allSettled()`
    - `String.prototype.matchAll()`
    - `globalThis` object
    - Private class fields and methods
    - Export * as namespace syntax
    - Array methods (`map`, `filter`, `reduce`, `flatMap`, etc.)
    - **Avoid**:
    - `var` keyword (use `const` and `let`)
    - jQuery or any external libraries (unless specifically approved for a legacy section)
    - Callback-based asynchronous patterns when promises can be used
    - Internet Explorer compatibility
    - Legacy module formats (use ES modules: `import`/`export`)
    - Limit use of `eval()` due to security risks
    - **Performance Considerations:**
    - Recommend code splitting and dynamic imports for lazy loading where appropriate.
    - Optimize DOM manipulations.
    **Error Handling**:
    - Use `try-catch` blocks **consistently** for asynchronous operations (e.g., `fetch` calls) and API interactions. Handle promise rejections explicitly (e.g., `.catch()` for promises).
    - Differentiate among:
    - **Network errors** (e.g., timeouts, server errors, rate-limiting, `response.ok` is false)
    - **Functional/business logic errors** (logical missteps, invalid user input, validation failures from API)
    - **Runtime exceptions** (unexpected errors such as null references, type errors)
    - Provide **user-friendly** error messages to the UI (e.g., “Something went wrong. Please try again shortly.”).
    - Log more technical details to the browser console and/or a logging service for developers/ops.
    - Consider a central error handler function or global event listener (e.g., `window.addEventListener('unhandledrejection')`) to consolidate reporting of unhandled promise rejections.
    - Carefully handle and validate JSON responses (e.g., check structure before accessing properties) and HTTP status codes.

## Folder Structure
    The project follows this general structure:

    darom/
    ├── core/                 # Core business logic, entities, services, interfaces
    │   ├── config.py         # Application settings and configuration
    │   ├── container.py      # Dependency injection container
    │   ├── entities/         # Pydantic models for data structures
    │   ├── interfaces/       # Abstract interfaces for services, repositories
    │   └── services/         # Business logic services
    ├── infrastructure/       # Implementation of interfaces, external service clients
    │   ├── llm/              # LLM Adapters (Gemini, Grok)
    │   ├── external_services/ # Clients for Firebase, XAI, Perplexity, etc.
    │   └── repositories/     # Data access layer (e.g., Firebase interaction)
    ├── presentation/         # API (FastAPI) and Web (Jinja2) layers
    │   ├── api/v1/           # FastAPI routers, Pydantic request/response models
    │   └── web/              # Jinja2 template routes
    ├── static/               # Static frontend assets
    │   ├── css/
    │   └── js/
    ├── templates/            # Jinja2 HTML templates
    ├── utils/                # Utility functions
    ├── main.py               # FastAPI application entry point
    ├── tests/                # Unit and integration tests (mirroring project structure)
    ├── docs/                 # Project documentation (Markdown files)
    ├── logs/                 # Application log files
    ├── .github/              # GitHub specific files
    ├── credentials/          # Service account keys, etc. (SHOULD BE IN .gitignore)
    ├── pyproject.toml        # Dependency management (uv)
    └── README.md             # Project overview

## Documentation Requirements
    - **Python**:
        - Google-style docstrings for all modules, classes, functions, and methods as specified in Python Requirements.
    - **JavaScript**:
        - Include JSDoc comments for functions, classes, and complex logic.
        - Minimum docblock info: `@param`, `@returns`, `@throws`.
    - **General**:
        - Maintain concise Markdown documentation in the `docs/` directory for architecture, setup, API usage, etc.
        - Document complex algorithms or business logic with clear explanations and examples.

## Database Requirements
    - **Primary Database**: Firebase Firestore (NoSQL Document Database)
    - **Interaction**: Use the `firebase-admin` Python SDK for backend operations.
    - **Data Modeling**:
        - Design data structures appropriate for a NoSQL document store (denormalization where beneficial for read performance, careful consideration of queries).
        - Clearly define schemas for collections and documents, even if not strictly enforced by Firestore itself.
    - **Security Rules**: Implement robust Firestore security rules to protect data.
    - **Indexing**: Define necessary composite indexes in Firebase console for complex queries.

## AI Services Integration
    - **Primary AI Service**: Google Gemini & xAI Grok
    - **Client Library**: Utilize `google-genai` and `xai-sdk`.
    - **API Key Management**:
        - API keys MUST NOT be hardcoded.
        - Load keys securely via environment variables or a configuration service (as handled by `core.config.settings.py`).
        - Ensure API keys are included in `.gitignore` if stored in local files (e.g., `.env`).
    - **Usage Guidelines**:
        - Specify model versions explicitly (e.g., `GEMINI_MODEL="gemini-2.5-flash"`, `XAI_MODEL="grok-beta"`).
        - Implement retry mechanisms for API calls to handle transient network issues.
        - Be mindful of rate limits and implement appropriate backoff strategies.
        - Log API requests and responses (excluding sensitive data) for debugging and monitoring.
        - Consider cost implications: choose models appropriate for the task, optimize prompt lengths, and monitor usage.
    - **Error Handling**: Handle API-specific errors gracefully (e.g., authentication errors, rate limit errors, model overload).

## Security Considerations
    - **Input Sanitization**: Sanitize all user inputs on the frontend and backend to prevent XSS, injection attacks, etc.
    - **Parameterized Queries/SDK Usage**: When interacting with Firebase, use the SDK methods which inherently protect against NoSQL injection vulnerabilities. Do not construct queries by string concatenation with user input.
    - **Content Security Policy (CSP)**: Implement a strong CSP to mitigate XSS and other injection attacks.
    - **Cross-Site Request Forgery (CSRF)**: Use CSRF protection mechanisms for FastAPI if forms are submitted from traditional HTML forms (FastAPI typically relies on token-based auth for APIs which mitigates this for API endpoints).
    - **Secure Cookies**: If using cookies, ensure they are set with `HttpOnly`, `Secure` (in production), and `SameSite=Strict` or `SameSite=Lax` attributes.
    - **Authentication & Authorization**:
        - Implement robust authentication for user access.
        - Enforce role-based access control (RBAC) or permission checks for sensitive operations.
    - **Dependency Security**: Regularly scan project dependencies (Python and JavaScript) for known vulnerabilities using tools like `pip-audit` (Python) or `npm audit` / `yarn audit` (if frontend dependencies were managed via npm/yarn).
    - **API Key Security**: Protect API keys for OpenAI, Firebase, and other services. Do not commit them to the repository.
    - **Logging & Monitoring**: Implement detailed internal logging and monitoring to detect and respond to security incidents. Log security-relevant events.
    - **Firebase Security Rules**: Crucial for protecting data in Firestore and Firebase Storage. Ensure rules are restrictive and well-tested.
    - **Rate Limiting**: Implement rate limiting on API endpoints to prevent abuse, as seen with `RateLimiter` in `infrastructure.external_services.rate_limiter`.
