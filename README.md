# Real-Time Claims Adjudication System

## Project Overview
This project implements a **data pipeline for a healthcare claims adjudication system** using **Databricks Medallion Architecture**.  
The pipeline processes healthcare claim data, validates eligibility, calculates payer liability, and generates analytics-ready datasets for reporting.

The solution supports **insurance operations teams and hospital management** by providing insights into claim approvals, liabilities, and claim trends.

---

# Business Problem

Healthcare insurance companies process a large number of claims submitted by hospitals.  
Manual claim processing leads to:

- Delayed claim approvals
- Lack of transparency in claim settlement
- Difficulty tracking insurance liability
- Limited analytics for operational decision-making

This project simulates a **claims adjudication workflow** where claims are validated against policy coverage, eligibility is checked, and payments are processed.

---

# Business Process Flow

### Step 1 – Claim Submission
Hospitals submit claims containing patient details, provider information, procedures, and claim amount.

### Step 2 – Eligibility Validation
The system verifies:
- Patient eligibility
- Insurance policy coverage
- Plan limits and copay rules

### Step 3 – Claim Adjudication
Based on policy rules:
- Claims are **approved or rejected**
- Approved amount is calculated
- Insurance liability is determined

### Step 4 – Payment Processing
Payments are processed and claim settlement status is updated.

### Output
- Claim approval status
- Approved claim amount
- Payment information
- Remaining balance

---

# Project Architecture

The pipeline is built using **Databricks Medallion Architecture**.


Raw Data (Databricks Volumes)
↓
Bronze Layer (Raw Delta Tables)
↓
Silver Layer (Cleaned & Transformed Data)
↓
Gold Layer (Star Schema for Analytics)
↓
Power BI Reports



---

# Data Sources

The project uses multiple datasets to simulate healthcare operations:

- Patients
- Providers
- Payers
- Policies
- Claims
- Claim Lines
- Payments

These files are stored in **Databricks Volumes** before ingestion.

---

# Bronze Layer – Raw Data Ingestion

Data is ingested from **Databricks Volumes** into the Bronze layer.

Characteristics:

- Raw data ingestion
- Minimal transformations
- Stored as Delta tables
- Schema applied during ingestion

Tables created:

- patients
- providers
- payers
- policies
- claims
- claim_lines
- payments

---

# Silver Layer – Data Transformation

The Silver layer processes and cleans the raw Bronze data.

Steps performed:

1. Created Silver table structures
2. Initial data load from Bronze
3. Applied merge logic for selected dimension tables
4. Flattened nested JSON structures
5. Standardized data types

Tables created:
silver_patient
silver_provider
silver_payer
silver_policy
silver_claims
silver_claim_lines
silver_payments


Dimension tables were handled with **merge logic**, while transactional tables were loaded directly.

---

# Gold Layer – Analytics Model

The Gold layer provides an **analytics-ready star schema** for reporting.

### Dimension Tables
- dim_patient
- dim_provider
- dim_policy
- dim_payer

### Fact Tables
- fact_claims
- fact_payments

Only **active records from Silver** were moved into the Gold layer for dimension tables.  
Transactional data such as claims and payments were loaded directly.

---

# Pipeline Automation

A **Databricks Job** was created to automate the pipeline execution.

Job Workflow:

1. Bronze ingestion
2. Silver transformations
3. Gold table creation

The job runs using a **scheduled trigger** to process updates and merge changes.

---

# Reporting and Analytics

Power BI dashboards were created using the **Gold layer tables**.

Key business insights include:

- Claim approval ratio
- Claims by state
- Claims by gender
- Claims by specialty
- Patient distribution by insurance plan
- Claim amount vs payment comparison
- Insurance liability analysis

These dashboards support **insurance operations teams and hospital management**.

---

# Technology Stack

- **Databricks**
- **Delta Lake**
- **PySpark**
- **SQL**
- **Power BI**
- **Git (Version Control)**

---

# Conclusion

This project demonstrates how a **Medallion Architecture pipeline** can be used to process healthcare claims data and generate actionable insights.

The system enables:

- Automated claim processing
- Reliable data pipelines
- Scalable architecture
- Analytics-driven decision making

---
