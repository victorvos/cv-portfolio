---
description: Mobile-First Frontend Optimization & Development Workflow
---

# Mobile-First Frontend Workflow

This workflow guides the development of a responsive, mobile-first web application using FastAPI, Jinja2, and Vanilla CSS/JS. Ideally, we aim for a "Reddit-app-like" feel.

## 1. Analysis & Structure
- [ ] **Identify the Component**: Isolate the UI part (e.g., "News Card", "Navigation Bar").
- [ ] **Mobile Layout First**: Visualize the component on a narrow screen (375px width). Stack elements vertically by default.
- [ ] **HTML Structure**: Ensure semantic HTML5.
    - Use `<nav>`, `<article>`, `<header>`, `<footer>`.
    - Avoid deep nesting if possible.

## 2. CSS Architecture (Mobile-First)
- [ ] **Base Styles**: Write CSS for the **mobile view** in the root class.
    ```css
    .card {
        display: flex;
        flex-direction: column; /* Default for mobile */
        padding: 10px;
    }
    ```
- [ ] **Desktop Enhancements**: Use `min-width` media queries to adjust for larger screens.
    ```css
    @media (min-width: 768px) {
        .card {
            flex-direction: row; /* Desktop adjustment */
        }
    }
    ```
- [ ] **Variables**: Use CSS variables in `universal.css` for consistency (colors, spacing).
- [ ] **Touch Targets**: Ensure all interactive elements (buttons, links) are at least **44x44px** on mobile.

## 3. Component Implementation
- [ ] **Jinja2 Macros/Includes**: If a UI element is used twice, move it to `templates/components/`.
- [ ] **Scoped CSS**: If a component is complex, create a dedicated CSS file (e.g., `static/css/components/card.css`).

## 4. Interactivity (App-Like Feel)
- [ ] **Feedback**: Add `:active` states for immediate touch feedback.
- [ ] **AJAX/Fetch**: Avoid full page reloads for small actions (upvotes, saves).
    - Use `fetch()` in `static/js`.
    - Update DOM immediately (optimistic UI) before waiting for server response.
- [ ] **Transitions**: Use `transition: transform 0.2s` for smooth state changes.

## 5. Verification Checklist
- [ ] **Viewport Testing**:
    - Mobile (375px) check.
    - Tablet (768px) check.
    - Desktop (1024px+) check.
- [ ] **Touch Test**: Verify buttons are clickable with fingers (no overlapping).
- [ ] **Dark Mode**: Toggle theme and ensure no hardcoded colors break accessibility.
