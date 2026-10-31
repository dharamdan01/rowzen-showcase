# Rowzen Testing Overview

[← Back to overview](../README.md) · [Features](features.md) · [User guide](user-guide.md)

This page summarizes Rowzen's testing approach and the **evidence available for this public showcase**. The maintainer reports that all currently completed test suites pass and that all three AI features work in both local development and the deployed application. This documentation update did **not** execute the private source repository's test suites.

## Current status

| Area | Latest reported status | Evidence boundary |
|---|---|---|
| Automated tests | **Passing**, per maintainer confirmation | Exact latest counts, execution date, and machine-readable results were not supplied for this update |
| Local AI functionality | **Working**, per maintainer confirmation | All three assistants tested by the maintainer |
| Deployed AI functionality | **Working**, per maintainer confirmation | Hosted Groq inference works on the live Rowzen application |

**Do not treat the historical numbers below as the latest run totals.** New pass counts should be published only from actual test output or an updated test report.

## Previously documented runs (historical)

| Recorded date | Test scope | Recorded result | Context |
|---|---|---|---|
| **November 1, 2026** | Vitest unit/integration suite, Node 22 | **781 passed, 0 failed, 0 skipped, across 90 files** | Historical result from the supplied source README |
| **October 31, 2026** | Playwright E2E, local hosted-mode build | **462 passed** | AI responses mocked in this E2E run; live inference was subsequently confirmed separately by the maintainer |

These are two distinct recorded executions, not a combined run. The supplied README did not contain a later machine-readable report with updated totals.

## Tested feature areas

The source documentation describes unit, integration, and browser testing across the following areas:

| Area | Behaviors covered |
|---|---|
| CSV processing | Parsing, upload limits, input validation, and feedback |
| Configuration | Column mappings, required fields, types, keys, and relationships |
| Deterministic validation | Duplicate keys, missing references, type/rule violations, cycles, and readiness semantics |
| Reports | Issue exploration, analytics, saved summaries, and exports |
| Corrections | Inline edits, undo/redo, What-If preview, and revalidation |
| AI contracts | Structured responses, evidence checks, invalid-output and unavailable-provider handling |
| Database outputs | Reports, corrected CSV, schema diagrams, and target-specific exports |
| Authentication and authorization | Session checks and project/report ownership |
| UI workflows | Responsive layouts and end-to-end interactions |

These are documented coverage areas, not independent proof that every possible scenario is tested.

## Verification tools

- **Vitest:** unit and integration tests.
- **Playwright:** browser end-to-end workflows.
- **ESLint and TypeScript:** static analysis and type checks.
- **Next.js production build:** build-time compatibility checks.
- **Mocked AI responses:** deterministic automated tests of UI/provider contracts.
- **Live AI checks:** separate runtime verification of the local Ollama and hosted Groq flows, as reported by the maintainer.

The source project documents `npm test`, `npm run test:e2e`, `npm run test:coverage`, `npm run lint`, and `npm run build`. These scripts belong to the **private application repository** and cannot be executed from this documentation-only showcase.

## How to interpret the results

- **Automated tests and live inference are different checks.** Mocked tests verify behavior under controlled responses. The maintainer separately confirmed that the deployed AI features now work with hosted inference.
- **Passing preflight tests does not prove successful import into every target database.** Rowzen does not execute the final database import.
- **Passing tests does not amount to independent security certification.** No such certification is claimed.
- **Saved report summaries are not persisted CSV datasets.** A history entry cannot reconstruct every record and local correction.
- **An external provider can still fail temporarily.** Groq and supporting services are dependencies of hosted AI requests.

## Safe testing practices

- Use synthetic CSV fixtures and isolated non-production environments.
- Do not execute stateful E2E tests against production databases.
- Keep browser storage-state files, session cookies, API credentials, and connection secrets out of public repositories and logs.
- Record failed, skipped, not-run, and passed checks separately.
- Verify hosted AI with real requests in addition to mocked feature tests.

## Publishing new results

After a future full verification, update the current-status table using the **actual run date, environment, commands, totals, and any blockers**. Replace historical counts only when newer test artifacts are available; do not estimate counts or silently carry them forward.
