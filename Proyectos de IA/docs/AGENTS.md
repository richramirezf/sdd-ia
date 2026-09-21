# AGENTS.md

This file provides guidance to AI coding agents working in this repository.
All paths in this document are relative to the repository root.

## Required reading

Before planning, reviewing, or modifying this project, read
[docs/GENERIC_RULES.md](docs/GENERIC_RULES.md) in full and apply it alongside
this file. The link is an explicit reading requirement; do not assume your
tool automatically imports linked Markdown files.

GENERIC_RULES.md contains reusable working rules. This file adds the project's
AI/ML conventions and spec-driven workflow. For repository conventions,
project-specific rules refine the generic defaults. Neither file overrides
the user's explicit instructions or the agent's higher-priority instructions.
If documents conflict in a way that affects behavior or scope, clarify the
conflict before implementing the affected part.

## Project

AI/ML project following a spec-driven development workflow. The scope covers
classical machine learning, deep learning, and applications built on large
language models (RAG, agents, fine-tuning), including their data pipelines,
evaluation, serving, and monitoring.

- Inspect the repository before assuming anything about it: `pyproject.toml`,
  `Makefile`, `README`, configuration files, and the existing modules define
  the actual stack, package manager, entry points, and conventions.
- The reference layout in **Architecture** below is a starting point, not a
  verified description of this repository. Correct it against the real files
  and follow what already exists; do not restructure the project to match it.
- The existing feature closest to the requested work is the reference for new
  work. Inspect its implementation, its data handling, and its evaluation
  before extending it.

## Commands

Run commands from the repository root using the project's configured
environment. Verify the real task names in `pyproject.toml`, `Makefile`, or the
CI configuration before using them; the commands below are the common baseline.

```bash
uv sync                                   # or: pip install -e ".[dev]" / poetry install
uv run pytest                             # Run the test suite
uv run pytest -m "not slow"               # Skip long-running training/eval tests
uv run pytest tests/test_features.py::test_name   # Run a single test
uv run ruff check .                       # Lint
uv run ruff format .                      # Format
uv run mypy src                           # Type check, if configured
uv run python -m src.training.train --config configs/<name>.yaml
uv run python -m src.evaluation.evaluate --run-id <id>
uv run jupyter lab                        # Exploratory work only
```

Tests live in `tests/` (unit, integration, data contract, and evaluation
tests). If the layout or the task runner differs, inspect the available
configuration and use the appropriate task. Do not introduce a new quality
tool or test framework as an unrelated change.

For code changes, run the linter, the type checker (if configured), and the
relevant tests before reporting completion. Run the full evaluation only when
acceptance criteria require a quality measurement, because it is usually slow
and may be expensive. For documentation-only changes, verify content and
references without requiring an environment or a model. Report any checks that
could not run and the reason.

### Expensive and irreversible operations

Training runs, hyperparameter searches, fine-tuning, large data downloads,
paid API calls, and deployments consume real money and real time, and some of
them mutate external systems.

- Never start them as a side effect of another task, and never start them to
  "see if it works". Authorization must be explicit and specific.
- Propose first: what will run, on how much data, for how long, at what
  estimated cost, and which limit or timeout will bound it.
- Prefer the cheapest step that answers the question: a data sample, a dry run,
  a smaller model, cached results, or a mocked provider in tests.
- Set and honor explicit limits: iteration or epoch caps, token and budget
  caps, timeouts, and a maximum number of retries.
- Never loop over a paid API without a cap, and never disable a rate limit,
  a budget guard, or a safety check to make a run finish.
- Record what was actually executed, with its cost and duration, in the
  validation evidence.

## Spec-driven workflow

### Reference documents

Each template carries its own instructions for the agent, its section
structure, and its identifier scheme. Read the template in full and follow it;
this file does not restate its content and must not contradict it.

- `docs/SPEC_TEMPLATE.md`: copy to the feature's `SPEC.md` when creating or
  updating a specification. It owns the spec's sections, its `RF-` requirement
  and `CA-` acceptance-criteria identifiers, and its approval states. It also
  owns the measurable quality, latency, and cost targets that make AI
  acceptance criteria decidable.
- `docs/PLAN_TEMPLATE.md`: copy to the feature's `PLAN.md` once the
  specification is approved. It owns the plan's sections and approval states,
  including the AI-specific sections on evaluation, reproducibility, cost, and
  responsible use. Reference requirements and criteria by their spec identifiers.
- `docs/AI_GUIDELINES.md`: consult when writing or reviewing requirements,
  acceptance criteria, the technical plan, and validation. Consider data
  quality and licensing, splits and leakage, metrics and baselines,
  reproducibility, non-determinism, latency, cost, provider failures, output
  validation, abstention, adversarial input and prompt injection, privacy,
  bias, monitoring and drift, artifact lifecycle, prompting and RAG. Apply only
  relevant items; clarify undefined product behavior instead of inventing it.

Preserve each template's structure and its embedded comments in the copy. Do not
rewrite the shared templates for an individual feature.

### Feature documents

Keep each feature's documents together:

- `docs/features/<feature-name>/SPEC.md`
- `docs/features/<feature-name>/PLAN.md`
- `docs/features/<feature-name>/TASKS.md`

Use an existing feature directory when continuing its work.

### Sequence

Each stage is gated by the previous document's state. A document is only
`Aprobada`/`Aprobado` when the user says so: a complete document is not an
approved one, and the agent never changes that state on its own.

1. **Specification:** complete `SPEC.md` from `docs/SPEC_TEMPLATE.md`,
   collaboratively and section by section, following the template's own
   instructions. A spec without a measurable quality target, a baseline, and a
   defined evaluation set is not complete. Do not start the plan until the user
   approves the spec.
2. **Plan:** write `PLAN.md` from `docs/PLAN_TEMPLATE.md` for the approved
   specification, following the template's own instructions. Additionally,
   record whether subagents are needed and their bounded responsibilities; do
   not assume delegation is required or available. Identify every expensive
   operation the plan needs and its authorization point. Do not start tasks
   until the user approves the plan.
3. **Tasks:** derive `TASKS.md` from the approved plan. There is no shared
   template for it, so this file defines it: small, ordered, verifiable
   checkboxes, each with an identifier, objective, scope, dependencies, the
   spec criteria it resolves, and its validation method. Keep tasks concise
   enough to execute and detailed enough to determine when they are done. Mark
   tasks that trigger expensive runs so authorization is visible before execution.
4. **Implementation:** execute the tasks within the agreed scope, preserving
   the architecture below. Authorization to implement must be explicit; it is
   not implied by the documents' state. Update task status as work progresses.
5. **Validation:** verify acceptance criteria with appropriate evidence and
   record the result in `TASKS.md`, including any outstanding checks. For
   quality criteria, record the metric, the evaluation set and its size, the
   artifact version, the baseline compared, and the observed variation.

Do not treat a filled template as resolution of unanswered questions. Ask
about missing product decisions that affect behavior, quality targets, data
usage, or cost; resolve routine technical details from the code and established
conventions. Do not ask for renewed permission for steps the user has already
authorized.

If implementation reveals a requirement gap or contradiction — for example,
the agreed quality target is not reachable with the available data — stop that
part, report the finding with evidence, and update the relevant documents
before continuing. Keep the specification, plan, tasks, and resulting behavior
consistent. Never lower an agreed threshold silently to make a result pass.

## Architecture

Reference layout for an AI/ML project, with clear boundaries between data,
modeling, evaluation, and serving. Verify the real structure before relying on
this table, and follow the repository's existing organization.

| Path | Responsibility |
| --- | --- |
| `src/data/` | Loading, schema validation, cleaning, splitting, and dataset construction |
| `src/features/` | Reproducible feature transformations fitted on training data only |
| `src/models/` | Model definitions, training steps, and serialization |
| `src/training/` | Run orchestration, seeds, hyperparameters, and experiment tracking |
| `src/evaluation/` | Metric implementations, evaluation sets, baselines, and reports |
| `src/inference/` | Prediction, prompts, retrieval, tool calls, post-processing, and output validation |
| `src/api/` | Serving endpoints and their request/response contracts |
| `src/pipelines/` | Batch orchestration and CLI entry points |
| `src/monitoring/` | Prediction logging, drift and quality checks, cost accounting |
| `src/config/` | Typed settings, paths, and environment variables |
| `configs/` | Declarative experiment, training, and deployment configuration |
| `prompts/` | Versioned prompt templates and their evaluation cases |
| `notebooks/` | Exploration only; never imported by production code |
| `tests/` | Unit, integration, data-contract, and evaluation tests |
| `data/` | Raw, interim, processed, and external data; kept out of version control |
| `artifacts/` or `models/` | Trained artifacts and registries; kept out of version control |

### Layer dependencies

- `api -> inference -> models/evaluation` for contracts and metrics; `training
  -> data, features, models`.
- Evaluation must not depend on training internals. It consumes an artifact, a
  version identifier, and an evaluation set, so it can judge any candidate
  under the same conditions.
- Serving must not train, refit, or mutate artifacts. It loads a pinned version
  and applies the same preprocessing the artifact was trained with.
- Keep framework specifics (PyTorch, scikit-learn, LangChain, a provider SDK)
  inside their own layer. The API and pipeline layers depend on project
  interfaces, not on framework internals.
- Feature and preprocessing code must be shared between training and inference,
  or generated from one definition. Duplicated transformation logic is a
  training-serving skew defect, not a style preference.

### Data and leakage

- Validate data schemas at the boundary. Reject or explicitly handle unexpected
  columns, types, nulls, and out-of-range values instead of silently coercing them.
- Split before fitting anything: preprocessors, encoders, scalers, thresholds,
  feature selection, and hyperparameter choices are all fitted on training data only.
- Use time-based splits for temporal data and group by entity when a subject
  contributes multiple samples. Random splits leak in both cases.
- Keep the held-out test set untouched until final evaluation. Repeated tuning
  against it turns it into a validation set; report that honestly.
- Record dataset provenance, license, and the exact snapshot or hash used for
  every reported result.

### Notebooks and production code

- Notebooks are for exploration and communication. They are not the production
  path and must not be imported by it.
- Promote a notebook's logic into `src/` before it is used by a pipeline, an
  endpoint, or a reported result, and cover it with tests there.
- A notebook is not evidence of validation: it is not reproducible by another
  person without its execution order, state, and environment.

### Training and experiments

- Configuration as code: every run reads a declarative config plus resolved
  environment, and both are recorded with the run.
- Fix all sources of randomness with explicit seeds and record them. Where a
  seed cannot control the outcome, say so and report the observed spread.
- Track each run with its parameters, data version, code version, metrics, and
  artifact identifier. An untracked result cannot be reproduced or compared.
- Report the selected model against its baseline on the same evaluation set.
  Do not present the best of many runs as the expected performance.

### Evaluation and metrics

- Implement metrics as tested code, not as ad-hoc notebook calculations.
- State metric, evaluation set, its size, artifact version, baseline, and
  variation with every reported number. A number without that context is not evidence.
- Use small fixed fixtures for deterministic tests of metric and transformation
  code. Reserve full evaluations for the runs that justify their cost.
- Non-deterministic outputs need a defined comparison method: a reference
  evaluation set with a scoring rule, an assertion on structure rather than
  exact text, or a recorded human review. Asserting exact equality on generated
  text produces tests that fail randomly.
- Never relax a threshold, shrink an evaluation set, or exclude inconvenient
  samples to make a criterion pass. Report the shortfall instead.

### LLM applications, prompting, and RAG

- Treat prompts as versioned artifacts with their own evaluation cases, stored
  in `prompts/` or the equivalent. Do not bury prompt text in code paths where
  a change goes untracked.
- Validate every model output against a schema before use. Parse defensively,
  bound retries, and fail loudly when the output stays invalid.
- Treat model output and retrieved content as untrusted input: they must not
  trigger privileged actions, database writes, code execution, or data exports
  without independent validation.
- Enforce context limits explicitly: truncation, chunking, and retrieval counts
  are decisions with quality and cost consequences, not accidents.
- Ground answers in retrieved sources when the spec requires it, and expose
  citations or provenance rather than asserting correctness.
- Record the model identifier, prompt version, and generation parameters with
  each result, because provider models change or are retired without notice.
- Keep provider access behind a project interface so a model or vendor swap
  does not rewrite the application.

### Artifacts, deployment, and monitoring

- Store datasets and artifacts outside version control using the project's
  mechanism (DVC, LFS, a registry, or object storage). Never commit large
  binaries, model weights, or datasets.
- Deploy a pinned, identified artifact version. Keep the previous version
  available and document how to roll back.
- Log predictions with their inputs or a reference to them, the artifact
  version, the output, the confidence, the latency, and the cost, respecting
  the project's privacy and retention rules.
- Define the drift and quality checks that would reveal degradation, and what
  condition triggers a review, a retrain, or a rollback.

### Security, privacy, and responsible use

- Secrets and API keys come from the project's configuration mechanism and
  environment variables, documented in `.env.example`. Never hardcode them, and
  never place them in prompts, notebooks, logs, fixtures, or committed configs.
- Do not send personal or sensitive data to an external provider without
  verified authorization and a checked provider data policy. Default to the
  local or approved alternative when it exists.
- Do not log secrets, credentials, or more personal data than the retention
  policy allows. Apply minimization and anonymization before logging or
  storing samples for debugging.
- Respect dataset and model licenses. Record the license of every dataset and
  pretrained model used, and flag terms that restrict commercial use or
  redistribution.
- Isolate any code execution the model can trigger, and bound its permissions,
  filesystem access, and network access.
- Document intended use, known limitations, evaluated subgroup behavior, and
  uses that are explicitly not supported. Do not present a model as reliable
  beyond the conditions actually measured.

### Cost, performance, and environments

- Design for the environment that will run the code. Do not assume a GPU, a
  specific accelerator, or network access to a paid provider is available;
  verify and state what was used.
- Keep CI cheap and deterministic: small fixtures, no GPU, mocked providers,
  and long or expensive runs excluded by a marker. A test suite that cannot run
  in CI does not protect anything.
- Measure latency and cost rather than assuming them. Report p95 latency and
  cost per operation against the target in the spec.
- Cache and batch where the spec allows it, and make the cache key include
  every input that affects the result, including model and prompt versions.

## Completion report

Summarize the implemented behavior, the affected feature documents, and the
validation results. Link acceptance criteria to evidence in `TASKS.md`.
For quality criteria, report the metric, the evaluation set and its size, the
artifact and code versions, the baseline compared, the observed variation, and
the cost and duration of the runs actually executed.

Clearly identify anything incomplete or unverified; do not present a test name,
an unexecuted command, a training curve, a single example output, or "should
work" as proof of success. State explicitly which results are not reproducible
and why, and which validations were blocked by the environment, by cost limits,
or by missing data.
