# Target Data for Respiratory Virus Detection Surveillance System's Lab Detections (2024-25)

## Overview

The `target-data` folder contains the **CSV** data that the forecasts will be compared against. This data serves as the "gold standard" for evaluating the forecasting models. For the current Flu season, the data is stored in `target-data/season_2024_2025/data_report.csv` file.

### Table of Contents
- [Lab Detections Data](#lab-detections-data)
- [Accessing Target Data](#accessing-target-data)
- [Data Processing](#data-processing)
- [Additional Resources](#additional-resources)

## Lab Detections Data

### Source
**Respiratory Virus Detection Surveillance System (RVDSS)**

Our hub's prediction targets (`sarscov2_pct_positive`, `rsv_pct_positive` and `flu_pct_positive`) are scraped from the Respiratory Virus Detection Surveillance System (RVDSS), published by the Public Health Agency of Canada (PHAC). The data was historically reported in weekly reports, but the current season is moved to an interactive dashboard. Historic reports and the interactive dashboard can be found [here](https://www.canada.ca/en/public-health/services/surveillance/respiratory-virus-detections-canada.html). The target data file `data_reports.csv` is generated using the raw data that is made available through the webscraping scripts provided by the [Delphi Epi Data](https://github.com/cmu-delphi/delphi-epidata).

Previously collected data from earlier seasons are included in the `.auxiliary-data\target-data-archive` directory in their respective season sub-directories as `data_reports.csv`. The `sarscov2_pct_positive` data starts from the `season_2022_2023` and hence these column values are not included in previous season data files. 

### Target Data Column Names (data_report.csv)

- `time_value`: the last day of the epiweek

- `geo_type`: the type of geographical location

- `geo_value`: the actual geographical location

- `[virus]_pct_positive`: the percentage of tests for a given virus that are positive (target)


## Accessing Target Data

**Primary Data Source:** [Respiratory Virus Detection Surveillance System (RVDSS)](https://www.canada.ca/en/public-health/services/surveillance/respiratory-virus-detections-canada.html)

### CSV Files
A set of CSV files is updated weekly with the latest observed values for [target type, e.g., percentage of positive virus detections]. These are available at:
- `./target-data/season_2024_2025/data_report.csv`
- `auxiliary-data/season_2024_2025_raw_files` (Raw Files)

## Data Processing
The `rvdss_update.py` code processes and updates weekly data on respiratory virus detections in Canada, automatically adding new entries. It begins by defining functions to standardize virus and geographic names (e.g., "parainfluenza" to "hpiv" and "Newfoundland" to "nl") and to categorize geographic areas (as nation, region, or province) for consistent organization.

Two main functions then retrieve and transform the data. `get_revised_data()` accesses historical weekly data, reformats it with a multi-index structure and ensures date consistency. `get_weekly_data()` retrieves data for the latest epidemiological week, determining the correct year and week from a summary file. It then applies the same formatting and standardization as with the historical data.

After processing, the code saves the data in `positive_tests.csv` and `respiratory_detections.csv` files. If these files already exist, it checks for new entries by comparing indices, appending updated data to prevent duplication. After saving updates to `positive_tests.csv` and `respiratory_detections.csv`, the code consolidates both datasets into a unified file, `raw.csv`. The file `raw.csv` includes updated `geo_type` values and removes duplicates, keeping only the latest (**revised**) entry for each combination of `time_value`, `geo_type`, and `geo_value`. 

Finally, the code refines `raw.csv` into `data_report.csv` by selecting target columns (`COLUMNS_TARGET`) and rounding percentage values to three decimal places, creating a ready-to-analyze file with standardized weekly data across Canada.

### Source Field
For each season, the code generates three intermediary files:

- **positive_tests.csv**
  - Displays the percentage of positive tests for each virus by week.
  - Aggregated at the regional level, with national totals included.
  - Includes revisions for each update.
  - Matches **Table 1** in the reports, typically titled [“Respiratory virus detections for the week ending...”](https://www.canada.ca/en/public-health/services/surveillance/respiratory-virus-detections-canada/2021-2022/week-28-ending-july-16-2022.html#a2)

- **respiratory_detections.csv**
  - Shows the number of positive tests for each virus (including subtypes) by week.
  - Aggregated at the lab level, with summaries at the regional level.
  - Includes revisions for each update.
  - Matches **Figures 3-9** in the reports, typically titled [“Positive [virus] tests (%)...”](<https://www.canada.ca/en/public-health/services/surveillance/respiratory-virus-detections-canada/2021-2022/week-28-ending-july-16-2022.html#a5>)

- **raw.csv**
  - Consolidates data from `positive_tests.csv` and `respiratory_detections.csv`.
  - Updates the `geo_type` field based on location corrections (from `LOC_CORRECTION`).
  - Removes duplicate rows, keeping only the latest (revised) entry for each combination of `time_value`, `geo_type`, and `geo_value`.
  - Drops unnecessary columns (e.g., `issue` and `epiweek`), creating a streamlined dataset for further analysis.


## Additional Resources

---
