# Dataset Governance Policy

## Purpose

This policy establishes the governance framework for datasets engineered through Orca and surfaced in G-Trac. It defines accountabilities and processes that protect data quality, respect source-study obligations, and ensure compliant access for analytics teams.

## Scope

The policy applies to:

- All datasets ingested, transformed, or published by Orca into G-Trac or downstream analytical environments.
- Any derivative data products, dashboards, or models that incorporate Orca-managed data.
- Internal and external collaborators who request, consume, or redistribute Orca datasets.

## Governing Principles

- **Stewardship first:** Source-study requirements and steward directives guide downstream usage.
- **Transparency:** Dataset lineage, assumptions, and known limitations remain discoverable in Orca Docs.
- **Least-privilege access:** Consumers receive the minimum access necessary for approved use cases.
- **Auditability:** Key decisions, approvals, and dataset changes are logged and reviewable.

## Roles and Responsibilities

- **Orca Governance Lead**  
  Owns this policy, adjudicates escalations, and coordinates annual reviews.

- **Dataset Stewards / Principal Investigators**  
  Validate source data alignment, define access controls, review major transformations, and approve external sharing.

- **Orca Engineering Team**  
  Implements pipelines in Dagster, maintains dataset metadata, enforces quality checks, and documents transformations.

- **Platform Consumers**  
  Follow approved use cases, cite datasets per the attribution policy, and report data quality or compliance issues promptly.

## Dataset Lifecycle Management

### Ingestion and Onboarding

- A steward sponsor must submit onboarding details (source system, refresh cadence, quality constraints, privacy considerations).  
- Orca engineering captures lineage, transformation logic, and dependencies in Dagster and Orca Docs before first release.

### Data Quality Assurance

- Automated validation checks run on each pipeline execution; failures block publication until resolved.  
- Stewards review and sign off on initial data drops and material schema changes.

### Documentation

- Each dataset must include a data dictionary, refresh schedule, steward contacts, and known limitations.  
- Documentation updates accompany any schema or semantic change.

### Access and Security

- Access requests route through the steward and governance lead, recorded in the Orca access log.  
- Sensitive fields are masked or excluded per steward guidance and regulatory requirements.

### Updates and Change Control

- Non-breaking updates (e.g., new derived columns) require steward notification and release notes in Orca Docs.  
- Breaking changes (e.g., schema revisions, deprecations) require steward approval, consumer communication, and a scheduled deployment window.

### Retention and Sunset

- Retention periods align with study agreements and institutional policy.  
- Sunsetting a dataset requires written steward approval, archive location documentation, and consumer impact communication.

## Issue Management and Escalation

- Consumers report data issues via email to the governance lead.
- High-severity incidents (privacy exposure, regulatory breach) trigger immediate escalation to the governance lead and institutional compliance office.

## Compliance and Auditing

- Quarterly audits verify access rights, pipeline approvals, and the integrity of lineage metadata.  
- Compliance findings and remediation actions are tracked through closure.

## Key Contacts

| Dataset Type | Study      | Source Data Contact       |
|--------------|------------|---------------------------|
| Clinical     | GI-DAMPs   | Shaun Chuah, Peter Cartlidge |
| Clinical     | MUSIC      | Shaun Chuah, Peter Cartlidge |
| Clinical     | Mini-MUSIC | David Wands               |

Report errors or omissions to the governance lead.

## Review Cycle and Versioning

- This policy undergoes formal review at least once per year or following significant changes to Orca platform capabilities.  
- Version history and change summaries are maintained in Orca Docs.

## Questions

For governance questions, access requests, or policy clarifications, contact [shaun.chuah@glasgow.ac.uk](mailto:shaun.chuah@glasgow.ac.uk). For dataset-specific inquiries, reach out to the steward listed in the table above.
