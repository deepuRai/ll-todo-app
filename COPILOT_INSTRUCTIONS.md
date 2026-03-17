# GitHub Copilot — Project & Code Review Instructions

Purpose
- Provide an automated assistant (Copilot / reviewer) with focused guidance for reviewing and contributing to this Next.js todo app.

Project overview
- Frameworks: Next.js v15, React 19 (RC), TypeScript 5
- Runtime: repository uses Bun in scripts (dev/test). Dependencies: `next`, `react`, `react-dom`, `zustand`.
- Key folders:
  - `app/` — Next.js app routes, layout, global styles
  - `app/components/` — UI components: `AddTodoForm`, `TodoItem`, `TodoList`
  - `app/lib/logic/` — business logic, `todoLogic.ts`
  - `app/lib/store/` — state management (`todoStore.ts`, `StoreProvider.tsx`)
  - `app/lib/types/` — shared TypeScript types
  - `tests/` — unit tests for logic and store

How to run locally (Windows PowerShell)
- If using Bun (recommended if available):
  - Install Bun (if not present) following Bun docs.
  - bun install
  - bun run next dev
  - bun test
- Alternative with Node/npm (if Bun unsupported):
  - npm install
  - npm run dev (may require adjusting `dev` script in `package.json` to `next dev`)

Primary goals for reviews
- Correctness: app functions as intended (add/remove/toggle todos), business logic matches tests.
- Types: TypeScript types are complete and accurate; check `@types` versions vs React/Next versions.
- Tests: unit tests cover logic and store; ensure tests are deterministic and meaningful.
- Runtime compatibility: Bun-specific scripts and `@types/bun` — flag issues if developer environment is Node-only.
- Security & data validation: sanitize user input, avoid unsafe client-side operations.
- Performance: avoid unnecessary renders; check use of keys, memoization when appropriate.
- Accessibility: forms and interactive elements must include accessible attributes (labels, roles).

Code review checklist (concrete items)
- Project structure: ensure components are small, single-responsibility.
- Type safety: no implicit any; explicit return types for exported functions where useful.
- Tests: every bugfix or new feature includes unit tests; tests pass locally.
- Linting & formatting: run `next lint` and project formatting rules.
- Dependencies: ensure dependencies and devDependencies are appropriate and versions compatible (React 19 vs `@types/react` ^18).
- Scripts: validate scripts in `package.json` (the current `dev` script looks like `bun --bun run next dev` — recommend `bun run next dev` or `next dev` depending on runtime).
- Edge cases: empty todo text, duplicate todos, persistence across reloads (if implemented), error handling.
- Accessibility: keyboard navigation, focus management, label elements.

PR review guidance
- Request a short description of behavior changes and provide reproduction steps.
- Ask for unit tests or a failing test for bugfixes.
- Prefer small, focused PRs.
- When suggesting code changes, include a minimal patch or diff and explain rationale.

Common issues to flag
- Mismatched TypeScript types for React 19 vs `@types/react` ^18.
- Bun-only commands that prevent running with Node/npm.
- Missing test coverage for core logic in `todoLogic.ts` and `todoStore.ts`.
- Unnecessary re-renders in component list rendering.

Formatting & style
- Follow project's TypeScript/ESLint rules and Next.js conventions.
- Keep component props minimal and well-typed.

References
- Next.js docs, React docs, Bun docs, TypeScript handbook.

If you want, I can also:
- Add a CI job example (GitHub Actions) to run lint/tests on PRs.
- Propose concrete package.json fixes (scripts/types alignment).
