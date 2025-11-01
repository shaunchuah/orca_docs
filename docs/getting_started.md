# Getting Started with Orca Datasets

This guide will help you quickly access and start working with datasets from the Orca platform.

## Overview

Orca datasets are stored in G-Trac and processed through Dagster pipelines. Each dataset goes through standardized cleaning, transformation, and validation steps before being made available for analysis.

## Available Datasets

### GI-DAMPs 

- **Study Name**: Investigation into the inflammatory mechanism of gut damage-associated molecular patterns in Inflammatory Bowel Disease
- **Study Type**: Cross-sectional IBD sampling study (with optional longitudinal sampling)
- **Data Structure**: Sampling visits with optional repeated measures
- **Key Features**: Comprehensive biomarker data, detailed medication tracking
- **More Info**: [GI-DAMPs Overview](datasets/gidamps.md)

### MUSIC

- **Study Name**: Mitochondrial DAMPs as mechanistic biomarkers of gut mucosal inflammation
- **Study Type**: Longitudinal adult IBD cohort study
- **Data Structure**: Fixed timepoints (timepoint_1 through timepoint_5)
- **Key Features**: Mucosal healing outcomes, longitudinal follow-up
- **More Info**: [MUSIC Overview](datasets/music.md)

### Mini-MUSIC

- **Study Name**: Mitochondrial DAMPs as mechanistic biomarkers of gut mucosal inflammation in children
- **Study Type**: Paediatric IBD cohort study
- **Data Structure**: Similar to MUSIC, but with paediatric-specific assessments (PUCAI, PCDAI, Paris classification)
- **Key Features**: Age-appropriate disease activity scores, exclusive enteral nutrition (EEN) tracking
- **More Info**: [Mini-MUSIC Overview](datasets/mini_music.md)

## Accessing Datasets

### Step 1: Understand the Data Structure

Before accessing data, familiarize yourself with:

1. **[Unified Data Dictionary](data_dictionary/index.md)** - Common variables across all datasets
2. **[Study-Specific Columns](data_dictionary/columns_tabbed.md)** - Variables unique to each study
3. **[Dataset Governance](dataset_governance.md)** - Access policies and requirements

### Step 2: Load and Explore Data

Datasets are typically provided as CSV files. Here's a basic workflow:

```python
import pandas as pd

# Load a dataset
df = pd.read_csv('gidamps_sampling_2025-10-30.csv')

# Check basic structure
print(f"Shape: {df.shape}")
print(f"Columns: {df.columns.tolist()[:10]}...")  # First 10 columns

# Explore common variables
print(df[['study_id', 'study_group', 'age', 'sex', 'crp', 'calprotectin']].head())
```

### Access Workflow

1. Review the [Dataset Governance](dataset_governance.md) policy to confirm you meet any prerequisite training and to identify the correct data steward for the study.
2. Email the governance lead and the relevant steward (see the contacts listed in the policy) with a short summary of your project, the datasets you need, and the timeframe for access.
3. The governance lead records the request, coordinates steward approval, and replies with confirmation plus the G-Trac folder path for the authorised datasets. Orca datasets are stored within the Orca workspace on G-Trac and each CSV filename includes the extraction date (for example, `music_main_2025-01-15.csv`).
4. Sign in to G-Trac with your institutional credentials to download the most recent dated files. When pipelines publish a refresh, the governance lead shares release notes by email and keeps the folder-level README up to date, so monitor those messages for cadence updates.

## Understanding Variable Names

All variables follow **snake_case** naming convention. Key patterns:

### Demographics

- `study_id`: Unique participant identifier (prefix: GID-, MID-, MINI-)
- `study_group`: Disease classification (cd, uc, ibdu, non_ibd, hc)
- `age`, `sex`, `height`, `weight`, `bmi`

### Laboratory Values

- Prefix pattern: Variable name indicates the measurement
- `nhs_bloods_date`: Date of blood sample
- `haemoglobin`, `crp`, `albumin`: Test results
- `calprotectin_date`, `calprotectin`: Faecal calprotectin

### Medications

- `sampling_*`: Medications at time of sampling (1 = yes, 0 = no)
- Examples: `sampling_asa`, `sampling_ifx`, `sampling_ada`
- `baseline_*`: Historical medication exposure

### Disease Activity Scores

- `hbi_total`: Harvey-Bradshaw Index total score
- `sccai_total`: Simple Clinical Colitis Activity Index
- `mayo_total`: Mayo Score
- `sescd`, `uceis`: Endoscopic scores

## Common Workflows

### Comparing Across Studies

When working with multiple datasets, focus on variables documented in the [Unified Data Dictionary](data_dictionary/index.md):

```python
# Example: Compare CRP levels across studies
common_vars = ['study_id', 'study_group', 'age', 'crp', 'calprotectin']

# Filter to common variables
gidamps_subset = gidamps_df[common_vars]
music_subset = music_df[common_vars]
mini_music_subset = mini_music_df[common_vars]

# Combine for analysis
combined = pd.concat([
    gidamps_subset.assign(source='GI-DAMPs'),
    music_subset.assign(source='MUSIC'),
    mini_music_subset.assign(source='Mini-MUSIC')
])
```

### Handling Missing Data

- Missing values are typically represented as `NaN` or empty strings
- Some categorical variables use specific codes for missing/unknown (see data dictionary)
- Review [Known Issues](issues.md) for dataset-specific considerations

### Date Variables

Date columns follow `YYYY-MM-DD` format:

```python
# Convert to datetime
df['nhs_bloods_date'] = pd.to_datetime(df['nhs_bloods_date'])
df['date_of_diagnosis'] = pd.to_datetime(df['date_of_diagnosis'])
```

## Important Considerations

### Study-Specific Differences

**Disease Activity Classifications**: Vary between studies (see [Known Issues](issues.md))

**Timepoints**:

- GI-DAMPs: Sampling visits (no fixed schedule)
- MUSIC: Fixed timepoints (1-5)
- Mini-MUSIC: Fixed timepoints (1-3)

**Scoring Systems**:

- Adults: HBI, SCCAI, Mayo
- Pediatrics: PCDAI, PUCAI, Paris classification

### Data Quality

- Always review [Known Issues](issues.md) before analysis
- Check for data version/date stamps in filenames
- Verify variable meanings in the data dictionary
- Contact data stewards for clarifications

## Next Steps

1. **[Explore Dataset Overviews](datasets/index.md)** - Detailed information about each dataset
2. **[Review Data Dictionary](data_dictionary/index.md)** - Complete variable reference
3. **[Check Known Issues](issues.md)** - Important limitations and considerations
4. **[Understand Pipelines](pipeline/index.md)** - How data is transformed

## Getting Help

- **Data questions**: Contact study data stewards (see [Dataset Governance](dataset_governance.md))
- **Technical issues**: [shaun.chuah@glasgow.ac.uk](mailto:shaun.chuah@glasgow.ac.uk)
- **Documentation updates**: Submit issues or pull requests
