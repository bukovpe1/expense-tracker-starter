# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project context

This is the starter project for a Claude Code course. The app is a small React 19 + Vite expense tracker. It intentionally has a bug, poor UI and messy code, which get fixed step by step over the course. Expect it to be refactored gradually rather than rewritten all at once.

## Commands

```bash
npm install       # required first; `vite` is not available until dependencies are installed
npm run dev       # dev server at http://localhost:5173
npm run build     # production build to dist/
npm run preview   # serve the production build
npm run lint      # ESLint (flat config in eslint.config.js)
```

There is no test framework configured.

## Architecture

- `src/main.jsx` mounts `<App />` in `StrictMode`.
- `src/App.jsx` owns the `transactions` array (seed data in `useState`, nothing persisted) and the module-level `categories` list. It renders three children:
  - `Summary` computes income, expenses and balance from `transactions`.
  - `TransactionForm` keeps its own input state and passes a finished transaction object (with `amount` as a number) to `onAdd`.
  - `TransactionList` keeps its own filter state (type and category) and renders the filtered table. Each row has a Delete button that asks for confirmation with `window.confirm` and then calls `onDelete(id)`.
- Styling uses plain CSS in `src/App.css` and `src/index.css`, with class names like `summary-card`, `income-amount` and `expense-amount`.

## Known issues (deliberate course material)

- In the seed data, "Freelance Work" has type `expense` but category `salary`.

## Lint notes

- `no-unused-vars` ignores identifiers that match `^[A-Z_]`.
- `eslint-plugin-react-refresh` (Vite preset) expects component files to export only components.
