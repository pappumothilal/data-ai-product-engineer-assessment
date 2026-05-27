# Weather Analytics Pipeline

## Project Overview

This project demonstrates a complete data pipeline built using Python, a public API, and Google BigQuery.

The goal of the pipeline is to automate the process of:

1. Extracting external data
2. Transforming raw API responses
3. Loading clean data into BigQuery
4. Running analytical SQL queries
5. Thinking through production deployment considerations

This project was built as part of the Data & AI Product Engineer assessment.

---

# Chosen API

## Open-Meteo API

Official Website:
https://open-meteo.com/

### Why I Chose This API

I selected the Open-Meteo API because:

- It is publicly accessible
- No authentication or API key is required
- The API provides clean structured JSON responses
- Weather data is ideal for transformation and analytics
- It allowed me to focus on pipeline engineering rather than authentication setup

The API provides forecast data such as:

- Maximum temperature
- Minimum temperature
- Rainfall
- Daily weather conditions

---

# Pipeline Architecture

```text
Open-Meteo API
      ↓
Python Extraction Script
      ↓
Data Transformation Layer
      ↓
BigQuery Loading Layer
      ↓
SQL Analytics Queries
```

---

# Technologies Used

| Layer | Technology |
|---|---|
| Programming Language | Python |
| API Requests | requests |
| Data Processing | pandas |
| Logging | logging |
| Environment Variables | python-dotenv |
| Cloud Warehouse | BigQuery |

---

# How to Run the Pipeline

## 1. Clone Repository

```bash
git clone <your-repository-url>
cd task-2-data-pipeline
```

---

## 2. Install Dependencies

```bash
pip install -r requirements.txt
```

---

## 3. Configure Google Credentials

Create a Google Cloud service account and download the JSON credentials file.

Set the environment variable:

### Mac/Linux

```bash
export GOOGLE_APPLICATION_CREDENTIALS='path/to/service-account.json'
```

### Windows

```bash
set GOOGLE_APPLICATION_CREDENTIALS=path/to/service-account.json
```

---

## 4. Run the Pipeline

```bash
python main.py
```

---

# BigQuery Setup

## Steps Followed

### 1. Open BigQuery Sandbox

I used the free BigQuery Sandbox provided by Google Cloud.

### 2. Create Dataset

Dataset Name:
```text
weather_analytics
```

### 3. Create Target Table

Table Name:
```text
weather_data
```

### 4. Configure Schema

The schema was designed to support analytical queries and future scalability.

---

# Final BigQuery Schema

| Field Name | Type |
|---|---|
| date | DATE |
| city | STRING |
| max_temperature | FLOAT |
| min_temperature | FLOAT |
| rainfall_mm | FLOAT |
| temperature_range | FLOAT |
| rain_indicator | INTEGER |
| weather_score | FLOAT |

---

# Data Transformation

The API returns nested JSON data that required cleaning and restructuring.

The transformation layer performs:

- Flattening nested structures
- Type conversion
- Null handling
- Derived field generation

---

# Derived Fields Added

| Field | Purpose |
|---|---|
| temperature_range | Measures daily temperature variation |
| rain_indicator | Indicates rainy day (1/0) |
| weather_score | Simplified analytical weather score |

Example transformation:

```python
weather_df["temperature_range"] = (
    weather_df["max_temperature"] - weather_df["min_temperature"]
)

weather_df["rain_indicator"] = (
    weather_df["rainfall_mm"] > 0
).astype(int)
```

---

# Error Handling

The pipeline includes basic production-oriented error handling.

## Scenarios Handled

- API failures
- Request timeouts
- Missing fields
- Invalid responses
- Connection interruptions

Example:

```python
try:
    response = requests.get(API_URL, timeout=10)
    response.raise_for_status()

except requests.exceptions.RequestException as e:
    logging.error(f"API request failed: {e}")
```

---

# Logging

Logging was implemented to improve observability and debugging.

Example logs:

```text
INFO - Starting extraction
INFO - API request successful
INFO - Transformation completed
INFO - BigQuery load completed
ERROR - API request failed
```

---

# Loading Data into BigQuery

The transformed pandas DataFrame is loaded directly into BigQuery using the Google Cloud Python SDK.

Example:

```python
from google.cloud import bigquery

client = bigquery.Client()

job = client.load_table_from_dataframe(
    weather_df,
    table_id
)

job.result()
```

---

# SQL Summary Query

The following query demonstrates that the stored data is queryable and analytically useful.

```sql
SELECT
    city,
    AVG(max_temperature) AS avg_max_temperature,
    SUM(rain_indicator) AS rainy_days,
    AVG(temperature_range) AS avg_temp_range
FROM weather_data
GROUP BY city
ORDER BY avg_max_temperature DESC;
```

---

# Example SQL Output

| city | avg_max_temperature | rainy_days | avg_temp_range |
|---|---|---|---|
| Hyderabad | 36.4 | 3 | 10.2 |
| Chennai | 34.8 | 5 | 8.6 |

---

# Production Thinking (Step 5)

## 1. Scheduling the Pipeline

If this pipeline were deployed in production, I would automate it using:

- Google Cloud Scheduler
- Apache Airflow
- GitHub Actions
- Cron jobs

Preferred solution:
- Cloud Scheduler + Cloud Run

Reason:
- Simple deployment
- Low operational overhead
- Cost-effective scaling

---

# 2. Failure Monitoring

To monitor failures and reliability:

- Cloud Logging
- Email alerts
- Retry mechanisms
- Slack notifications
- Health checks

This would ensure failures are detected quickly and resolved before impacting downstream systems.

---

# 3. Scaling to 10x Data Volume

If data volume increased significantly, I would improve the system by:

## Data Processing
- Batch processing
- Parallel API requests
- Incremental extraction

## Infrastructure
- Docker containerization
- Airflow orchestration
- Kubernetes or Cloud Run deployment

## Storage Optimization
- Partitioned BigQuery tables
- Clustered tables
- Query optimization

## Monitoring
- Centralized observability dashboards
- Data quality validation
- SLA tracking

---

# Trade-Off Decisions

| Decision | Trade-Off |
|---|---|
| Open-Meteo API | Simpler setup but less business complexity |
| Batch pipeline | Easier implementation than streaming |
| BigQuery Sandbox | Free but limited compared to full GCP |
| Minimal transformations | Faster delivery and maintainability |

---

# What I Would Improve With More Time

If given more time, I would add:

- Automated testing
- CI/CD pipeline
- Docker deployment
- Airflow DAG scheduling
- Data quality framework
- Dashboard visualization layer
- Historical trend analysis

---

# Walkthrough Summary

This project was designed to demonstrate practical data engineering fundamentals rather than over-engineering the solution.

My main focus areas were:

- Reliable data extraction
- Clean transformation logic
- Structured BigQuery storage
- Production-oriented thinking
- Simplicity and maintainability

I intentionally kept the architecture lightweight and understandable while still incorporating best practices such as:

- logging,
- parameterization,
- error handling,
- schema design,
- and scalability planning.

If this were developed further, the next priorities would be automation, testing, and orchestration improvements.

---

# Conclusion

This pipeline demonstrates an end-to-end workflow for:

- extracting external data,
- transforming raw API responses,
- storing analytical datasets in BigQuery,
- and planning for production scalability.

The solution prioritizes clarity, reliability, maintainability, and practical engineering decisions.
