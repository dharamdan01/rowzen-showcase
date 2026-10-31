# Rowzen Features

[← Back to overview](../README.md) · [User guide](user-guide.md) · [Testing overview](testing-overview.md)

Rowzen helps prepare CSV datasets for database import. It separates **deterministic checks** from **AI-assisted suggestions** and keeps record changes under user control.

## Six-step workspace

### 1. Upload CSV datasets

- Select or drag and drop CSV files.
- Work with **up to five CSV files**, each **up to 1 MB**, in the full workspace.
- Inspect parsed datasets and receive feedback on invalid input.
- Keep raw CSV records in the browser rather than persisting them in Rowzen's application database by default.

The public `/rehearsal` demo supports a smaller scenario involving one or two CSV files.

### 2. Configure the expected schema

Users specify the rules that imported data should satisfy:

- Source column to target field mapping.
- Expected data types and required fields.
- Primary keys, including composite keys.
- Uniqueness constraints.
- Foreign keys and cross-dataset relationships.
- Reusable, project-owned mapping templates.

An optional schema mapping assistant can suggest mappings or highlight possible drift. Suggestions require user review; they are not automatically applied.

### 3. Validate with a deterministic engine

Rowzen checks configured rules against uploaded records, including:

| Validation area | What it helps detect |
|---|---|
| Required values | Missing values in required columns |
| Types | Values incompatible with configured field types |
| Primary and unique keys | Duplicated or invalid identifiers and uniqueness conflicts |
| Foreign keys | References to records not present in related uploaded datasets |
| Relationship configuration | Invalid or incompatible relationship definitions |
| Dependency analysis | Cycles and constraints on the recommended import order |

Results come from the deterministic validation engine, not from AI judgments. A readiness result only reflects the checks performed and configured rules.

### 4. Review findings and relationships

The review workspace includes:

- Summary cards and dataset-level metrics.
- Issue Explorer with search, filtering, and pagination.
- Error distribution charts and dataset analytics.
- A dependency graph showing relationships and import-order guidance.
- A separate schema/entity-relationship diagram for fields, keys, and relationships.

The optional Root-Cause & Impact Analyzer suggests explanations grounded in available validation evidence. These explanations are hypotheses, not confirmed causal findings.

### 5. Correct and revalidate

Supported correction tools include:

- Inline cell editing and original-versus-current values.
- Undo and redo with correction activity history.
- Deterministic **What-If** previews before committing a candidate change.
- Automatic revalidation and updated results after approved changes.

The optional **Verified Smart Repair Planner** proposes a strategy. The application resolves and checks a candidate through its existing deterministic rules, shows a preview, and requires explicit approval. “Verified” does not mean business correctness is guaranteed.

### 6. Export the artifacts you need

| Export | Documented output |
|---|---|
| Validation reports | CSV and JSON |
| Corrected records | CSV |
| PostgreSQL | Schema SQL and supported optional record exports |
| MySQL | MySQL-compatible SQL and supported optional record exports |
| MongoDB | Collection definitions and optional JSONL records |
| Schema diagram | SVG |

Exports are generated files. Rowzen does **not** connect to or execute imports on the target database.

## Accounts, projects, and history

- Sign in with GitHub or Google, subject to provider configuration.
- Create, edit, and delete projects.
- Save and reuse project-owned mapping templates.
- Save validation-run summaries and revisit report history.
- Access private project and report resources through authenticated, ownership-checked server operations.

**Persistence boundary:** Project metadata, mappings, relationship configuration, templates, and validation summaries may be stored in PostgreSQL. Raw CSV rows and local correction activity are not stored there by default. Reopening a saved summary does not restore the uploaded CSV workspace.

## AI assistance: capabilities and boundaries

| Assistant | Step | User-controlled outcome |
|---|---|---|
| Schema Mapping & Drift Detection | Configure | Review suggestions before applying mappings |
| Root-Cause & Impact Analyzer | Review | Inspect evidence-linked explanations and investigate findings |
| Verified Smart Repair Planner | Correct | Preview a candidate with What-If and approve or dismiss |

The supplied application README describes typed AI contracts, response validation, explicit user consent, cancellation, and protection against stale responses. It documents **Groq** as a hosted provider and **Ollama** as a local provider. Hosted inference still depends on provider availability and configuration; its successful operation on the deployed site was not established in the supplied evidence.

## Design and data-handling principles

- Preflight before importing: no direct database writes to the intended target.
- Deterministic results remain the source of truth for configured validation rules.
- Raw CSV rows are processed in browser memory.
- AI requests use selected metadata after explicit consent, rather than raw CSV records.
- No automatic application of AI-suggested corrections.
- Accessible visualizations, responsive layouts, and light/dark presentation are part of the documented UI.

## Product boundaries

Rowzen does not simulate every database constraint, live transaction, or external target-database state. It does not guarantee a successful import. The supplied README does not describe a working GraphQL export interface.

