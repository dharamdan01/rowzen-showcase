# Rowzen User Guide

[← Back to overview](../README.md) · [Features](features.md) · [Testing overview](testing-overview.md)

Use Rowzen to identify potential CSV import problems, correct supported issues, and download preparation files **before** importing data into a database.

**Open the app:** [rowzen.vercel.app](https://rowzen.vercel.app)

## Choose how to start

**Quick trial:** Open the public [rehearsal demo](https://rowzen.vercel.app/rehearsal). It supports a limited scenario with **one or two CSV files** and does not require sign-in.

**Full workspace:** Sign in with an available GitHub or Google provider. Open **Projects** to create or select a project, then enter its workspace. The full workspace supports **up to five CSV files, 1 MB each**.

The steps below describe the workflow, not fixed button labels; controls may change as the interface evolves.

## Step 1: Upload files

1. Open the workspace's **Upload** step.
2. Select CSV files using the file picker or drag-and-drop area.
3. Check parsing feedback and preview the detected datasets.
4. Fix rejected file inputs before proceeding.

**Example:** Upload `customers.csv` and `orders.csv` to rehearse an import where orders reference customers. Use synthetic sample data when demonstrating the product publicly.

## Step 2: Configure mappings and rules

For each dataset:

1. Review the source column names and their intended target fields.
2. Configure expected data types and mark required fields.
3. Set primary or unique keys when applicable.
4. Define foreign keys that refer to another uploaded dataset.
5. Review the configuration before applying it.

**Example configuration:** `customers.customer_id` is the customer identifier; `orders.customer_id` refers to it. If an order refers to a customer ID absent from `customers.csv`, the foreign-key check can surface the problem.

You can reuse project-owned mapping templates where available. Optional AI mapping suggestions should be reviewed before applying changes.

## Step 3: Run validation

Go to **Validate** and run the configured preflight checks.

Rowzen evaluates required values, types, keys, references, and dependency configuration. A blocked or warning state means review is needed; it is not an indication that a database import has already occurred.

## Step 4: Review issues

In **Review**:

- Start with the summary and readiness information.
- Use Issue Explorer to find and filter particular problems.
- Inspect dataset analytics and the distribution of errors.
- Explore the dependency graph for import ordering and cycles.
- Inspect the schema diagram to check how fields and relationships are represented.

Where available, use **Root-Cause & Impact Analyzer** for supplementary evidence-linked explanations. Treat these as possible explanations, not verified causes or replacement validation results.

## Step 5: Correct problems safely

1. Navigate to the affected dataset or cell using the issue details and correction workspace.
2. Check the original value before editing.
3. Enter an intended correction, or review an optional AI repair strategy.
4. Use **What-If** to inspect the candidate change against current validation rules when applicable.
5. Approve only a change you understand, then inspect updated validation results.
6. Use undo/redo or correction history if you need to reconsider a change.

Do not invent missing IDs or assume a suggested replacement is correct merely because a validation rule accepts it. The intended value may require knowledge outside the uploaded files.

## Step 6: Export results

Choose the output appropriate to your next task:

| Need | Export to look for |
|---|---|
| Share a validation summary | CSV or JSON report |
| Continue with corrected rows | Corrected CSV |
| Prepare relational database artifacts | PostgreSQL or MySQL export |
| Prepare document database artifacts | MongoDB definitions or JSONL records |
| Share the visual schema | SVG diagram |

Exports are downloaded artifacts. **Rowzen does not import them into your target database.** Review compatibility and warnings before using them elsewhere.

## Save reports and reuse a project

Authenticated users can save supported validation summaries and access them through **Results**. Saved report history helps revisit the outcomes of earlier runs.

**Important:** A saved summary is not a backup of your CSV records. Raw rows and local corrections are not restored merely by reopening the summary. Keep your original files and corrected exports separately.

## Common questions

**Does Rowzen upload my complete CSV data to its application database?**  
According to the supplied project README, raw CSV rows are processed in browser memory and are not persisted in PostgreSQL by default. Project configuration and report summaries can be stored.

**Do I need AI to validate files?**  
No. Validation, manual correction, and exports rely on the deterministic workflow. AI is optional assistance.

**Why might an AI feature be unavailable?**  
Hosted inference depends on its configured provider and related services. Local Ollama mode requires a compatible model running on the user's own machine, with suitable browser permissions and origins. An unavailable assistant does not mean the preflight engine stopped working.

**Does “ready” mean a real database import will succeed?**  
No. It reflects Rowzen's configured preflight checks, not live target database constraints, transaction behavior, or production state.

**Why can't I reopen all rows from an old report?**  
Saved report history contains summaries, not the complete original dataset or full local correction activity.

**What if my CSV file is rejected?**  
Check the input feedback, CSV format, file count, and 1 MB per-file limit; then retry with a supported file.

## Next steps

See [Features](features.md) for a full capability map and [Testing overview](testing-overview.md) for what the supplied project verification does and does not establish.

