# Dataset Overviews

This section provides comprehensive overviews of each dataset available through the Orca platform. Each dataset has unique characteristics, data structures, and research focus areas.

=== "GI-DAMPs"

    **Study ID Prefix**: `GID-`

    GI-DAMPs is a cross-sectional sampling study (with optional longitudinal sampling) that collects comprehensive clinical and biomarker data from participants with IBD and healthy controls.

    **Key Characteristics:**

    - Data Structure: Sampling-based visits (not fixed timepoints)
    - Participants: Adults only
    - Recruitment Settings: Inpatient, outpatient, and endoscopy-based
    - Focus Areas: Biomarker research, drug monitoring, disease activity assessment

    **Dataset Statistics:**

    - Columns: 227
    - Study Centers: Edinburgh, Glasgow, Dundee
    - Study Groups: CD, UC, IBDU, non-IBD, awaiting diagnosis, healthy controls

    **[View Full GI-DAMPs Documentation →](gidamps.md)**

=== "MUSIC"

    **Study ID Prefix**: `MID-`

    MUSIC is a longitudinal adult IBD cohort study with fixed follow-up timepoints focusing on mucosal healing outcomes.

    **Key Characteristics:**

    - Data Structure: Fixed timepoints (timepoint_1 through timepoint_5)
    - Participants: Adults only
    - Longitudinal Follow-up: Scheduled visits at baseline and follow-up intervals
    - Focus Areas: Mucosal healing

    **Dataset Statistics:**

    - Columns: 369
    - Study Centers: Edinburgh, Glasgow, Dundee
    - Study Groups: CD, UC

    **[View Full MUSIC Documentation →](music.md)**

=== "Mini-MUSIC"

    **Study ID Prefix**: `MINI-`

    Mini-MUSIC is a longitudinal pediatric IBD cohort study with fixed follow-up timepoints, using age-appropriate disease activity scores and classification systems designed for children/adolescents.

    **Key Characteristics:**

    - Data Structure: Fixed timepoints (timepoint_1 through timepoint_3)
    - Participants: Pediatric only (typically <18 years)
    - Age Groups: 6-10, 10-13, 14-18 years
    - Focus Areas: Pediatric-specific outcomes, EEN, age-appropriate disease activity

    **Dataset Statistics:**

    - Columns: 423
    - Study Centers: Edinburgh, Glasgow, Dundee, Aberdeen
    - Study Groups: CD, UC, IBDU, non-IBD

    **[View Full Mini-MUSIC Documentation →](mini_music.md)**

=== "Comparison"

    **Quick Comparison Table:**

    | Feature | GI-DAMPs | MUSIC | Mini-MUSIC |
    |---------|----------|-------|------------|
    | **Study ID Prefix** | `GID-` | `MID-` | `MINI-` |
    | **Population** | Adults only | Adults only | Pediatric only |
    | **Data Structure** | Sampling visits | Fixed timepoints | Fixed timepoints |
    | **Timepoints** | Variable | 1-5 | 1-3 |
    | **Columns** | 227 | 369 | 423 |
    | **Primary Focus** | Biomarkers, drug monitoring | Mucosal healing | Pediatric outcomes, EEN |
    | **Disease Activity Scores** | HBI, SCCAI | HBI, SCCAI, Mayo | PCDAI, PUCAI |

    **[View Detailed Comparison Guide →](comparison.md)**

