# Aws-project-Covid-19
# COVID Data Engineering Pipeline (AWS + PySpark)

##  Project Overview

This project demonstrates an end-to-end **Data Engineering pipeline** built using **AWS services and PySpark**, following the **Medallion Architecture (Bronze → Silver → Gold)**.

The pipeline processes COVID-19 datasets, transforms raw data into structured analytical tables, and enables querying using Athena and Redshift.

---

## Architecture

```
CSV Files
   ↓
S3 (Bronze Layer - Raw Data)
   ↓
PySpark Processing
   ↓
S3 (Silver Layer - Cleaned Data)
   ↓
PySpark Transformations
   ↓
S3 (Gold Layer - Fact & Dimension Tables)
   ↓
Athena (Query Layer)
   ↓
Redshift (Serving Layer)
```

---

##  Tech Stack

* Storage: Amazon S3
* Processing: PySpark
* Data Warehouse: Amazon Redshift
* Query Engine: Amazon Athena
* Language: Python
* Format: CSV → Parquet

---

##  Bronze Layer (Raw Data)

* Raw CSV files stored in S3
* Data sources:

  * NYTimes COVID dataset
  * COVID Tracking Project
  * State lookup file

 Example:

```
s3://rajshreetakeo/covid/bronze/
```

---

##  Silver Layer (Data Cleaning & Standardization)

* Cleaned and standardized datasets using PySpark
* Converted data into Parquet format
* Applied transformations:

  * Type casting
  * Date formatting
  * Data normalization

 Output:

```
s3://rajshreetakeo/covid/silver/
```

Tables:

* `cases_standardized`
* `testing_standardized`

---

##  Gold Layer (Data Modeling)

Built analytical **fact and dimension tables**:

### Dimension Tables

* `dim_date`
* `dim_state`

### Fact Tables

* `fact_cases_state_daily`
* `fact_testing_state_daily`

 Output:

```
s3://rajshreetakeo/covid/covid_gold/
```

---

##  Athena (Query Layer)

Registered Gold tables in Athena and performed analytical queries such as:

* Top 5 states by new COVID cases
* Positivity rate trends
* Daily cases vs testing analysis

---

##  Redshift (Serving Layer)

Loaded Gold data into Redshift using COPY commands.

* Created star schema
* Loaded Parquet data from S3
* Enabled fast analytical queries

---

##  Sample Queries

### Top 5 States by Cases

```sql
SELECT s.state_name, f.new_cases
FROM covid_gold_db.fact_cases_state_daily f
JOIN covid_gold_db.dim_state s
  ON s.state_code = f.state_code
ORDER BY f.new_cases DESC
LIMIT 5;
```

---

##  Key Learnings

* Built a complete ETL pipeline using PySpark
* Implemented Medallion Architecture
* Worked with S3, Athena, and Redshift
* Debugged real-world issues (schema mismatch, file formats)
* Understood data modeling (fact & dimension tables)

---

##  Project Structure

```
project/
│
├── bronze/
├── silver.py
├── covid_gold.py
├── output/
│   ├── silver/
│   └── gold/
└── README.md
```

---

##  Conclusion

This project showcases the design and implementation of a **scalable data pipeline** using modern data engineering tools. It demonstrates how raw data can be transformed into meaningful insights using cloud-based technologies.

---

##  Author

Rajshree Thapa
