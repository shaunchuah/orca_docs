# Orca Documentation

Orca is a Dagster-powered data platform that unifies REDCap study exports into curated datasets stored in G-Trac. This repository hosts the MkDocs Material site that documents those datasets, their pipelines, and the governance policies that guide access.

## Documentation highlights

- Home and Getting Started pages summarise the platform, onboarding steps, and access workflow.
- Dataset guides cover GI-DAMPs, MUSIC, Mini-MUSIC, and comparative statistics across cohorts.
- Data dictionaries catalogue shared and study-specific variables, value mappings, and abbreviations.
- Pipeline pages trace each Dagster asset from source extraction through to the published CSV outputs.
- Policy and governance sections list attribution requirements, contacts, and known data limitations.

The live site is published at <https://shaunchuah.github.io/orca_docs/>.

## Repository layout

- `docs/` – Markdown content for every page referenced by `mkdocs.yml`.
- `mkdocs.yml` – Site configuration (navigation, theme, Markdown extensions).
- `example_datasets/` – Representative CSV snapshots for local exploration.
- `pyproject.toml`, `uv.lock` – Python project metadata and locked dependencies.
- `agent/` – ExecPlan framework, historical plans, and scratch space for research.

## Prerequisites

- Python 3.12 or newer.
- Optional but recommended: [uv](https://docs.astral.sh/uv/) for reproducible dependency management.

## Installation

Using uv:

```bash
uv sync
```

## Local workflows

- Lint and build the docs to ensure navigation and metadata are valid:

  ```bash
  uv run mkdocs build --strict
  ```

- Preview locally while editing (serves at <http://127.0.0.1:8000/> by default):

  ```bash
  uv run mkdocs serve --livereload
  ```

  If uv is unavailable, substitute `mkdocs build --strict` or `mkdocs serve`.

## Working with example datasets

Example CSVs in `example_datasets/` mirror the schema described in the docs. They are safe to copy into notebooks or scripts for local analysis, but avoid modifying them in place—treat them as read-only fixtures.

## Contributing

- Read `AGENTS.md` for project expectations and communication norms.
- Significant features or refactors must start with an ExecPlan following `agent/PLANS.md`. Store new plans in `agent/plans/` and keep them up to date as work progresses.
- Place temporary research artifacts inside `agent/` (for example, `agent/research/...`).
- Before opening a pull request, run the strict MkDocs build command above and resolve any warnings or broken links.

## Support

For dataset access or interpretation questions, see the contacts listed in `docs/dataset_governance.md`. Technical queries about the documentation tooling can be directed to the Orca engineering team at [shaun.chuah@glasgow.ac.uk](mailto:shaun.chuah@glasgow.ac.uk).
