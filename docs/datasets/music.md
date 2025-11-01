# MUSIC Dataset

## Overview

MUSIC (Mitochondrial DAMPs as mechanistic biomarkers of gut mucosal inflammation) is a longitudinal adult IBD cohort study with fixed follow-up timepoints focusing on mucosal healing outcomes and comprehensive disease activity assessment.

**Study ID Prefix**: `MID-`

## Key Characteristics

- **Data Structure**: Fixed timepoints (timepoint_1 through timepoint_5)
- **Participants**: Adults only (≥18 years)
- **Longitudinal Follow-up**: Scheduled visits at baseline and follow-up intervals
- **Focus Areas**: Mucosal healing, PRO2 scores, treatment response

## Dataset Statistics

- **Approximate Rows**: ~17,260 (all timepoints)
- **Columns**: 369
- **Study Centers**: Edinburgh, Glasgow, Dundee
- **Study Groups**: CD, UC

## Key Variables

### Demographics & Baseline
- `study_id`: Format `MID-xxx`
- `redcap_event_name`: `timepoint_1` through `timepoint_5`
- `study_group`: CD or UC
- `age`, `sex`, `height`, `weight`, `bmi`
- `date_of_diagnosis`, `age_at_diagnosis`

### Disease Activity Scores
- **Crohn's Disease**: 
  - `hbi_total`: Harvey-Bradshaw Index
  - Individual HBI components: `hbi_abdominal_pain`, `hbi_liquid_stools`, etc.
- **Ulcerative Colitis**:
  - `sccai_total`: Simple Clinical Colitis Activity Index
  - `mayo_total`: Mayo Score
  - Individual Mayo components: `mayo_stool_frequency`, `mayo_rectal_bleeding`
- **Endoscopic Scores**:
  - `sescd`: Simple Endoscopic Score for Crohn's Disease
  - `uceis`: Ulcerative Colitis Endoscopic Index of Severity
  - `mayo_endoscopic_score`: Mayo endoscopic subscore
- `physician_global_assessment`: Remission, mild, moderate, severe
- `disease_activity`: Biochemical remission, remission, active, biochemically active

### Mucosal Healing Outcomes
- `endoscopic_mucosal_healing`: yes/no (SES-CD or UCEIS = 0)
- `complete_mucosal_healing`: yes/no/partial (endoscopic healing + normal pathology)
- `endoscopic_mucosal_healing_at_3_6_months`: Outcome at timepoint_2, populated to all timepoints
- `complete_mucosal_healing_at_3_6_months`: Outcome at timepoint_2
- `endoscopic_mucosal_healing_at_12_months`: Outcome at timepoint_5
- `complete_mucosal_healing_at_12_months`: Outcome at timepoint_5

### PRO2 Scores
- `cd_pro2_raw`: HBI liquid stools + HBI abdominal pain (raw)
- `cd_pro2_weighted`: HBI liquid stools × 2 + HBI abdominal pain × 5 (weighted)
- `uc_pro2`: Mayo stool frequency + Mayo rectal bleeding
- `ibdresponse_criteria_cd_met`: Boolean for CD PRO2 criteria (liquid stools ≥4 AND pain moderate/severe)
- `ibdresponse_criteria_uc_met`: Boolean for UC PRO2 criteria (stool frequency = 3 AND rectal bleeding >0)

### Laboratory Values
- Blood parameters: `haemoglobin`, `crp`, `albumin`, `white_cell_count`, etc.
- `calprotectin`: Faecal calprotectin
- `calprotectin_date`: Sample collection date
- Drug levels: `ifx_level`, `ada_level`, `ifx_antibody`, `ada_antibody`
- `drug_level_date`: Date of drug level testing

### Medications
- `sampling_*`: Medications at time of visit (1 = yes, 0 = no)
  - `sampling_asa`, `sampling_aza`, `sampling_mp`, `sampling_ifx`, `sampling_ada`
  - `sampling_vedo`, `sampling_uste`, `sampling_tofa`, `sampling_mtx`
  - `sampling_steroids`, `sampling_abx`, `sampling_ppi`
- Baseline medication history: `baseline_asa`, `baseline_ifx`, `baseline_ada`, etc.

### Clinical Events
- `new_flare_up`: New flare since last visit
- `flare_up_1_date`, `flare_up_1_description`: Flare details
- `unplanned_hospital_admission`: Hospital admission since last visit
- `hospital_admission_1_*`: Admission details
- `new_oral_steroids_since_last_visit`: New steroid use

### Phenotyping
- Montreal Classification: `montreal_cd_location`, `montreal_cd_behaviour`, `montreal_uc_extent`, `montreal_uc_severity`
- Extra-intestinal manifestations: `baseline_eims_*`
- Surgical history: `surgical_history_1_*`, `surgical_history_2_*`, etc.

### Investigations
- `endoscopy_date`, `endoscopy_type_colonoscopy`, `endoscopy_type_flexible_sigmoidoscopy`
- `endoscopy_report`, `pathology_report`
- `radiology_test_date`: CT/MRI dates
- `mri_small_bowel`, `mri_pelvis`, `ct_abdomen_pelvis`: Imaging performed
- Radiology reports available

### Patient-Reported Outcomes
- `cucq_total`: CUCQ-32 total score
- `cucq_1` through `cucq_32`: Individual questionnaire items
- `proms_comments`: Patient-reported outcome comments

### Saliva Sampling
- `saliva_sample`: Sample collected (1 = yes, 0 = no)
- `saliva_setting`: Sample collection setting
- `sample_date`: Date of saliva sample
- Saliva-specific variables: `saliva_eim`, `saliva_abx`, `saliva_piercing`, etc.

## Data Structure Notes

### Timepoint Structure
- `timepoint_1`: Baseline visit
- `timepoint_2`: ~3-6 months follow-up
- `timepoint_3`: ~6-9 months follow-up
- `timepoint_4`: ~9-12 months follow-up
- `timepoint_5`: ~12 months follow-up

### Demographics DataFrame
A separate `music_demographics_dataframe` asset contains only `timepoint_1` data with selected columns for baseline analyses.

### Mucosal Healing Forward-Filling
Mucosal healing outcomes at later timepoints (3-6 months, 12 months) are forward-filled to baseline for convenience in analyses.

## Study-Specific Features

1. **Mucosal Healing Focus**: Comprehensive tracking of endoscopic and complete mucosal healing
2. **PRO2 Scores**: Both raw and weighted PRO2 scores for CD and UC
3. **Fixed Timepoints**: Consistent follow-up intervals enable temporal analyses
4. **Comprehensive Phenotyping**: Detailed baseline characteristics and longitudinal tracking

## Important Considerations

### Disease Activity Variables
MUSIC has two disease activity variables:
- `physician_global_assessment`: Clinical assessment (remission, mild, moderate, severe)
- `disease_activity`: Broader classification including biochemical status

See [Known Issues](../issues.md) for comparison with other studies.

### Timepoint Completeness
Not all participants have data at all timepoints. Check `redcap_event_name` when analyzing longitudinal trends.

### Saliva Sample Data
Saliva sampling data is merged from separate REDCap instruments. Some timepoints may not have saliva data.

## Data Dictionary

- **[Unified Variables](../data_dictionary/index.md)**: Common variables across all datasets
- **[MUSIC Columns](../data_dictionary/music_columns.md)**: Complete column list with construction notes

## Pipeline Documentation

- **[MUSIC Pipeline](../pipeline/music.md)**: Data extraction and transformation code

## Data Access

For access requests or data questions, contact the data stewards listed in [Dataset Governance](../dataset_governance.md).

