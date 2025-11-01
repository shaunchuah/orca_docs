# Dataset Comparison Guide

This guide helps you understand the similarities and differences between Orca datasets to choose the right data for your analysis.

## Quick Comparison Table

| Feature | GI-DAMPs | MUSIC | Mini-MUSIC |
|---------|----------|-------|------------|
| **Study ID Prefix** | `GID-` | `MID-` | `MINI-` |
| **Population** | Adults only | Adults only | Pediatric only |
| **Data Structure** | Sampling visits | Fixed timepoints | Fixed timepoints |
| **Timepoints** | Variable | 1-5 | 1-3 |
| **Columns** | 227 | 369 | 423 |
| **Primary Focus** | Biomarkers, drug monitoring | Mucosal healing | Pediatric outcomes, EEN |
| **Disease Activity Scores** | HBI, SCCAI | HBI, SCCAI, Mayo | PCDAI, PUCAI |

## Variable Availability

### Common to All Datasets

All datasets share standardized variables across demographics, laboratory values, medications, and phenotyping. For complete variable definitions and documentation, see the [Unified Data Dictionary](../data_dictionary/index.md).

### Dataset-Specific Variables

#### GI-DAMPs Unique Features

- `sampling_date`, `sampling_setting` (inpatient/outpatient/endoscopy)
- `redcap_repeat_instance` for multiple sampling visits per participant
- `comment`, `medication_comments` (free text fields)
- More detailed medication history with start/stop dates

#### MUSIC Unique Features

- `endoscopic_mucosal_healing`, `complete_mucosal_healing`
- `endoscopic_mucosal_healing_at_3_6_months`, `endoscopic_mucosal_healing_at_12_months`
- `cd_pro2_raw`, `cd_pro2_weighted`, `uc_pro2`
- `ibdresponse_criteria_cd_met`, `ibdresponse_criteria_uc_met`
- `saliva_sample`, `saliva_setting`, saliva-specific variables

#### Mini-MUSIC Unique Features

- `pucai_score`, `pcdai_score` (pediatric disease activity)
- `cdparis_*`, `ucparis_*` (pediatric classification)
- `impact3_score`, `promis_fatigue_score` (pediatric PROs)
- `een_use`, `een_formula_type`, `een_start_date`, `een_end_date`
- `patient_age_group` (6-10, 10-13, 14-18)
- `ibd_drug_1_*` through `ibd_drug_5_*` (detailed current medication tracking)

## Disease Activity Scores

### Comparison of Scoring Systems

| Score | GI-DAMPs | MUSIC | Mini-MUSIC | Notes |
|-------|----------|-------|------------|-------|
| **HBI** (Harvey-Bradshaw) | ✓ | ✓ | ✗ | Adults with CD only |
| **SCCAI** (Simple Clinical Colitis) | ✓ | ✓ | ✗ | Adults with UC only |
| **Mayo Score** | ✓ | ✓ | ✗ | Adults with UC only |
| **SES-CD** (Crohn's endoscopy) | ✓ | ✓ | ✓ | All studies |
| **UCEIS** (UC endoscopy) | ✓ | ✓ | ✓ | All studies |
| **PCDAI** (Pediatric CD) | ✗ | ✗ | ✓ | Pediatrics only |
| **PUCAI** (Pediatric UC) | ✗ | ✗ | ✓ | Pediatrics only |

**Important**: PCDAI and PUCAI are not comparable to HBI and SCCAI. Use pediatric scores only for Mini-MUSIC analyses.

## Classification Systems

### Montreal Classification (Adults)

- Used in: GI-DAMPs, MUSIC
- Variables: `montreal_cd_location`, `montreal_cd_behaviour`, `montreal_uc_extent`, `montreal_uc_severity`

### Paris Classification (Pediatrics)

- Used in: Mini-MUSIC
- Variables: `cdparis_location`, `cdparis_behaviour`, `cdparis_upper_gi`, `cdparis_growth`, `cdparis_perianal`, `ucparis_extent`, `ucparis_severity`

**Note**: These systems are designed for different age groups and should not be directly compared.

## Disease Activity Variables

Disease activity classifications vary significantly across studies. Each study uses different variable names and value sets for representing disease activity. For a detailed comparison table, standardization suggestions, and example implementation code, see [Known Issues - Disease Activity Definitions](../issues.md#disease-activity-definitions-vary-between-studies).

## Longitudinal Structure

### GI-DAMPs

- **Structure**: Sampling visits (not fixed intervals)
- **Key Variable**: `redcap_repeat_instance` (instance number)
- **Visit Date**: `sampling_date`
- **Considerations**: Variable intervals between visits, based on clinical events

### MUSIC

- **Structure**: Fixed timepoints
- **Key Variable**: `redcap_event_name` (timepoint_1 through timepoint_5)
- **Visit Date**: `visit_date`
- **Considerations**: Fixed intervals (Baseline, 3 months, 6 months, 9 months, 12 months)

### Mini-MUSIC

- **Structure**: Fixed timepoints
- **Key Variable**: `redcap_event_name` (timepoint_1, timepoint_2, timepoint_3)
- **Visit Date**: Available in dataset
- **Considerations**: Fixed intervals (Baseline, 3 months, 6 months)

## Medication Variables

### Sampling Status (All Studies)

All studies use `sampling_*` prefix to indicate medications at time of visit/sampling:

- `sampling_asa`, `sampling_ifx`, `sampling_ada`, `sampling_vedo`, `sampling_uste`, etc.
- Values: `1` = yes, `0` = no

### Historical Medication (Study-Specific)

- **GI-DAMPs**: `ifx`, `ada`, `vedo`, etc. with `*_start`, `*_stop` dates
- **MUSIC**: `baseline_*` prefix (e.g., `baseline_ifx`, `baseline_ada`)
- **Mini-MUSIC**: `baseline_ibd_drug_1_*` through `baseline_ibd_drug_5_*` (structured format)

## Combining Datasets

### Recommended Approach

1. **Focus on Common Variables**: Use variables documented in the [Unified Data Dictionary](../data_dictionary/index.md)

2. **Standardize Disease Activity**: Consider creating a standardized variable based on:
    - `has_active_symptoms`
    - `crp` (threshold >5 mg/L)
    - `calprotectin` (threshold >250 μg/g)

    See [Known Issues](../issues.md) for example implementation.

3. **Respect Study-Specific Differences**:
    - Don't compare pediatric scores (PCDAI/PUCAI) with adult scores
    - Don't mix Montreal and Paris classifications
    - Account for different timepoint structures

4. **Use Combined Dataset When Available**:
    - [Combined MUSIC/Mini-MUSIC](../pipeline/combined_music.md) already merges those two datasets
    - For GI-DAMPs + MUSIC, manually merge on common variables

### Example: Cross-Study Analysis

```python
# Load datasets
gidamps = pd.read_csv('gidamps_sampling_2025-10-30.csv')
music = pd.read_csv('music_main_2025-10-30.csv')

# Select common variables
common_vars = [
    'study_id', 'study_group', 'age', 'sex', 'bmi',
    'crp', 'calprotectin', 'has_active_symptoms',
    'sampling_ifx', 'sampling_ada'
]

# Filter and combine
gidamps_subset = gidamps[common_vars].assign(source='GI-DAMPs')
music_subset = music[music['redcap_event_name'] == 'timepoint_1'][common_vars].assign(source='MUSIC')

combined = pd.concat([gidamps_subset, music_subset])

# Create standardized disease activity
def standardize_activity(row):
    if row['has_active_symptoms'] == 'yes' or row['has_active_symptoms'] == 1:
        if row['crp'] > 5 and pd.notna(row['calprotectin']) and float(str(row['calprotectin']).replace('<', '').replace('>', '')) > 250:
            return 'biochem_active'
        else:
            return 'active'
    else:
        if row['crp'] > 5 or (pd.notna(row['calprotectin']) and float(str(row['calprotectin']).replace('<', '').replace('>', '')) > 250):
            return 'remission'
        else:
            return 'biochem_remission'

combined['standardized_activity'] = combined.apply(standardize_activity, axis=1)
```

## Choosing the Right Dataset

### Use GI-DAMPs if you need:

- ✅ Sampling-based data collection
- ✅ Diverse recruitment settings
- ✅ Rich biomarker data
- ⚠️ Not suitable for fixed-interval longitudinal analyses
- ⚠️ Adults only (no paediatric data)

### Use MUSIC if you need:

- ✅ Adult longitudinal data
- ✅ Mucosal healing outcomes
- ✅ Fixed timepoint structure
- ⚠️ Adults only (no paediatric data)

### Use Mini-MUSIC if you need:

- ✅ Paediatric-specific data
- ✅ EEN (exclusive enteral nutrition) information
- ✅ Pediatric disease activity scores (PCDAI, PUCAI)
- ✅ Age-appropriate classifications (Paris)
- ⚠️ Cannot combine with adult scores

### Combine Multiple Datasets if you need:

- ✅ Cross-study comparisons
- ✅ Larger sample sizes
- ✅ Validation across populations
- ⚠️ Must standardize variables first (see above)
