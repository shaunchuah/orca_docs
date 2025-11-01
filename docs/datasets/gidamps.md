# GI-DAMPs Dataset

## Overview

GI-DAMPs (Investigation into the inflammatory mechanism of gut damage-associated molecular patterns [DAMPs] in Inflammatory Bowel Disease) is a cross-sectional and longitudinal sampling study that collects comprehensive clinical and biomarker data from participants with IBD and healthy controls.

**Study ID Prefix**: `GID-`

## Key Characteristics

- **Data Structure**: Sampling-based visits (not fixed timepoints)
- **Participants**: Adults only
- **Recruitment Settings**: Inpatient, outpatient, and endoscopy-based
- **Focus Areas**: Biomarker research, drug monitoring, disease activity assessment

## Dataset Statistics

- **Approximate Rows**: ~9,756 (sampling visits)
- **Columns**: 227
- **Study Centers**: Edinburgh, Glasgow, Dundee
- **Study Groups**: CD, UC, IBDU, non-IBD, awaiting diagnosis, healthy controls

## Key Variables

### Demographics & Baseline
- `study_id`: Format varies by center (see [Known Issues](../issues.md))
- `study_group`: Disease classification
- `baseline_recruitment_type`: endoscopy, outpatient, inpatient
- `age`, `sex`, `height`, `weight`, `bmi`
- `date_of_diagnosis`, `age_at_diagnosis`

### Sampling Information
- `sampling_date`: Date of sample collection
- `sampling_setting`: inpatient, outpatient, endoscopy
- `has_active_symptoms`: Symptom status at sampling
- `symptoms_description`: Free text description

### Disease Activity Scores
- **Crohn's Disease**: `hbi_total`, individual HBI components
- **Ulcerative Colitis**: `sccai_total`, individual SCCAI components
- **Endoscopic**: `mayo_total`, `uceis_total`, `sescd_total`
- `endoscopy_active`: Active disease indicator

### Laboratory Values
- Blood parameters: `haemoglobin`, `crp`, `albumin`, `white_cell_count`, etc.
- `calprotectin`: Faecal calprotectin (ug/g)
- `calprotectin_date`: Sample collection date
- Drug levels: `ifx_level`, `ada_level`, `ifx_antibody`, `ada_antibody`

### Medications
- `sampling_*`: Medications at time of sampling (1 = yes, 0 = no)
  - `sampling_asa`, `sampling_aza`, `sampling_mp`, `sampling_ifx`, `sampling_ada`
  - `sampling_vedo`, `sampling_uste`, `sampling_tofa`, `sampling_mtx`
  - `sampling_steroids`, `sampling_abx`
- Historical medication exposure: `ifx`, `ada`, `vedo`, `uste`, etc. with start/stop dates

### Phenotyping
- Montreal Classification: `montreal_cd_location`, `montreal_cd_behaviour`, `montreal_uc_extent`, `montreal_uc_severity`
- Extra-intestinal manifestations: `baseline_eims_*`
- Surgical history: `past_ibd_surgery`

### Investigations
- `endoscopy_date`, `endoscopy_report`, `pathology_report`
- `radiology_test_date`: CT/MRI dates
- `mri_small_bowel`, `mri_pelvis`, `ct_abdomen`: Imaging performed (1 = yes, 0 = no)
- Radiology reports: `mri_small_bowel_report`, `mri_pelvis_report`, `ct_abdomen_report`

### Patient-Reported Outcomes
- `cucq_total`: CUCQ-32 total score
- `cucq_1` through `cucq_32`: Individual questionnaire items
- `participant_questionnaire_comments`: Free text comments

## Data Structure Notes

### Multiple Rows Per Participant
Each participant can have multiple sampling visits, identified by:
- `study_id`: Unique participant identifier
- `redcap_repeat_instance`: Instance number for the sampling visit

### Demographics Data
Baseline demographics are repeated across sampling rows. The `gidamps_demographics_dataframe` asset provides a single row per participant.

### CUQ-32 Integration
CUCQ-32 questionnaire data is merged with sampling data based on `study_id` and `sampling_date`.

## Study-Specific Features

1. **Flexible Sampling Schedule**: Unlike fixed timepoint studies, GI-DAMPs samples are collected based on clinical events
2. **Diverse Recruitment**: Captures data from inpatient flares, outpatient visits, and scheduled endoscopies
3. **Comprehensive Biomarkers**: Rich laboratory data including drug levels and antibodies
4. **Multi-Center**: Data from Edinburgh, Glasgow, and Dundee centers

## Important Considerations

### Study ID Format
Study IDs have evolved over time. Edinburgh uses `GID-x`, while Glasgow uses `GID-136-x` and Dundee uses `GID-138-x`. See [Known Issues](../issues.md) for details.

### Disease Activity Variable
GI-DAMPs uses `ibd_status` instead of `disease_activity`, with values:
- `biochem_remission`
- `remission`
- `active`
- `highly_active`
- `not_applicable`

### Missing Timepoints
Since visits are sampling-based rather than scheduled, there's no consistent follow-up schedule across participants.

## Data Dictionary

- **[Unified Variables](../data_dictionary/index.md)**: Common variables across all datasets
- **[GI-DAMPs Columns](../data_dictionary/gidamps_columns.md)**: Complete column list

## Pipeline Documentation

- **[GI-DAMPs Pipeline](../pipeline/gidamps.md)**: Data extraction and transformation code

## Data Access

For access requests or data questions, contact the data stewards listed in [Dataset Governance](../dataset_governance.md).
