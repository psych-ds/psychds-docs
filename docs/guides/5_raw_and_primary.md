# Raw and primary data

A fundamental principle of Psych-DS is the preservation of the earliest available form of research data. This page explains the distinctions between raw and primary data, and how to handle different data types within the Psych-DS framework.

## Core principles

!!! important "Key Requirements"
    - The earliest form of data must be preserved
    - Original data should never be modified
    - Different versions of the data should be kept separate
    - All transformations should be documented

## Understanding raw vs primary data

### Raw data

Raw data refers to the very first form in which data exists, regardless of format. This could be:

- Paper questionnaires
- Audio/video recordings
- Device output files
- Hand-written notes
- Original Excel workbooks
- Survey software exports

### Primary data

Primary data refers to the first *digital* form of the data. As defined by the German Psychological Society, this distinction becomes important when raw data begins in a non-digital format.

!!! example "Raw vs Primary Data Examples"
    **Scenario 1: Paper-based collection**

    - Raw Data: Physical paper questionnaires
    - Primary Data: Scanned PDFs or spreadsheet with transcribed responses
    
    **Scenario 2: Digital Collection**

    - Raw Data: Survey software export file
    - Primary Data: Same file (raw and primary are identical)
    
    **Scenario 3: Behavioral Observation**

    - Raw Data: Video recordings of participant behavior
    - Primary Data: Spreadsheet of coded behaviors from videos

## Data organization in Psych-DS

### The `data/` directory

Your Psych-DS `data/` directory should contain:

1. Primary data (or the earliest version available)
2. Any Psych-DS compliant versions of that data
3. All subsequent processed/transformed versions

### The `data/raw/` subdirectory

If your primary data is not in CSV format, store it in the `data/raw/` subdirectory. This tells the Psych-DS validator to ignore these files while still preserving them as part of your dataset.

!!! tip "Directory structure example"
    ```
    my-study/
        data/
            raw/
                original-survey-responses.xlsx
                participant-videos/
                    participant001.mp4
                    participant002.mp4
            participant-001_data.csv
            participant-002_data.csv
    ```
