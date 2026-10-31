# Rowzen Features

[← Back to overview](../README.md) · [User guide](user-guide.md) · [Testing overview](testing-overview.md)

Rowzen prepares CSV datasets for database imports through deterministic validation, controlled corrections, visual analysis, and AI-assisted recommendations. **The validation engine, not an AI model, determines whether configured rules pass or fail.**

## Six-step workspace

### 1. Upload CSV datasets

- Select or drag and drop CSV files.
- Work with **up to five CSV files**, each **up to 1 MB**, in the full workspace.
- Inspect parsed datasets and receive feedback on invalid input.
- Keep raw CSV records in the browser instead of persisting them in Rowzen's application database by default.

The public `/rehearsal` demo supports one or two CSV files.

### 2. Configure the expected schema

Users specify the rules that imported data should satisfy:

- Source-column-to-target-field mapping.
- Expected data types and required fields.
- Primary keys, including composite keys.
- Uniqueness constraints.
- Foreign keys and cross-dataset relationships.
- Reusable, project-owned mapping templates.

The **Schema Mapping & Drift Detection** assistant suggests mappings and possible schema differences for the user to review before applying changes.

### 3. Validate with a deterministic engine

| Validation area | What it helps detect |
|---|---|
| Required values | Missing values in required columns |
| Types | Values incompatible with configured field types |
| Primary and unique keys | Duplicated or invalid identifiers and uniqueness conflicts |
| Foreign keys | References absent from related uploaded datasets |
| Relationship configuration | Invalid or incompatible relationship definitions |
| Dependency analysis | Cycles and constraints on the recommended import order |

Validation results are reproducible and independent of AI suggestions. Readiness reflects the configured rules and checks actually performed.

### 4. Review findings and relationships

- Summary cards and dataset-level metrics.
- Issue Explorer with search, filtering, and pagination.
- Error distribution charts and dataset analytics.
- Dependency graph with relationship and import-order guidance.
- Separate schema/entity-relationship diagram showing fields, keys, and relationships.

The **Root-Cause & Impact Analyzer** adds evidence-linked hypotheses to help investigate existing findings. Possible causes are presented separately from verified validation facts.

### 5. Correct and revalidate

- Inline cell editing and original-versus-current values.
- Undo and redo with correction activity history.
- Deterministic **What-If** previews before committing a candidate change.
- Automatic revalidation after approved corrections.

The **Verified Smart Repair Planner** proposes a strategy. Rowzen checks a candidate with its deterministic engine, displays the before/after preview, and requires explicit user approval. A validated preview does not guarantee the candidate reflects the intended business value.

### 6. Export artifacts

| Export | Documented output |
|---|---|
| Validation reports | CSV and JSON |
| Corrected records | CSV |
| PostgreSQL | Schema SQL and supported optional record exports |
| MySQL | MySQL-compatible SQL and supported optional record exports |
| MongoDB | Collection definitions and optional JSONL records |
| Schema diagram | SVG |

Exports are generated files. Rowzen **does not connect to or execute imports on the target database**.

## Accounts, projects, and history

- Sign in with GitHub or Google.
- Create, edit, and delete projects.
- Save and reuse project-owned mapping templates.
- Save validation-run summaries and revisit report history.
- Access private project and report resources through authenticated, ownership-checked server operations.

**Persistence boundary:** Project metadata, mappings, relationship configuration, templates, and validation summaries can be stored in PostgreSQL. Raw CSV rows and local correction activity are not stored there by default. Reopening a saved summary does not restore the uploaded CSV workspace.

## AI features and inference options

| Assistant | Step | What the user reviews |
|---|---|---|
| **Schema Mapping & Drift Detection** | Configure | Suggested mappings and possible schema differences before Apply |
| **Root-Cause & Impact Analyzer** | Review | Explanations tied to validation evidence and related findings |
| **Verified Smart Repair Planner** | Correct | Suggested strategy, What-If comparison, and explicit Apply/Dismiss decision |

### Hosted inference: Groq

The deployed Rowzen application uses a **Groq-hosted AI provider** through a server-side inference route. The project's documented implementation uses structured input/output contracts, validates model responses, and applies shared request rate limits. Users can access the deployed AI features without installing Ollama.

**Current status:** The maintainer confirms that the three AI features work on the deployed application following production integration fixes. External provider outages or rate limits can still affect individual requests.

### Local inference: Ollama

The application also supports **Ollama** for local development. Earlier documented supported models include `qwen2.5:0.5b` and `qwen2.5:1.5b`, subject to the application's active model allowlist. Running local AI requires the selected model and Ollama service on the user's device.

### User control and safety

- AI requests use selected metadata after explicit consent, rather than sending raw CSV rows by default.
- Responses are checked against typed contracts and available evidence.
- Cancellation and stale-result handling protect the current workspace.
- Suggestions never silently change mappings or records.
- Core validation, manual correction, reports, and exports remain usable when AI is unavailable.

For step-by-step instructions, see the [User guide](user-guide.md).

## Design and product boundaries

Rowzen provides responsive interfaces, light/dark appearance, and accessible data visualizations. It does not simulate every database constraint, live transaction, or external database state. A preflight result cannot guarantee a successful import. A GraphQL export interface is not documented as available.
