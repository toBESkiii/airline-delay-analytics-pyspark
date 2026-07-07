# airline-delay-analytics-pyspark
Description: End-to-end PySpark analytics project exploring airline delay trends, carrier performance, airport delay rates, and seasonal operational disruption patterns.
[README.md](https://github.com/user-attachments/files/29755281/README.md)
# Airline Delay Analytics with PySpark

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue)](#)
[![PySpark](https://img.shields.io/badge/PySpark-Data%20Analytics-orange)](#)
[![Status](https://img.shields.io/badge/Status-Portfolio%20Project-success)](#)

An end-to-end PySpark analytics project that examines airline arrival-delay patterns across time, carriers, airports, and operational delay causes. The workflow is structured as a reproducible data-analysis case study: raw-data inspection, evidence-based preprocessing, weighted metric engineering, distributed aggregation, and charting from small pandas summaries.

## Business context

This project models the kind of analysis an airline operations, airport performance, or network-planning team could use to monitor disruption, compare operational performance, and identify recurring delay-risk hotspots.

## Questions answered

1. How have overall flight delays changed over time?
2. Which airlines have the highest percentage of delayed flights?
3. Which airlines experience the most carrier-caused delays?
4. Which airports have the highest delay rates?
5. What are the dominant causes of delays across all flights by year?
6. How do delay causes vary by season?
7. Which months have the highest and lowest delay percentages?

## Technical approach

```text
Raw CSV
  → PySpark DataFrame loading and schema inspection
  → Missing-value assessment and validation
  → Clean analytical DataFrame
  → Delay-rate feature engineering
  → Spark groupBy aggregations and weighted metrics
  → Small aggregated results converted to pandas
  → Matplotlib visualisations
```

### Key analytical decisions

- **Raw data is preserved.** The project uses separate DataFrames for the untouched source data (`airline_raw`), cleaned data (`airline_clean`), and engineered analysis data (`airline_metrics`).
- **Missing values were not blindly imputed.** Rows missing `arr_flights` were removed because a valid delay-rate denominator was unavailable. Rows with `arr_flights` present but `arr_del15` missing were validated against delay-cause and delay-minute fields before `arr_del15` was imputed as zero.
- **Delay rates are weighted correctly.** Aggregate rates use `sum(arr_del15) / sum(arr_flights)` rather than the mean of row-level percentages. This prevents low-volume airport or carrier records from receiving the same influence as high-volume operations.
- **Spark remains responsible for large-data work.** Only small, final summary tables are converted to pandas for plotting.

## Repository structure

```text
airline-delay-analytics-pyspark/
├── notebooks/
│   └── Airline_Delay_Analytics_with_PySpark.ipynb
├── images/
│   ├── 01_overall_delay_rate_over_time.png
│   ├── 02_airlines_by_delay_rate.png
│   ├── 03_carrier_caused_delays.png
│   ├── 04_airports_by_delay_rate.png
│   ├── 05_delay_cause_distribution_by_year.png
│   ├── 06_monthly_delay_cause_patterns.png
│   └── 07_monthly_delay_rate_seasonality.png
├── data/
│   └── README.md
├── .gitignore
├── requirements.txt
└── README.md
```

## Visual outputs

### Overall delay rate over time

![Overall delay rate over time](images/01_overall_delay_rate_over_time.png)

### Airlines with the highest delay rates

![Airlines by delay rate](images/02_airlines_by_delay_rate.png)

### Carrier-caused delays by airline

![Carrier-caused delays](images/03_carrier_caused_delays.png)

### Airports with the highest delay rates

![Airports by delay rate](images/04_airports_by_delay_rate.png)

### Delay-cause distribution by year

![Delay cause distribution by year](images/05_delay_cause_distribution_by_year.png)

### Monthly patterns in delay causes

![Monthly delay cause patterns](images/06_monthly_delay_cause_patterns.png)

### Monthly delay-rate seasonality

![Monthly delay-rate seasonality](images/07_monthly_delay_rate_seasonality.png)

## How to run the project

1. Clone or download this repository.
2. Install dependencies:

```bash
pip install -r requirements.txt
```

3. Place a permitted copy of the source CSV in the `data/` folder using this exact filename:

```text
Airline_Delay_Cause.csv
```

4. Open and run:

```text
notebooks/Airline_Delay_Analytics_with_PySpark.ipynb
```

For Google Colab, upload the CSV to the runtime and update the `file_path` configuration cell before executing the notebook.

## Tools used

- Python
- PySpark DataFrames and Spark SQL functions
- pandas
- Matplotlib
- Jupyter Notebook / Google Colab

## Portfolio value

This project demonstrates practical capability in data cleaning, imputation validation, feature engineering, distributed aggregation, analytical metric design, and business-focused visual storytelling.

## Data note

The raw CSV is excluded from this repository. Before publishing publicly, confirm the dataset's original source, licence, and redistribution permissions, then add the official source link and attribution here.
