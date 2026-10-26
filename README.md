# CFPB Mortgage Complaint Analytics & Forecasting

## Project Overview

This project analyzes approximately **99,000 CFPB mortgage complaints** from October 2022 through September 2026 to understand complaint trends, issue concentration, company response behavior, mortgage-market context, and short-term complaint forecasting.

The project combines exploratory analysis, external market data, time-series feature engineering, and machine-learning model evaluation.

## Key Questions

- How has mortgage complaint volume changed over time?
- Which complaint categories drive the largest share of activity?
- Which companies account for the highest complaint volumes?
- Are there meaningful differences in company response timeliness?
- Do mortgage rates or refinancing activity help explain complaint trends?
- Can historical complaint behavior predict future weekly complaint volume?

## Key Findings

### Complaint Volume

Mortgage complaint volume increased materially during the later portion of the dataset, particularly during 2026.

The forecasting holdout period averaged approximately **659 complaints per week**, compared with approximately **437 complaints per week** during the training period.

### Complaint Concentration

The two largest complaint categories were:

- Trouble during the payment process
- Struggling to pay mortgage

The ten largest companies accounted for approximately **49% of all complaints**.

### Company Response Performance

Approximately **98.2%** of complaints received a timely response overall.

Among the largest companies analyzed, **Shellpoint Mortgage Servicing was a significant outlier**, with approximately **95.4% timely responses**, compared with approximately 99.9%–100% for several other major companies.

Shellpoint represented roughly **10% of total complaint volume**, but approximately **26% of all untimely complaints**.

### Mortgage Market Enrichment

Complaint trends were compared with:

- Freddie Mac 30-year mortgage rates
- Fannie Mae refinance application activity

The market indicators showed moderate correlations with complaint levels, but correlations between month-over-month changes were close to zero.

This suggests that mortgage-market conditions provide useful context but do not strongly explain short-term changes in aggregate complaint volume.

## Forecasting

Weekly complaint volume was modeled using:

- 1-week lag
- 2-week lag
- 4-week lag
- 4-week rolling average
- 8-week rolling average

Three forecasting approaches were evaluated:

| Model | Holdout MAE | Average Time-Series CV MAE |
|---|---:|---:|
| Naive Baseline | **58.33** | **47.32** |
| Linear Regression | 90.23 | 47.48 |
| Random Forest | 117.15 | 61.84 |

The naive one-week persistence forecast performed best during the final holdout period.

Linear Regression performed similarly to the naive baseline across multiple historical validation periods but struggled during the higher-volume 2026 regime.

Random Forest performed worst overall and showed difficulty adapting to the structural increase in complaint volume.

## Main Takeaway

The analysis found that **company-level operational behavior and recent complaint trends were more informative than broad mortgage-market correlations or increased model complexity**.

A simple forecasting baseline proved highly competitive, reinforcing the importance of benchmarking, time-aware validation, and monitoring structural changes in time-series data.

## Tools & Technologies

- Python
- Pandas
- NumPy
- Matplotlib
- scikit-learn
- pandas-datareader
- Jupyter Notebook
- Git / GitHub

## Data Sources

- Consumer Financial Protection Bureau Consumer Complaint Database
- Freddie Mac 30-Year Mortgage Rate via FRED
- Fannie Mae Weekly Mortgage Applications Data

## Project Structure

```text
notebooks/
├── 01_cfpb_eda.ipynb
└── 02_cfpb_forecasting.ipynb

data/
├── complaints.csv
└── fannie_mae_pali_rali_pull_as_of_2026-10-16.xlsx
```

## Limitations

- CFPB complaints are not representative of all mortgage customers.
- Complaint counts are not normalized by company market share or loans serviced.
- Correlation does not establish causation.
- Recent CFPB observations may be affected by reporting lag.
- The forecasting dataset contains approximately 200 usable weekly observations.
- Forecasting results should be interpreted as short-term predictive analysis rather than long-range forecasting.
