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

### Source Field

### Location Mapping


## Additional Resources

---