# Getting Started with Orca Datasets

This guide will help you quickly access and start working with datasets from the Orca platform.

## Overview

Orca datasets are stored in G-Trac and processed through Dagster pipelines. Each dataset goes through standardized cleaning, transformation, and validation steps before being made available for analysis.

## Available Datasets

### GI-DAMPs (GID)
- **Study Type**: Cross-sectional and longitudinal IBD sampling study (Investigation into the inflammatory mechanism of gut damage-associated molecular patterns [DAMPs] in Inflammatory Bowel Disease)
- **Data Structure**: Sampling visits with repeated measures
- **Key Features**: Comprehensive biomarker data, detailed medication tracking
- **Rows**: ~9,756 (as of example dataset)
- **Columns**: 227
- **More Info**: [GI-DAMPs Overview](datasets/gidamps.md)

### MUSIC (MID)
- **Study Type**: Longitudinal adult IBD cohort (Mitochondrial DAMPs as mechanistic biomarkers of gut mucosal inflammation)
- **Data Structure**: Multiple timepoints (timepoint_1 through timepoint_5)
- **Key Features**: Mucosal healing outcomes, comprehensive PRO2 scores
- **Rows**: ~17,260 (as of example dataset)
- **Columns**: 369
- **More Info**: [MUSIC Overview](datasets/music.md)

### Mini-MUSIC (MINI)
- **Study Type**: Pediatric IBD cohort study
- **Data Structure**: Pediatric-specific assessments (PUCAI, PCDAI, Paris classification)
- **Key Features**: Age-appropriate disease activity scores, exclusive enteral nutrition (EEN) tracking
- **Rows**: ~9,265 (as of example dataset)
- **Columns**: 423
- **More Info**: [Mini-MUSIC Overview](datasets/mini_music.md)

## Accessing Datasets

### Step 1: Understand the Data Structure

Before accessing data, familiarize yourself with:
1. **[Unified Data Dictionary](data_dictionary/index.md)** - Common variables across all datasets
2. **[Study-Specific Columns](data_dictionary/)** - Variables unique to each study
3. **[Dataset Governance](dataset_governance.md)** - Access policies and requirements

### Step 2: Request Access

Contact the appropriate data steward (see [Dataset Governance](dataset_governance.md)) to:
- Obtain access credentials
- Specify your intended use case
- Review any restrictions or requirements

### Step 3: Load and Explore Data

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

1. **Disease Activity Classifications**: Vary between studies (see [Known Issues](issues.md))
2. **Timepoints**: 
   - GI-DAMPs: Sampling visits (no fixed schedule)
   - MUSIC: Fixed timepoints (1-5)
   - Mini-MUSIC: Fixed timepoints (1-3)
3. **Scoring Systems**: 
   - Adults: HBI, SCCAI, Mayo
   - Pediatrics: PCDAI, PUCAI, Paris classification

### Data Quality

- Always review [Known Issues](issues.md) before analysis
- Check for data version/date stamps in filenames
- Verify variable meanings in the data dictionary
- Contact data stewards for clarifications

## Next Steps

1. **[Explore Dataset Overviews](datasets/)** - Detailed information about each dataset
2. **[Review Data Dictionary](data_dictionary/index.md)** - Complete variable reference
3. **[Check Known Issues](issues.md)** - Important limitations and considerations
4. **[Understand Pipelines](pipeline/index.md)** - How data is transformed

## Getting Help

- **Data questions**: Contact study data stewards (see [Dataset Governance](dataset_governance.md))
- **Technical issues**: `orca-governance@domain.org`
- **Documentation updates**: Submit issues or pull requests

