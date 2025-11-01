# Documentation Redundancy Report

This document identifies areas of repetition and redundancy across the Orca documentation for review and potential consolidation.

## 1. Dataset Statistics (Row/Column Counts)

**Repeated in:**
- `docs/getting_started.md` (lines 15-16, 23-24, 31-32)
- `docs/datasets/index.md` (lines 9-11)
- `docs/datasets/comparison.md` (line 13-14)
- `docs/datasets/gidamps.md` (lines 18-19)
- `docs/datasets/music.md` (lines 18-19)
- `docs/datasets/mini_music.md` (lines 19-20)

**Issue**: Row counts (~9,756, ~17,260, ~9,265) and column counts (227, 369, 423) are duplicated across multiple files.

**Recommendation**: Consider creating a single source of truth (e.g., metadata file or single location) and reference it, or keep minimal summary in index/comparison pages and detailed stats only in individual dataset pages.

---

## 2. Study ID Prefixes

**Repeated in:**
- `docs/index.md` (in study descriptions)
- `docs/getting_started.md` (section headers: GID, MID, MINI)
- `docs/datasets/index.md` (table column)
- `docs/datasets/comparison.md` (table)
- `docs/datasets/gidamps.md` (line 7)
- `docs/datasets/music.md` (line 7)
- `docs/datasets/mini_music.md` (line 7)

**Issue**: Study ID prefix format (`GID-`, `MID-`, `MINI-`) is mentioned in nearly every file.

**Recommendation**: This is acceptable as it's a key identifier, but could be standardized to reference the individual dataset page definitions.

---

## 3. Study Type/Population Descriptions

**Repeated in:**
- `docs/datasets/index.md` (Study Populations section, lines 19-21)
- `docs/datasets/comparison.md` (Population row in table, line 10)
- Individual dataset pages (Key Characteristics sections)

**Issue**: "Adults only", "Pediatric only", "Adults and children" descriptions are duplicated.

**Recommendation**: Acceptable as each serves a different purpose (overview vs. detailed), but wording could be standardized.

---

## 4. Data Structure Information

**Repeated in:**
- `docs/getting_started.md` ("Data Structure" bullet points)
- `docs/datasets/index.md` (table "Data Structure" column, lines 9-11)
- `docs/datasets/comparison.md` ("Data Structure" row, line 11)
- Individual dataset pages (Key Characteristics sections)

**Issue**: "Sampling visits" vs. "Fixed timepoints" information is repeated.

**Recommendation**: Acceptable - serves different contexts (quick reference vs. detailed explanation).

---

## 5. "Choosing the Right Dataset" Guidance

**Repeated in:**
- `docs/datasets/index.md` (lines 43-63: "Choosing the Right Dataset")
- `docs/datasets/comparison.md` (lines 169-195: "Choosing the Right Dataset")

**Issue**: Similar bullet-point lists of "Use X if you need..." appear in both files with slight variations.

**Recommendation**: **Consider consolidating** - the comparison.md version is more detailed. Could remove from index.md or make index.md link to comparison.md for this guidance.

---

## 6. Key Features/Characteristics

**Repeated in:**
- `docs/getting_started.md` ("Key Features" bullet points for each dataset)
- `docs/datasets/index.md` (Quick Comparison table, lines 27-31)
- `docs/datasets/comparison.md` (comparison tables throughout)
- Individual dataset pages (various sections)

**Issue**: Disease activity scores, classification systems, mucosal healing tracking, etc. are described in multiple places.

**Recommendation**: Acceptable - each serves different levels of detail. However, the comparison.md "Disease Activity Scores" section (lines 60-70) overlaps significantly with the individual dataset pages.

---

## 7. Common Variables Lists

**Repeated in:**
- `docs/datasets/index.md` (lines 33-41: "Common Variables")
- `docs/datasets/comparison.md` (lines 19-26: "Common to All Datasets")
- `docs/data_dictionary/index.md` (complete detailed tables)

**Issue**: Similar lists of common variables (demographics, laboratory, medications, phenotyping) in multiple locations.

**Recommendation**: **Consider consolidating** - the data_dictionary/index.md is the authoritative source. The other locations could provide brief summaries with links to the full dictionary.

---

## 8. Dataset-Specific Variable Lists

**Repeated in:**
- `docs/datasets/comparison.md` (lines 28-46: "Dataset-Specific Variables")
- Individual dataset pages (extensive "Key Variables" sections)

**Issue**: Unique features/variables for each dataset appear in both comparison.md and individual dataset pages.

**Recommendation**: Acceptable - comparison provides quick reference, individual pages provide detail. However, some variable descriptions are verbatim duplicated.

---

## 9. Disease Activity Score Information

**Repeated in:**
- `docs/datasets/index.md` (Quick Comparison table, line 27)
- `docs/datasets/comparison.md` (Disease Activity Scores section, lines 60-70)
- Individual dataset pages (Disease Activity Scores sections)
- `docs/issues.md` (disease activity variations, lines 5-18)

**Issue**: Information about which scores are available in which datasets is repeated across multiple files.

**Recommendation**: **Consider consolidating** - The issues.md table is most comprehensive. Could standardize on that as the reference.

---

## 10. Study Centers Information

**Repeated in:**
- Individual dataset pages (Dataset Statistics sections)
- `docs/dataset_governance.md` (Key Contacts table, lines 81-86)

**Issue**: Study center information (Edinburgh, Glasgow, Dundee) appears in multiple locations.

**Recommendation**: Acceptable - different contexts (dataset stats vs. governance contacts).

---

## 11. Contact/Steward Information

**Repeated in:**
- `docs/dataset_governance.md` (Key Contacts table)
- Individual dataset pages (Data Stewards sections at end)

**Issue**: Same contact information for data stewards appears in governance.md and each dataset page.

**Recommendation**: **Consider consolidating** - Individual dataset pages could reference the governance page instead of repeating names.

---

## 12. Data Dictionary Links

**Repeated in:**
- Multiple files reference `../data_dictionary/index.md` or `data_dictionary/index.md`
- "Unified Data Dictionary" is mentioned with similar descriptions in:
  - `docs/datasets/index.md` (line 35)
  - `docs/datasets/comparison.md` (line 21)
  - `docs/getting_started.md` (line 40)

**Issue**: Similar link descriptions and introductions to the data dictionary.

**Recommendation**: Acceptable - standard linking practice, but wording could be standardized.

---

## 13. Pipeline Documentation Links

**Repeated in:**
- Individual dataset pages (all have "Pipeline Documentation" sections)
- `docs/pipeline/index.md` (if it exists)

**Issue**: Similar text linking to pipeline documentation for each dataset.

**Recommendation**: Acceptable - standard section in each dataset page.

---

## 14. Next Steps / Additional Resources

**Repeated in:**
- `docs/datasets/index.md` (lines 71-75: "Next Steps")
- `docs/datasets/comparison.md` (lines 197-201: "Additional Resources")
- `docs/getting_started.md` (lines 137-145: "Next Steps")

**Issue**: Similar lists of links to other documentation sections.

**Recommendation**: Acceptable - each serves its context, but could be standardized with a shared "See also" section.

---

## 15. Disease Activity Variable Differences

**Repeated in:**
- `docs/datasets/comparison.md` (lines 90-100: "Disease Activity Variables")
- `docs/issues.md` (lines 5-52: detailed disease activity comparison)

**Issue**: Same information about disease activity variable names and values across studies appears in both files.

**Recommendation**: **Consider consolidating** - The issues.md version is more detailed with code examples. comparison.md could reference issues.md instead of duplicating the table.

---

## Summary of Recommended Actions

### High Priority (Significant Redundancy):
1. **Consolidate "Choosing the Right Dataset"** - Remove from `datasets/index.md`, keep in `datasets/comparison.md`
2. **Consolidate Common Variables** - Simplify summaries in comparison/index pages, link to full dictionary
3. **Consolidate Disease Activity Information** - Reference `issues.md` from comparison.md instead of duplicating
4. **Consolidate Contact Information** - Reference governance.md from dataset pages instead of repeating

### Medium Priority (Acceptable but Could Be Improved):
5. **Standardize Variable Lists** - Use consistent wording when listing common variables
6. **Standardize Next Steps Sections** - Use consistent format for cross-references
7. **Create Single Source for Statistics** - Consider metadata file, or clearly designate authoritative location

### Low Priority (Acceptable Redundancy):
8. Study ID prefixes (needed in multiple contexts)
9. Basic study characteristics (serves different detail levels)
10. Data structure descriptions (serves different purposes)

---

## Notes

- Some redundancy is intentional and useful (e.g., quick reference tables in comparison pages vs. detailed descriptions in individual pages)
- The goal should be to eliminate **unnecessary** redundancy while maintaining **useful** repetition that serves different contexts
- Consider adding a "See Also" or "Related Documentation" section template for consistent cross-referencing

