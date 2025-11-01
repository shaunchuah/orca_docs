# Dataset Overviews

This section provides comprehensive overviews of each dataset available through the Orca platform. Each dataset has unique characteristics, data structures, and research focus areas.

## Available Datasets

| Dataset | Study ID Prefix | Study Type | Participants | Columns | Data Structure |
|---------|----------------|------------|--------------|---------|----------------|
| [GI-DAMPs](gidamps.md) | `GID-` | Cross-sectional & longitudinal | ~9,756 rows* | 227 | Sampling visits |
| [MUSIC](music.md) | `MID-` | Adult longitudinal cohort | ~17,260 rows* | 369 | Fixed timepoints (1-5) |
| [Mini-MUSIC](mini_music.md) | `MINI-` | Pediatric longitudinal cohort | ~9,265 rows* | 423 | Fixed timepoints (1-3) |

\* Row counts are approximate and based on example datasets. Actual counts may vary.

## Quick Comparison

### Study Populations

- **GI-DAMPs**: Adults and children, multiple recruitment settings (inpatient, outpatient, endoscopy)
- **MUSIC**: Adults only (≥18 years)
- **Mini-MUSIC**: Pediatric only (typically <18 years)

### Key Differences

| Feature | GI-DAMPs | MUSIC | Mini-MUSIC |
|---------|----------|-------|------------|
| Disease Activity Scores | HBI, SCCAI | HBI, SCCAI, Mayo | PCDAI, PUCAI |
| Classification System | Montreal | Montreal | Paris (pediatric) |
| Mucosal Healing Tracking | Limited | Comprehensive | Comprehensive |
| EEN Tracking | No | No | Yes |
| Longitudinal Follow-up | Variable | Fixed timepoints | Fixed timepoints |

### Common Variables

All datasets share standardized variables for demographics, laboratory values, medications, and phenotyping. See the [Unified Data Dictionary](../data_dictionary/index.md) for complete variable definitions and documentation.

For guidance on selecting the appropriate dataset for your analysis, see the [Dataset Comparison Guide](comparison.md).

## Combining Datasets

For analyses that span multiple studies, use the [Combined MUSIC dataset](../pipeline/combined_music.md) or focus on variables documented in the [Unified Data Dictionary](../data_dictionary/index.md) to ensure compatibility.

**Important**: Always review study-specific differences in disease activity classifications as documented in [Known Issues](../issues.md).

## Next Steps

- Review individual dataset pages for detailed information
- Check the [Data Dictionary](../data_dictionary/index.md) for variable definitions
- See [Getting Started](../getting_started.md) for access and usage guidelines

