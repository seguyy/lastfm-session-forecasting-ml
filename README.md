# Session Activity Forecasting with Machine Learning

## Project Overview

This project forecasts future listening session activity using the Last.fm 1K listening history dataset.

The workflow reconstructs listening sessions from raw listening events using a 20-minute inactivity threshold, selects the user with the highest number of sessions, and applies supervised machine learning to forecast the next 3 months of session activity.

The project combines PySpark-based preprocessing and feature engineering with a scikit-learn regression pipeline inside a Databricks environment.

---

## Dataset

Dataset source: [Last.fm 1K Dataset](http://ocelma.net/MusicRecommendationDataset/lastfm-1K.html)

Dataset attribution: [Last.fm](https://www.last.fm/)

Main file used:

```text
userid-timestamp-artid-artname-traid-traname.tsv
```

---

## Methodology

1. Reconstruct sessions using a 20-minute inactivity threshold
2. Select the user with the highest number of sessions
3. Aggregate monthly session activity
4. Apply time-series feature engineering
5. Train a regression forecasting pipeline
6. Predict the next 3 months of session activity

---

## Session Definition

A new session is created when the time gap between two consecutive listening events from the same user exceeds:

```text
20 minutes
```

---

## Forecasting Target

The selected forecasting metric is:

```text
number_of_sessions_per_month
```

The forecasting workflow predicts the next 3 months of session activity for the selected top user.

---

## Feature Engineering

The monthly time series is transformed into a supervised learning dataset using:

```text
month_index
month_of_year
lag_1
lag_2
rolling_3
```

Target variable:

```text
target_next_month_sessions
```

---

## Machine Learning Pipeline

A scikit-learn Pipeline is used with:

```text
SimpleImputer
StandardScaler
RandomForestRegressor
```

The pipeline performs:
- preprocessing
- feature scaling
- model training
- forecasting

---

## Technology Stack

```text
Databricks
PySpark
Pandas
scikit-learn
RandomForestRegressor
```

---

## Repository Structure

```text
lastfm-session-forecasting-ml/
├── README.md
├── .gitignore
├── notebooks/
│   └── session_forecasting_databricks.py
└── output/
    └── forecast_next_3_months.csv
```

---

## Output

The forecasting result is saved as:

```text
output/forecast_next_3_months.csv
```

Example forecast:

```text
month,forecast_number_of_sessions
2009-06,203
2009-07,190
2009-08,181
```
