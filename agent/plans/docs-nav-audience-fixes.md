# Fix documentation navigation gaps and dataset audience accuracy

This ExecPlan is a living document. The sections `Progress`, `Surprises & Discoveries`, `Decision Log`, and `Outcomes & Retrospective` must be kept up to date as work proceeds.

This repository stores the planning standard in `agent/PLANS.md`. Maintain this ExecPlan in accordance with that document.

## Purpose / Big Picture

We need the published documentation to steer readers to the right pages and portray each dataset accurately. After these edits, newcomers will land on working navigation links, understand that GI-DAMPs is an adults-only sampling study, and see clear next steps for requesting data access and interpreting pipeline pages.

## Progress

- [x] (2025-11-01 14:22Z) Audit existing pages to confirm scope and capture any additional stray references.
- [x] (2025-11-01 14:26Z) Update `docs/index.md` so the Quick Start and structure table link to the actual dataset overview page.
- [x] (2025-11-01 14:28Z) Align every GI-DAMPs population description in `docs/datasets/index.md` and `docs/datasets/comparison.md` with the adults-only scope, including the decision helper bullets.
- [x] (2025-11-01 14:32Z) Expand `docs/getting_started.md` with a short, numbered access workflow that explains how to request credentials, where files live in G-Trac, and how refresh cadences are communicated.
- [x] (2025-11-01 14:37Z) Preface each dataset pipeline page with a brief prose summary of the transformations so readers are not forced to parse raw code before learning what the pipeline does.
- [x] (2025-11-01 14:46Z) Run `mkdocs build --strict` and fix any warnings that surface.

## Surprises & Discoveries

- Observation: `uv run mkdocs build --strict` failed until the cache directory was redirected inside the workspace.
  Evidence: Initial run raised `failed to open file ... .cache/uv/sdists-v9/.git: Operation not permitted`, and rerunning with `UV_CACHE_DIR=.uv-cache` succeeded.

## Decision Log

- Decision: Treat all GI-DAMPs documentation as adults-only unless specifically noted otherwise.
  Rationale: User confirmed GI-DAMPs does not include paediatric participants.
  Date/Author: 2025-11-01 / Codex

## Outcomes & Retrospective

All navigation targets now resolve, GI-DAMPs is consistently described as adults-only, access steps are clearer, and each pipeline doc opens with context before code. Strict MkDocs build passes after adjusting link formats and email targets, demonstrating the updates compile cleanly.

## Context and Orientation

The site is configured by `mkdocs.yml`, which exposes content from `docs/`. The landing page references `datasets/datasets_tabbed.md`, but only `docs/datasets/index.md` exists, so the link 404s. Within the dataset overview and comparison guides, GI-DAMPs alternates between “Adults and children” and “Adults only,” leaving readers unsure whether paediatric data is present. The Getting Started guide gestures towards governance but lacks explicit access steps. Pipeline pages such as `docs/pipeline/gidamps.md` embed full Python files without contextual summaries, which slows comprehension for analysts.

## Plan of Work

First, confirm there are no other broken dataset links by searching the repo. Edit `docs/index.md` to point Quick Start item 2 and the datasets row in the structure table at `datasets/index.md`, updating the link text if needed, and fix the support email formatting while there. In `docs/datasets/index.md` and `docs/datasets/comparison.md`, ensure every population description matches the adults-only scope described earlier in the GI-DAMPs section, adjusting comparison bullets and helper notes accordingly. Augment `docs/getting_started.md` with a concise “Access workflow” subsection that names the governance request path, expected approval steps, and where finalized CSVs can be found in G-Trac; mention how refresh notifications are communicated. For `docs/pipeline/gidamps.md`, `docs/pipeline/music.md`, `docs/pipeline/mini_music.md`, and `docs/pipeline/combined_music.md`, insert short introductory paragraphs ahead of the code fences summarising the pipeline’s purpose, inputs, and key transformations. After making the edits, run the mkdocs build in strict mode to surface any broken links or formatting issues, resolving anything that appears.

## Concrete Steps

Search for other references to `datasets_tabbed`:

    workdir=/Users/chershiongchuah/Developer/orca_docs
    rg "datasets_tabbed" docs

Update Markdown files as described in the plan. When edits are complete, validate the site:

    workdir=/Users/chershiongchuah/Developer/orca_docs
    uv run mkdocs build --strict

If `uv run` is unavailable, fall back to `poetry run mkdocs build --strict` or `mkdocs build --strict`, matching the project’s tooling.

## Validation and Acceptance

Acceptance requires that `mkdocs build --strict` finishes without warnings or errors, and that manual inspection of the rendered Markdown confirms the Quick Start “Datasets” link opens the dataset overview. The GI-DAMPs comparison rows must clearly label the study as adults-only, and the Getting Started page must provide a numbered access workflow detailing request and retrieval steps. Pipeline pages should now begin with readable summaries before any code listings.

## Idempotence and Recovery

Edits consist solely of Markdown updates, so rerunning the steps is safe. If validation fails, review the strict build output, adjust the affected Markdown, and rerun the build until it passes.

## Artifacts and Notes

- MkDocs strict build:
    UV_CACHE_DIR=.uv-cache uv run mkdocs build --strict
    INFO    -  Cleaning site directory
    INFO    -  Building documentation to directory: /Users/chershiongchuah/Developer/orca_docs/site
    INFO    -  The following pages exist in the docs directory, but are not included in the "nav" configuration:
      - pipeline/index.md
    INFO    -  Documentation built in 0.52 seconds

## Interfaces and Dependencies

Expect to use whichever packaging tool (`uv`, `poetry`, or plain mkdocs) the repo already supports. No additional third-party services are required beyond the local mkdocs build.
