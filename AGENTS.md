# Orca Documentation Project

This project is a documentation platform running on mkdocs-material that surfaces information on the datasets surfaced in G-Trac by Orca, which is a dagster-based data engineering platform. Currently it aggregates data from multiple redcap study databases, processes them, and stores the final datasets in G-Trac.

## ExecPlans

When writing complex features or significant refactors, use an ExecPlan (as described in `agent/PLANS.md`) from design to implementation. Write new plans to the `agent/plans` dir. Place any temporary research, clones, etc., in a subdirectory of `agent`.

## Do

- Ask clarifying questions if unsure about requirements.

## Don't

- Do not run the dev server unless asked to.
