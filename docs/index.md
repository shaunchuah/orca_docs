# Welcome to Orca

Meet our friendly Orca, your companion in navigating the data waves. Orca is a collaborative data platform that unifies diverse scientific and clinical datasets. Just as orcas work together in pods to achieve their goals, our platform harnesses the power of teamwork to accelerate scientific discovery and innovation. This documentation guides you through effectively utilizing our integrated datasets.

![Orca](orca_logo_min.png)

## What is Orca?

Orca is a Dagster-based data engineering platform that aggregates data from multiple REDCap study databases, processes them, and stores the final datasets in G-Trac. The platform currently manages data from three primary studies focused on Inflammatory Bowel Disease (IBD) research:

- **GI-DAMPs**: Investigation into the inflammatory mechanism of gut damage-associated molecular patterns (DAMPs) in Inflammatory Bowel Disease
- **MUSIC**: Mitochondrial DAMPs as mechanistic biomarkers of gut mucosal inflammation
- **Mini-MUSIC**: Pediatric IBD cohort study

## Quick Start

1. **[Getting Started](getting_started.md)** - Learn how to access and work with Orca datasets
2. **[Dataset Overviews](datasets/index.md)** - Explore each dataset's features and statistics (with tabs for quick comparison)
3. **[Data Dictionary](data_dictionary/index.md)** - Understand the standardized variables and study-specific fields
4. **[Pipelines](pipeline/index.md)** - Review the data transformation code and lineage

## Key Features

### Unified Data Standards

All datasets follow standardized naming conventions (snake_case) and share common variables for demographics, laboratory values, medications, and clinical assessments. This enables seamless cross-study analysis while preserving study-specific details.

### Comprehensive Clinical Data

Datasets include:

- Demographics and baseline characteristics
- Disease activity scores (HBI, SCCAI, Mayo, UCEIS, SES-CD)
- Laboratory values (bloods, calprotectin, drug levels)
- Medication history and sampling status
- Endoscopic and radiological findings
- Patient-reported outcomes

### Data Quality Assurance

- Automated validation checks on each pipeline execution
- Comprehensive data dictionaries with clear variable definitions
- Documentation of known data issues and limitations
- Clear lineage tracking through Dagster assets

## Documentation Structure

| Section | Description |
|---------|-------------|
| [Dataset Overviews](datasets/index.md) | Key statistics, features, and characteristics of each dataset (tabbed view) |
| [Data Dictionary](data_dictionary/index.md) | Complete variable reference with types, values, and descriptions |
| [Pipelines](pipeline/index.md) | Code documentation for data extraction and transformation (tabbed view) |
| [Policies](dataset_governance.md) | Dataset governance, attribution policy, and access requirements |
| [Known Issues](issues.md) | Important data quality considerations and limitations |

## Getting Help

For questions about:

- **Dataset access**: Contact the data steward listed in [Dataset Governance](dataset_governance.md)
- **Data interpretation**: Review the [Data Dictionary](data_dictionary/index.md) and [Known Issues](issues.md)
- **Technical support**: Contact the Orca engineering team via [shaun.chuah@glasgow.ac.uk](mailto:shaun.chuah@glasgow.ac.uk)
