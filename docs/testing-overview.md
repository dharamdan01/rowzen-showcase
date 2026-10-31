# Rowzen Testing Overview

[← Back to overview](../README.md) · [Features](features.md) · [User guide](user-guide.md)

This is a **public summary of verification recorded in the supplied project README**. It is not a fresh test execution or an independent production audit.

## Reported verification results

| Date in supplied README | Test scope | Recorded result | Qualification |
|---|---|---|---|
| **November 1, 2026** | Vitest unit/integration suite, Node 22 | **781 passed, 0 failed, 0 skipped, across 90 files** | Reported as the latest local run in that checkout |
| **October 31, 2026** | Full Playwright E2E run against a local hosted-mode build | **462 passed** | AI provider responses were mocked; this does not verify live hosted inference |
| At time of that README | Deployed Groq / Redis AI inference | **Not verified end to end** | No claim of working production AI follows from mocked E2E tests |

The supplied README says the Playwright suite **was not rerun for the November 1 README update**. Therefore, 781 and 462 refer to different recorded executions and should not be combined into a single run total.

## Areas covered by the test approach

The application documentation describes unit, integration, and browser testing around these areas:

| Area | Behaviors under test |
|---|---|
| CSV processing | Parsing, upload limitations, and input feedback |
| Configuration | Column mappings, required fields, types, keys, and relationships |
| Deterministic validation | Duplicate keys, missing references, type/rule violations, dependency cycles, and readiness semantics |
| Reports | Issue exploration, analytics, saved summaries, and report output |
| Corrections | Inline edits, undo/redo, What-If preview, and revalidation |
| AI contracts | Structured responses, invalid output handling, evidence grounding, and unavailable-provider paths |
| Export formats | Reports, corrected CSV, schema diagrams, and database-specific artifacts |
| Authentication and authorization | Session checks and resource ownership boundaries |
| UI flows | Responsive screens and end-to-end workspace interactions |

These are documented coverage *areas*, not individually verified pass counts. Exact assertions and current results belong to the private source repository's test reports.

## Testing tools

- **Vitest:** unit and integration tests.
- **Playwright:** browser end-to-end workflows.
- **ESLint and TypeScript:** static checks.
- **Production build:** framework and dependency integration checks.
- **Mocked AI:** controlled feature-path tests without relying on external model availability.

The source project README documents `npm test`, `npm run test:e2e`, `npm run test:coverage`, `npm run lint`, and `npm run build` as project scripts. These are **source-code commands**, not commands that can be run from this documentation-only showcase repository.

## What the reported tests do not prove

1. **Live AI operation:** Mocked Groq responses do not prove working end-to-end hosted inference or provider reliability on the deployed site.
2. **Import success:** Rowzen performs preflight checks and generates artifacts. Tests do not establish that any particular export will import successfully into a real production database.
3. **Comprehensive constraint simulation:** The engine does not model every database rule, live transaction, or target state.
4. **Independent security certification:** The supplied README explicitly says the student project has not undergone an independent security audit or earned compliance certification.
5. **Persisted raw datasets:** Saved report summaries are not evidence that full CSV content is stored or recoverable from Rowzen's database.

## Safe verification practices

- Use synthetic datasets and isolated non-production test environments.
- Do not execute stateful E2E tests against a live production database.
- Keep browser storage-state files, cookies, API credentials, and test-generated secrets out of public repositories and logs.
- Treat an unavailable external AI provider as a separate condition from deterministic validation failures.
- Clearly separate passed, failed, skipped, and not-run checks whenever publishing new results.

## Future updates

When the application is retested, update this page with the **actual execution date, environment, commands, totals, and unresolved limitations**. Do not silently carry forward older counts as the latest test evidence.

