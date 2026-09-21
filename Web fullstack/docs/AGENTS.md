# AGENTS.md

This file provides guidance to AI coding agents working in this repository.
All paths in this document are relative to the repository root.

## Required reading

Before planning, reviewing, or modifying this project, read
[docs/GENERIC_RULES.md](docs/GENERIC_RULES.md) in full and apply it alongside
this file. The link is an explicit reading requirement; do not assume your
tool automatically imports linked Markdown files.

GENERIC_RULES.md contains reusable working rules. This file adds the project's
web conventions and spec-driven workflow. For repository conventions,
project-specific rules refine the generic defaults. Neither file overrides
the user's explicit instructions or the agent's higher-priority instructions.
If documents conflict in a way that affects behavior or scope, clarify the
conflict before implementing the affected part.

## Project

Modern Web Application built with a component-based framework (e.g., React/TypeScript)
following a spec-driven development workflow.

- The existing core features (like `Home` or `Dashboard`) are the reference
  for new features. Inspect their implementation before extending the app.

## Commands

Run commands from the repository root using the project's package manager.

```bash
npm run dev          # Start the local development server
npm run build        # Build for production and verify compilation
npm run lint         # Run linter and formatter (e.g., ESLint/Prettier)
npm run test         # Run local unit tests (e.g., Vitest/Jest)
npm run test:e2e     # Run end-to-end tests (e.g., Cypress/Playwright)
npm run db:migrate   # Run database migrations (if aplicable)
```

Local tests live alongside components (e.g., `*.test.tsx`) or in `src/tests`;
E2E tests live in their dedicated root directory. If build scripts change, inspect the available `package.json` scripts and use the appropriate task.

For code changes, `run npm run` lint and `npm run build` before reporting completion.
Run relevant unit and E2E tests when acceptance criteria require behavior validation. Report any checks that could not run and the reason.


## Spec-driven workflow

### Reference documents

Each template carries its own instructions for the agent, its section
structure, and its identifier scheme. Read the template in full and follow it;
this file does not restate its content and must not contradict it.
- `docs/SPEC_TEMPLATE.md`: copy to the feature's `SPEC.md` when creating or updating a specification. It owns the spec's sections, its RF- requirement and `CA-` acceptance-criteria identifiers, and its approval states.

 - `docs/PLAN_TEMPLATE.md`: copy to the feature's `PLAN.md` once the specification is approved. It owns the plan's sections and approval states. Reference requirements and criteria by their spec identifiers.

 - `docs/WEB_GUIDELINES.md`: consult when writing or reviewing requirements, acceptance criteria, the technical plan, and web validation. Consider DOM state retention, connectivity, browser storage persistence, responsive design, accessibility (a11y), API error handling, database transactions, and security. Apply only relevant items; clarify undefined product behavior.

Preserve each template's structure and its embedded comments in the copy. Do not
rewrite the shared templates for an individual feature.

## Feature documents 
Keep each feature's documents together:
 * docs/features/<feature-name>/SPEC.md
 * docs/features/<feature-name>/PLAN.md
 * docs/features/<feature-name>/TASKS.md

## Sequence
Each stage is gated by the previous document's state. A document is only
Aprobada/Aprobado when the user says so.

 1. Specification: complete `SPEC.md` from `docs/SPEC_TEMPLATE.md`, collaboratively. Do not start the plan until the user approves the spec.
 2. Plan: write `PLAN.md` from `docs/PLAN_TEMPLATE.md` for the approved specification. Do not start tasks until the user approves the plan.
 3. Tasks: derive `TASKS.md` from the approved plan. Small, ordered, verifiable checkboxes.
 4. Implementation: execute the tasks within the agreed scope. Authorization to implement must be explicit. Update task status as work progresses.
 5. Validation: verify acceptance criteria with appropriate evidence and record the result in `TASKS.md`.

If implementation reveals a requirement gap, clarify the affected behavior and update the relevant documents before continuing.

## Architecture
Full Stack architecture with clear boundaries between Client (Frontend) and Server (Backend). The baseline is wired with this structure:
| Path | Responsibility |
|---|---|
| src/components/ | Pure, stateless UI components (Client-side) |
| src/app/ or src/pages/ | Stateful entry points and UI routing (Client/Server-side rendering) |
| src/api/ or server/ | API route handlers, REST/GraphQL endpoints (Server-side) |
| src/services/ | Business logic, called by API routes or Server Actions |
| src/database/ | ORM configurations (e.g., Prisma, Drizzle), schemas, and migrations |
| src/types/ | Shared TypeScript interfaces and validation schemas (e.g., Zod) |


Layer dependencies & Full Stack boundaries
 * Client-Side Restrictions: UI components must NEVER import server-only modules (like `fs`, `crypto`, or ORM clients). They must communicate with the database exclusively through API endpoints or Server Actions.
 * Server-Side Validation: Never trust client input. All incoming API payloads and parameters must be strictly validated on the server using schema validation (e.g., Zod) before processing.
 * Business Logic: Keep route handlers (controllers) thin. Delegate complex operations and database queries to the `services/` layer.

Database and ORM
 * Define all database schemas centrally. Do not execute raw SQL queries unless strictly necessary for performance, preferring the project's chosen ORM/Query Builder.
 * Treat schema modifications as critical changes. If a feature requires new tables or columns, explicitly include the migration steps in the `PLAN.md`.

Security and Environment
 * Secrets: Never hardcode API keys, database URLs, or secrets in the codebase. Use environment variables (e.g., `process.env.DATABASE_URL`) and document required variables in `.env.example`.
 * Authentication/Authorization: Protect sensitive API routes by verifying the user's session or token before executing any logic. Ensure ownership checks are performed (e.g., User A cannot delete User B's data).

State and UI
 * Handle expected API failures gracefully. Reflect network, authorization, and validation errors in the UI state (Loading, Empty, Error, Success) as required by the spec.
 * Avoid inline CSS. Use the project's design system and global variables.

## Completion report

Summarize the implemented behavior, the affected feature documents, and the
validation results. Link acceptance criteria to evidence in `TASKS.md`.
Clearly identify anything incomplete or unverified; do not present a test name,
an unexecuted command, or "should work" as proof of success.

