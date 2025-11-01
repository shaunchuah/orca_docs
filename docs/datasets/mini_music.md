# Mini-MUSIC Dataset

## Overview

Mini-MUSIC is a longitudinal pediatric IBD cohort study with fixed follow-up timepoints, using age-appropriate disease activity scores and classification systems designed for children and adolescents.

**Study ID Prefix**: `MINI-`

## Key Characteristics

- **Data Structure**: Fixed timepoints (timepoint_1 through timepoint_3: baseline, 3 months, 6 months)
- **Participants**: Pediatric only (typically <18 years)
- **Age Groups**: 6-10, 10-13, 14-18 years
- **Longitudinal Follow-up**: Scheduled visits at baseline and follow-up intervals
- **Focus Areas**: Pediatric-specific outcomes, EEN, age-appropriate disease activity

## Dataset Statistics

- **Columns**: 423
- **Study Centers**: Edinburgh, Glasgow, Dundee, Aberdeen
- **Study Groups**: CD, UC, IBDU, non-IBD

## Key Variables

### Demographics & Baseline

- `study_id`: Format `MINI-xxx`
- `redcap_event_name`: `timepoint_1`, `timepoint_2`, `timepoint_3`
- `patient_age_group`: 6-10, 10-13, 14-18, no_data
- `study_group`: CD, UC, IBDU, non_ibd
- `new_diagnosis_of_ibd`: yes/no
- `age`, `sex`, `height`, `weight`, `bmi`
- `date_of_diagnosis`, `age_at_diagnosis`

### Pediatric Disease Activity Scores

- **Ulcerative Colitis**:
  - `pucai_score`: Pediatric Ulcerative Colitis Activity Index (0-85)
  - Components: `pucai_pain`, `pucai_bleeding`, `pucai_consistency`, `pucai_stools`, `pucai_nocturnal`, `pucai_activity`
- **Crohn's Disease**:
  - `pcdai_score`: Pediatric Crohn's Disease Activity Index (0-100)
  - Components: `pcdai_pain`, `pcdai_general`, `pcdai_frequency`, `pcdai_esr`, `pcdai_alb`, `pcdai_weight`, `pcdai_perianal`
  - EIM components: `pcdai_eim_fever`, `pcdai_eim_arthritis`, `pcdai_eim_uveitis`, etc.

### Pediatric Classification Systems

- **Crohn's Disease**: Paris Classification
  - `cdparis_location`: L1, L2, L3, L4
  - `cdparis_behaviour`: B1, B2, B3, B2+B3
  - `cdparis_upper_gi`: L4a, L4b, none
  - `cdparis_growth`: G0, G1
  - `cdparis_perianal`: yes/no
- **Ulcerative Colitis**: Paris Classification
  - `ucparis_extent`: E1, E2, E3, E4
  - `ucparis_severity`: S0, S1

### Patient-Reported Outcomes (Pediatric)

- `impact3_score`: IMPACT-III total score (0-100)
- `impact_wellbeing`, `impact_emotional`, `impact_social`, `impact_bodyimage`: IMPACT-III subscales
- `impactq1` through `impactq35`: Individual IMPACT-III items
- `promis_fatigue_score`: PROMIS Fatigue Score
- `fatigue_severity`, `fatigue_standard_error`, `fatigue_tscore`: Fatigue metrics
- `fatigueq1` through `fatigueq10`: Individual fatigue items

### Exclusive Enteral Nutrition (EEN)

- `een_use`: EEN use (yes/no)
- `een_formula_type`: Modulen IBD, Fortisip, Nutrison Energy, Elemental EO28, Pediasure, Nutrini, Neocate Jr, other
- `een_formula_type_text`: Free text for other formulas
- `een_start_date`, `een_end_date`: EEN dates
- `een_still_taken`: Currently on EEN (yes/no)

### Disease Activity Assessment

- `has_active_symptoms`: yes/no
- `physician_global_assessment`: biochem_remission, clinical_remission, mild, moderate, severe
- `disease_activity`: remission, mild, moderate, severe, not_applicable
- Individual symptoms: `symptoms_abdominal_pain`, `symptoms_diarrhoea`, `symptoms_urgency`, `symptoms_pr_bleeding`, `symptoms_weight_loss`, `symptoms_fatigue`, `symptoms_perianal`

### Laboratory Values

- Blood parameters: `haemoglobin`, `crp`, `albumin`, `white_cell_count`, `esr`, etc.
- `calprotectin`: Faecal calprotectin
- `calprotectin_date`: Sample collection date
- Drug levels: `ifx_level`, `ada_level`, `ifx_antibody`, `ada_antibody`
- `drug_level_date`: Date of drug level testing

### Medications

- `sampling_*`: Medications at time of visit (1 = yes, 0 = no)
  - `sampling_asa`, `sampling_een`, `sampling_steroids_oral`, `sampling_steroids_iv`, `sampling_steroids_topical`
  - `sampling_imm`, `sampling_mtx`, `sampling_ifx`, `sampling_ada`
  - `sampling_vedo`, `sampling_uste`, `sampling_other`
- Current drug tracking: `ibd_drug_1_*` through `ibd_drug_5_*` (name, dose, frequency, dates)
- Baseline medication history: `baseline_ibd_drug_1_*` through `baseline_ibd_drug_5_*`
- Concomitant non-IBD drugs: `concomitant_drug_1_*` through `concomitant_drug_5_*`

### Clinical Events

- `new_flare_up`: New flare since last visit
- `flare_up_1_date`: Flare date
- `flare_up_1_description_*`: Detailed flare symptoms (abdominal_pain, diarrhoea, urgency, etc.)
- `flare_up_1_setting`: outpatient/inpatient
- `flare_up_1_management_*`: Management strategies (iv_steroids, oral_steroids, een, new_biologic, other)
- `unplanned_hospital_admission`: Hospital admission since last visit
- `hospital_admission_1_*`: Admission details

### Phenotyping

- Extra-intestinal manifestations: `baseline_eims_*` (arthritis, erythema_nodosum, pyoderma, uveitis, episcleritis, sacroileitis, conjunctivitis, angular_cheilitis, psc, other)
- Surgical history: `surgical_history_*`
- Past medical history: `pmh_1_diagnosis` through `pmh_7_diagnosis`
- Family history: `fh_of_ibd_present`, `fh_1_*` through `fh_5_*` (relationship, age_at_diagnosis, diagnosis)

### Investigations

- `endoscopy_date`, `endoscopy_type_colonoscopy`, `endoscopy_type_upper_gi_endoscopy`
- `endoscopy_report`, `pathology_report`
- `mayo_endoscopic_findings`, `sescd_calc`, `sescd_noncalc`
- `physician_endoscopic_severity`: normal, mild, moderate, severe
- `radiology_test_date`: CT/MRI dates
- `mri_small_bowel`, `mri_pelvis`, `ct_abdomen_pelvis`: Imaging performed
- Radiology reports available

### Saliva Sampling

- `saliva_sample`: Sample collected (1 = yes, 0 = no)
- `saliva_setting`: Sample collection setting
- `sample_date`: Date of saliva sample
- Saliva-specific variables: `saliva_eim`, `saliva_abx`, `saliva_piercing`, `saliva_brushing`, `saliva_dietibd`, etc.

## Data Structure Notes

### Timepoint Structure

- `timepoint_1`: Baseline visit
- `timepoint_2`: 3 months follow-up
- `timepoint_3`: 6 months follow-up

### Age Groups

- `patient_age_group`: Categorical grouping (6-10, 10-13, 14-18 years)
- Used for appropriate scoring system selection

## Study-Specific Features

1. **Pediatric-Specific Scores**: PCDAI and PUCAI instead of adult scores (HBI, SCCAI, Mayo)
2. **Paris Classification**: Pediatric-specific IBD classification system
3. **EEN Tracking**: Detailed exclusive enteral nutrition data (not in adult studies)
4. **Pediatric PROs**: IMPACT-III and PROMIS fatigue scores
5. **Age-Appropriate Data**: All assessments designed for pediatric populations

## Important Considerations

### Disease Activity Scores

Mini-MUSIC uses pediatric-specific scores that cannot be directly compared to adult scores:

- **Do not compare** PCDAI with HBI
- **Do not compare** PUCAI with SCCAI or Mayo
- Use Paris classification (not Montreal) for phenotype comparisons

### Age Groups

When analyzing by age, consider using `patient_age_group` for categorical analyses or `age` for continuous analyses.

### Missing Adult Scores

Mini-MUSIC does not include HBI, SCCAI, or Mayo scores, as these are not validated in pediatric populations.

## Data Dictionary

- **[Unified Variables](../data_dictionary/index.md)**: Common variables across all datasets
- **[Mini-MUSIC Columns](../data_dictionary/mini_music_columns.md)**: Complete column list

## Pipeline Documentation

- **[Mini-MUSIC Pipeline](../pipeline/mini_music.md)**: Data extraction and transformation code

## Data Access

For access requests or data questions, contact the data steward listed in [Dataset Governance](../dataset_governance.md).
