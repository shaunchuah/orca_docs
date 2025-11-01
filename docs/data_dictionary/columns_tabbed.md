# Study-Specific Columns

Each study dataset includes study-specific variables in addition to the [common variables](index.md) shared across all datasets.

=== "GI-DAMPs"

    GI-DAMPs includes 227 columns. In addition to the common standardized variables, GI-DAMPs includes:

    - Sampling-specific variables: `sampling_date`, `sampling_setting`, `redcap_repeat_instance`
    - Detailed medication tracking with start/stop dates
    - Comprehensive biomarker and drug level data
    - CUCQ-32 questionnaire items (`cucq_1` through `cucq_32`)

    **[View Complete GI-DAMPs Column List →](gidamps_columns.md)**

=== "MUSIC"

    MUSIC includes 369 columns. In addition to the common standardized variables, MUSIC includes:

    - Mucosal healing outcomes: `endoscopic_mucosal_healing`, `complete_mucosal_healing`
    - Timepoint-specific outcomes at 3-6 and 12 months
    - PRO2 scores: `cd_pro2_raw`, `cd_pro2_weighted`, `uc_pro2`
    - Saliva sampling variables: `saliva_sample`, `saliva_setting`, and related fields
    - Comprehensive flare-up and hospitalization tracking

    **[View Complete MUSIC Column List →](music_columns.md)**

=== "Mini-MUSIC"

    Mini-MUSIC includes 423 columns. In addition to the common standardized variables, Mini-MUSIC includes:

    - Pediatric disease activity scores: `pucai_score`, `pcdai_score`
    - Paris classification variables: `cdparis_*`, `ucparis_*`
    - Pediatric PROs: `impact3_score`, `promis_fatigue_score`
    - EEN (exclusive enteral nutrition) variables: `een_use`, `een_formula_type`, etc.
    - Detailed current medication tracking: `ibd_drug_1_*` through `ibd_drug_5_*`

    **[View Complete Mini-MUSIC Column List →](mini_music_columns.md)**
