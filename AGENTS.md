# Chained Echoes Guide - Agent Instructions

## Project Architecture

- Framework: Astro (SSR disabled, static site), TypeScript (Strict), Vanilla CSS.
- Core Layouts: `src/layouts/` contains `Layout.astro`, `WalkthroughLayout.astro`, and `DlcLayout.astro`.
- Global Styles: Reference `src/styles/global.css` for all CSS variables, tokens, and responsive breakpoints. Do not invent new colors.

## Coding Conventions

- **TypeScript:** Always define explicit `Props` interfaces. Return types must be explicit.
- **CSS:** Use BEM-like naming (`.quest-step`, `.step-title`). Rely on the existing design tokens in `global.css`.
- **Client-Side JS:** Always wrap browser-specific code in `if (typeof document !== "undefined")`.
- **Error Handling:** Do not use try/catch blocks. Prefer defensive null-checking for DOM elements (e.g., `if (button)`) and localStorage.

## Application State & Local Storage

- Base Game Progress Key: `chained-echoes-completed` (Stores JSON array of string IDs).
- Data Attributes: Use `data-guide-id` and `data-guide-title` on interactive DOM elements for tracking.

## CRITICAL: DLC Pages

Pages covering DLC content have entirely different rules:

- Must use the `.dlc-theme` class on the `<body>` tag.
- Accent colors switch from Gold to Teal (`#2dd4bf`).
- Uses a separate tracking key: `chained-echoes-dlc-completed`.

## Strict Communication Protocol

CRITICAL: Do not answer quickly without carefully analyzing the questions or requests first. Only answer or give suggestions if you are at least 97% confident in what your responses exactly match what the user needs. In case there is not enough information, the requests or questions are not clear in context, or there are too many responses that suit the context, you should ask follow-up questions to clarify exactly what the requirements are, and respond when there is enough context.
