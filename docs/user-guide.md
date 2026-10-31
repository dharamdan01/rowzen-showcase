# Rowzen User Guide

[← Back to overview](../README.md) · [Features](features.md) · [Testing overview](testing-overview.md)

Use Rowzen to find potential CSV import problems, review relationships, correct supported issues, and download preparation files **before** importing data into a database.

**Open the deployed application:** [rowzen.vercel.app](https://rowzen.vercel.app)

## Choose how to start

**Quick trial:** Open the public [rehearsal demo](https://rowzen.vercel.app/rehearsal). It supports one or two CSV files without sign-in.

**Full workspace:** Sign in with GitHub or Google, open **Projects**, create or select a project, and enter its workspace. The full workspace supports up to five CSV files, 1 MB each.

The steps below describe the workflow rather than promising exact button labels for every interface state.

## Step 1: Upload files

1. Open **Upload** in your workspace.
2. Select CSV files using the file picker or drag-and-drop area.
3. Review parsing feedback and preview the datasets.
4. Correct rejected inputs before continuing.

**Example:** Upload `customers.csv` and `orders.csv` to rehearse a relationship where orders reference customers. Use sample or synthetic data for public demonstrations.

## Step 2: Configure mappings and rules

1. Review the source column names and intended target fields for each dataset.
2. Configure expected data types and required fields.
3. Set primary or unique keys where needed.
4. Define foreign key relationships between uploaded datasets.
5. Review and apply the final configuration.

**Example:** `customers.customer_id` identifies a customer, while `orders.customer_id` references that identifier. If an order refers to a missing customer, the validation engine can report it.

You can save or reuse project-owned mapping templates.

### Use AI Schema Mapping & Drift Detection on the deployed app

1. Open [Rowzen](https://rowzen.vercel.app) and sign in.
2. Open your project and go to **Configure**.
3. Choose the dataset and review its mapping configuration.
4. Open **Schema Mapping & Drift Detection** and start an analysis using the available action.
5. Review any consent notice, then request suggestions.
6. Compare suggested source/target fields and possible drift against your intended schema.
7. Apply only the mappings you approve; discard unsuitable suggestions.

The deployed app uses hosted **Groq** inference, so you do **not** need Ollama installed on your computer to use this feature.

## Step 3: Run validation

Go to **Validate** and run the configured preflight checks. Rowzen evaluates required values, data types, keys, references, and dependency configuration.

A blocked or warning state means review is required. It does not mean a database import has occurred.

## Step 4: Review issues and investigate causes

In **Review**:

- Start with the validation summary and readiness status.
- Use Issue Explorer to find and filter individual problems.
- Inspect dataset analytics and error distribution.
- Explore the dependency graph for ordering and cycles.
- Inspect the schema diagram for fields and relationships.

### Use AI Root-Cause & Impact Analyzer on the deployed app

1. Run validation and open **Review**.
2. Select or focus on a relevant finding, where available.
3. Open **Root-Cause & Impact Analyzer** and request an analysis after reviewing any consent notice.
4. Read the proposed explanations and follow the linked supporting evidence.
5. Inspect related issues and dependencies to decide what to investigate next.

AI-generated causes and impacts are **hypotheses**, not independently confirmed causes. The deterministic results remain unchanged by the analysis.

## Step 5: Correct problems safely

1. Navigate to an affected cell using the issue details or correction workspace.
2. Inspect the original value before changing it.
3. Make a manual correction, or consider an AI repair strategy.
4. Use **What-If** to review the candidate against current validation rules when applicable.
5. Apply only a correction you understand and approve.
6. Inspect the updated validation results; use undo/redo or correction history if needed.

### Use AI Verified Smart Repair Planner on the deployed app

1. Open **Correct** and focus on a supported issue.
2. Open **Verified Smart Repair Planner** and request a repair suggestion, accepting any required consent prompt.
3. Review the proposed strategy. Provide any information the interface requests rather than accepting invented values.
4. Run the available **What-If preview** for a concrete candidate.
5. Compare original versus proposed values and the resulting validation findings.
6. Choose **Apply** only if the change matches your intended data; otherwise cancel or dismiss it.
7. Confirm automatic revalidation and the updated correction history.

A candidate passing deterministic rules is not proof that its value is correct for your business data.

## Step 6: Export results

| Need | Export to look for |
|---|---|
| Share validation findings | CSV or JSON report |
| Continue with corrected records | Corrected CSV |
| Prepare relational database artifacts | PostgreSQL or MySQL exports |
| Prepare document database artifacts | MongoDB definitions or JSONL records |
| Share schema visualization | SVG diagram |

Exports are downloaded artifacts. **Rowzen does not import them into your target database.** Review compatibility guidance before using the files elsewhere.

## Save results and reuse a project

Authenticated users can save supported validation summaries and access them in **Results**. Saved report history helps revisit previous outcomes.

**Important:** A saved summary is not a backup of CSV records. Uploaded rows and local corrections are not restored merely by opening a historical summary. Keep your original files and corrected exports separately.

## Common questions

**Do the AI features work on the deployed website?**  
Yes. The maintainer confirms that Schema Mapping & Drift Detection, Root-Cause & Impact Analysis, and Verified Smart Repair work in the deployed Rowzen app. Hosted inference uses Groq and does not require a local Ollama installation.

**Do I need to install Ollama?**  
Not to use the deployed application. Ollama is supported as a separate local inference option for development or locally configured use.

**What if an AI request fails?**  
Check the displayed error and retry if appropriate. Hosted inference depends on provider availability and request limits. You can still validate datasets, edit records manually, and export results without AI.

**Does Rowzen save my full CSV files to its database?**  
No. According to the documented design, raw CSV rows are processed in browser memory and are not persisted to PostgreSQL by default. Project metadata and report summaries can be saved.

**Does a “ready” status guarantee import success?**  
No. It reflects configured preflight checks, not live database constraints or transaction behavior.

**Why can't I reopen every row from an old report?**  
Saved history contains summaries, not the full original dataset or correction history.

**What if a CSV file is rejected?**  
Review the parser feedback, CSV format, file count, and 1 MB per-file limit, then try again.

## Further reading

See [Features](features.md) for the full capability map and [Testing overview](testing-overview.md) for the project's verification approach.
