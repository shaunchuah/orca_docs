# Common Data Dictionary for Orca Study Datasets

This ExecPlan is a living document. The sections `Progress`, `Surprises & Discoveries`, `Decision Log`, and `Outcomes & Retrospective` must be kept up to date as work proceeds.

Maintain this plan in accordance with `agents/PLANS.md`, which defines the required structure, tone, and level of detail for ExecPlans in this repository.

## Purpose / Big Picture

Researchers use the Orca documentation site (MkDocs Material) to understand datasets surfaced in G-Trac. Today the “Unified Data Dictionary” only lists a handful of legacy fields and no longer reflects the current GI-DAMPs, MUSIC, and Mini-MUSIC exports. After this work, a reader can open `docs/data_dictionary/index.md` (and the companion CSV) to see an accurate, field-by-field dictionary covering every column that the three study datasets share, including plain-language descriptions, data types, and enumerated value sets where applicable. They will also know how those fields map back to each study dataset.

## Progress

- [x] (2025-10-30 17:14Z) Drafted initial ExecPlan outlining research method and documentation updates.
- [x] (2025-10-30 17:18Z) Catalogued current data dictionary assets and dataset column listings to confirm baseline structure.
- [x] (2025-10-30 17:18Z) Computed common field intersection and profiled value types from example datasets.
- [x] (2025-10-30 17:24Z) Drafted common-field definitions and recorded them in agent/research/common_data_dictionary/draft_dictionary.md.
- [x] (2025-10-30 17:28Z) Updated MkDocs data dictionary assets and validated the site with `uv run mkdocs build`.

## Surprises & Discoveries

- Observation: `previous_tonsillectomy` includes `-1000` in GI-DAMPs, used as an explicit unknown response.
  Evidence: example_datasets/gidamps_sampling_2025-10-30.csv row for study_id `GID-11`.

## Decision Log

- Decision: Present the unified dictionary grouped by theme (demographics, labs, phenotyping, medications, investigations).
  Rationale: Thematic grouping mirrors how analysts browse related variables and keeps the Markdown tables readable while the CSV preserves the same order for downstream tooling.
  Date/Author: 2025-10-30 (Codex)

## Outcomes & Retrospective

- (2025-10-30 17:28Z) Unified data dictionary now documents 54 shared fields across GI-DAMPs, MUSIC, and Mini-MUSIC. Markdown and CSV sources stay in sync via generated assets, and the MkDocs build passes. Remaining follow-up: monitor future dataset exports for new common columns and extend the dictionary as needed.

## Context and Orientation

The repository documentation site is configured by `mkdocs.yml`, pointing the “Data Dictionary” navigation section at the Markdown files in `docs/data_dictionary/`. That directory currently holds:

- `index.md`, a Markdown table labeled “Unified Data Dictionary” that lists 13 fields with minimal descriptions.
- `data_dictionary.csv`, a CSV mirroring the same table.
- Dataset-specific column dumps (`gidamps_columns.md`, `music_columns.md`, `mini_music_columns.md`) showing raw column names for each study, embedded in Python-style lists.
- Abbreviation references (`abbreviations.md` and `.csv`) that may help with terminology.

Example datasets for the three studies live under `example_datasets/`:

- `gidamps_sampling_2025-10-30.csv`
- `music_main_2025-10-30.csv`
- `mini_music_main_2025-10-30.csv`

Each file is a comma-separated export with headers that correspond to the columns described in the dataset-specific Markdown files. The goal is to derive the intersection of these headers, confirm that each field truly appears in all three datasets, and then document their meaning and structure within `docs/data_dictionary/index.md` and `docs/data_dictionary/data_dictionary.csv`.

The project currently has no scripted process for deriving the common dictionary; updates are manual. Python 3 is available (verified via `python3 --version`). No additional dependencies should be introduced; the standard library (`csv`, `collections`, `statistics`, etc.) is sufficient for scanning columns and sampling values.

## Plan of Work

### Milestone 1 — Audit Current Documentation

Read the existing Markdown and CSV data dictionary assets to understand their structure, formatting conventions (tables with `Variable`, `Type`, `Values`, `Comments` columns), and how navigation links reference them. Cross-check dataset-specific column listings to confirm they match the headers in the example CSVs. Document any mismatches or formatting constraints (for example, whether lists should stay sorted alphabetically) so later edits preserve conventions.

### Milestone 2 — Derive Common Field Inventory

Write a short Python script (stored under `agent/research/common_data_dictionary/`) that loads the three CSV files, normalizes headers (strip whitespace, ensure lower-case comparisons where needed), and computes:

- The exact set of field names that occur in all three datasets.
- For each common field, inferred data type (e.g., integer, float, boolean, categorical string) based on the non-empty sample values across the files.
- Enumerations for categorical fields with manageable cardinality (for example, `sex`, `study_group`), noting when fields are effectively boolean (values like `1`/`0` or `yes`/`no`).

Persist the computed metadata to a JSON file (for example, `agent/research/common_data_dictionary/common_fields.json`) to make later doc edits reproducible and auditable. Capture a human-readable summary in a Markdown note (`summary.md`) within the same directory for quick reference during documentation edits.

### Milestone 3 — Author Field Definitions

Combine the inferred metadata with contextual definitions sourced from existing docs:

- Reuse descriptions already present in `docs/data_dictionary/index.md` where valid.
- Look at dataset-specific Markdown files and any references in `docs/pipeline/` or `docs/data_dictionary/abbreviations.md` to derive plain-language explanations for fields lacking documentation.
- For fields with numeric codes (e.g., Montreal classification), confirm value meanings from current docs and ensure enumerations are accurate.

Draft a structured list of field definitions (variable, type, allowed values, comments) that can be inserted into both the Markdown table and the CSV. Keep narrative notes of any assumptions or gaps in `agent/research/common_data_dictionary/summary.md` to update the `Surprises & Discoveries` or `Decision Log` sections as needed.

### Milestone 4 — Update Documentation Assets

Edit `docs/data_dictionary/index.md` to replace the outdated table with the complete common-field dictionary, keeping the four-column format and Markdown table syntax. Ensure ordering is either logical (grouped by theme) or alphabetical; document the choice in the `Decision Log`. Update `docs/data_dictionary/data_dictionary.csv` to match the Markdown content exactly so downstream consumers can download the structured data. If helpful, add cross-links or short paragraphs explaining how the common dictionary relates to the dataset-specific column lists, but avoid duplicating large tables elsewhere.

### Milestone 5 — Validate and Capture Evidence

Run `mkdocs build` from the repository root to ensure the docs site builds without warnings. Spot-check the generated `site/data_dictionary/index.html` (optional, by inspecting Markdown output) to verify table rendering. Record the `mkdocs build` command output and any relevant excerpts from the generated Markdown or CSV diffs in the `Artifacts and Notes` section. Update `Progress`, `Surprises & Discoveries`, and `Decision Log` with final outcomes, then summarize results in `Outcomes & Retrospective`.

## Concrete Steps

1. Catalogue existing docs

    Working directory: repository root.

    Review key files without modifying them to establish baseline content:

        sed -n '1,160p' docs/data_dictionary/index.md
        sed -n '1,40p' docs/data_dictionary/data_dictionary.csv
        sed -n '1,80p' docs/data_dictionary/gidamps_columns.md

    Note formatting conventions and any discrepancies in `Progress` or `Surprises & Discoveries`.

2. Prepare research workspace

    Create a dedicated area for scripts and notes:

        mkdir -p agent/research/common_data_dictionary

3. Compute common fields and metadata

    Use Python to derive intersection and basic profiling, saving results to JSON and Markdown for reuse:

        python3 - <<'PY'
        import csv, json, pathlib, statistics
        from collections import Counter, defaultdict

        data_dir = pathlib.Path("example_datasets")
        research_dir = pathlib.Path("agent/research/common_data_dictionary")
        research_dir.mkdir(parents=True, exist_ok=True)

        datasets = {
            "gidamps": data_dir / "gidamps_sampling_2025-10-30.csv",
            "music": data_dir / "music_main_2025-10-30.csv",
            "mini_music": data_dir / "mini_music_main_2025-10-30.csv",
        }

        headers = {}
        samples = defaultdict(list)

        for name, path in datasets.items():
            with path.open(newline="", encoding="utf-8") as fh:
                reader = csv.DictReader(fh)
                headers[name] = [h.strip() for h in reader.fieldnames]
                for idx, row in enumerate(reader):
                    if idx >= 250:
                        break
                    for field, value in row.items():
                        value = value.strip() if value is not None else ""
                        if value:
                            samples[field].append(value)

        common_fields = sorted(set(headers["gidamps"]).intersection(headers["music"], headers["mini_music"]))

        def infer_type(values):
            ints = 0
            floats = 0
            boolish = 0
            lowered = []
            for v in values:
                lowered.append(v.lower())
                try:
                    int(v)
                    ints += 1
                    continue
                except ValueError:
                    pass
                try:
                    float(v)
                    floats += 1
                    continue
                except ValueError:
                    pass
                if v.lower() in {"yes", "no", "true", "false"}:
                    boolish += 1
            if ints == len(values):
                return "int"
            if floats == len(values):
                return "float"
            if boolish == len(values):
                return "boolean"
            return "string"

        field_profiles = []
        for field in common_fields:
            values = samples[field]
            field_type = infer_type(values) if values else "string"
            counter = Counter(v.lower() for v in values)
            distinct = len(counter)
            top_values = counter.most_common(10)
            profile = {
                "field": field,
                "type": field_type,
                "distinct_values": distinct,
                "top_values": top_values,
            }
            field_profiles.append(profile)

        (research_dir / "common_fields.json").write_text(json.dumps({
            "datasets": headers,
            "common_fields": field_profiles,
        }, indent=2), encoding="utf-8")

        summary_lines = [
            "# Common Field Summary",
            "",
            "Derived from example_datasets on first 250 rows per file.",
            "",
            f"Total common fields: {len(common_fields)}",
            "",
        ]
        for profile in field_profiles:
            top_preview = ", ".join(f"{val} ({count})" for val, count in profile["top_values"])
            summary_lines.append(f"- {profile['field']}: type≈{profile['type']}; distinct≈{profile['distinct_values']}; sample values: {top_preview}")
        (research_dir / "summary.md").write_text("\n".join(summary_lines) + "\n", encoding="utf-8")
        PY

    Update `Progress`, and if unexpected header mismatches occur, log them.

4. Draft dictionary content

    Using the generated summary plus existing docs, compose a proposed table in `agent/research/common_data_dictionary/draft_dictionary.md` before touching published docs. Capture rationale for tricky fields (e.g., Montreal classifications, boolean encodings) for later reference.

5. Update published documentation

    Apply changes to `docs/data_dictionary/index.md` and `docs/data_dictionary/data_dictionary.csv`, ensuring both sources stay synchronized. Keep Markdown tables valid (header separator row with matching column count). Retain or improve introductory narrative that explains scope.

6. Validate site build

    From the repository root, run:

        mkdocs build

    Expect a successful build with exit code 0. If warnings appear (for example, about malformed Markdown tables), fix the docs and re-run.

7. Finalize plan sections

    Record command outputs, decisions (such as field ordering or type interpretation), and any surprises. Complete the `Outcomes & Retrospective` section with a concise summary of achievements and remaining follow-ups.

## Validation and Acceptance

The work is accepted when:

- `docs/data_dictionary/index.md` presents a Markdown table enumerating every field shared by the three study datasets with accurate types, value ranges/categories, and clear descriptions.
- `docs/data_dictionary/data_dictionary.csv` contains the same rows and columns as the Markdown table, enabling CSV download.
- The example datasets’ headers, when intersected, exactly match the documented variables (verified using the Python profiling output).
- `mkdocs build` succeeds without errors, indicating the documentation site can be regenerated with the new dictionary.
- The ExecPlan sections reflect the final state (Progress checklist accurate, Decision Log populated, Surprises noted if any, Outcomes summarised).

## Idempotence and Recovery

All analysis scripts operate on read-only copies of the example CSVs and write outputs to `agent/research/common_data_dictionary/`, so they can be rerun without side effects. Edits to Markdown and CSV files can be reverted via version control if needed. If `mkdocs build` fails due to table formatting, adjust the table and rerun until the build passes. No databases or external services are touched, keeping the process safe to repeat.

## Artifacts and Notes

- `agent/research/common_data_dictionary/common_fields.json` stores the profiled headers and value distributions.
- `agent/research/common_data_dictionary/summary.md` summarizes inferred types and sample values.
- `agent/research/common_data_dictionary/dictionary_entries.json` and `draft_dictionary.md` capture the curated definitions.
- `agent/research/common_data_dictionary/grouped_tables.md` and `grouped_data_dictionary.csv` preserve the themed presentation used in the published docs.
- Validation evidence: `uv run mkdocs build` (2025-10-30 17:28Z) completed without errors.

## Interfaces and Dependencies

- Tooling: `python3`, standard library modules (`csv`, `json`, `collections`), `mkdocs` CLI already available via project dependencies.
- Documentation: MkDocs Material theme driven by `mkdocs.yml`; ensure edits respect existing navigation structure.
- Data: `example_datasets/*.csv` for profiling; do not modify these source files.
