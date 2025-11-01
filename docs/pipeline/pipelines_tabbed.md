# Data Pipelines

This section provides references for the code used in data transformation and extraction. Each dataset has its own pipeline that processes data from REDCap and transforms it into the standardized format available in G-Trac.

If you need to trace the changes made to a variable, you can search within the pipeline to find the relevant transformations.

=== "GI-DAMPs"

    The GI-DAMPs pipeline extracts data from the IGMM RedCap Server and performs:

    - **Raw Data Extraction**: Fetches data from REDCap API
    - **Data Cleaning**: Renames columns, maps values, converts data types
    - **Demographics DataFrame**: Creates baseline participant data
    - **Sampling DataFrame**: Creates visit-level sampling data with merged demographics and CUCQ-32

    **[View GI-DAMPs Pipeline Code →](gidamps.md)**

=== "MUSIC"

    The MUSIC pipeline extracts data from the IGMM RedCap Server and performs:

    - **Raw Data Extraction**: Fetches data from specific REDCap forms
    - **Baseline Drug Columns**: Re-engineers baseline medication columns
    - **Data Reshaping**: Merges laboratory tests and saliva samples
    - **Data Cleaning**: Fixes column names, maps values, creates derived variables
    - **Mucosal Healing**: Creates mucosal healing outcome variables
    - **PRO2 Scores**: Calculates CD and UC PRO2 scores
    - **Demographics DataFrame**: Creates baseline-only dataset

    **[View MUSIC Pipeline Code →](music.md)**

=== "Mini-MUSIC"

    The Mini-MUSIC pipeline extracts data from the IGMM RedCap Server and performs:

    - **Raw Data Extraction**: Fetches data from specific REDCap forms
    - **Data Cleaning**: Renames columns, maps categorical values
    - **Drug Mapping**: Maps medication codes to standardized names
    - **Pediatric Classifications**: Processes Paris classification variables

    **[View Mini-MUSIC Pipeline Code →](mini_music.md)**

=== "Combined"

    The Combined MUSIC pipeline merges MUSIC and Mini-MUSIC datasets:

    - **Dataset Merging**: Concatenates MUSIC and Mini-MUSIC dataframes
    - **Column Analysis**: Identifies overlapping and dataset-specific columns
    - **Metadata**: Provides detailed information about merged dimensions

    **[View Combined Pipeline Code →](combined_music.md)**


