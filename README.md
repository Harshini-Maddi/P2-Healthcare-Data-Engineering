Healthcare Patient Analytics Pipeline Project Overview

The Healthcare Patient Analytics Pipeline is a data engineering project designed to ingest, clean, transform, and analyze patient health records using AWS S3, Databricks, PySpark, and Delta Lake.

The pipeline processes CSV-based patient health records and follows a Bronze → Silver → Gold architecture to produce reliable, analytics-ready healthcare data. It includes data quality checks, error handling, daily batch processing, and Git integration.

Data Source

The pipeline uses CSV files based on Kaggle's Heart Disease Dataset.

Expected S3 location:

s3://bucket/raw/health_records/YYYY/MM/DD/

The data contains patient information such as vitals and diagnoses.

Data Lake Layers Layer Table Description Bronze health_catalog.raw.patient_records Raw patient records Silver health_catalog.processed.patient_cleaned Cleaned and standardized patient data Gold health_catalog.analytics.health_metrics Aggregated patient risk metrics

Pipeline Tasks

Data Ingestion Read CSV files from AWS S3 Infer and validate schemas Handle malformed records Partition data by year and month
Data Cleansing & Transformation Remove duplicate records Standardize dates and medical codes Join with dimension tables such as hospitals Apply patient risk-scoring logic Enrich records with demographic information
Data Processing & Storage Write raw data to the Bronze layer Upsert cleaned data into the Silver layer Generate aggregated Gold tables Perform Delta Lake optimization and vacuum operations
Data Quality & Error Handling Validate record counts and schemas Perform data quality checks Capture ETL errors Store errors in: health_catalog.logs.etl_errors Send email alerts for data anomalies.
Orchestration
The pipeline is orchestrated using Databricks Workflows and is scheduled as a daily batch job at 2:00 AM UTC.

Technology Stack Databricks PySpark Delta Lake AWS S3 boto3 pytest Git / AWS CodeCommit Databricks Workflows

The Databricks environment uses a standard autoscaling cluster with 4–16 workers and m5.large nodes.

Testing

The pipeline includes:

Unit testing for key transformation logic Schema validation Record-count validation Testing with Kaggle sample data QA validation and sign-off Performance & Optimization

The pipeline is designed for scalable healthcare analytics using:

Data partitioning Delta Lake optimization Periodic VACUUM operations Autoscaling Databricks clusters Efficient Bronze, Silver, and Gold data processing Project Objectives

The primary objective is to process patient data and create reliable datasets that support predictive analytics and improved healthcare outcomes.

Key Outcomes Scalable Data Pipeline – Processes healthcare data using S3 and Delta Lake. Data Quality Assurance – Provides validation and robust error handling. Performance Optimization – Uses partitioning and Delta Lake optimizations. Version Control & Collaboration – Supports Git-based development workflows. Business Impact – Enables predictive patient risk analytics to support improved healthcare outcomes. Future Enhancements

Potential enhancements include:

Real-time patient data ingestion Advanced ML-based risk prediction Interactive healthcare dashboards Automated data-quality monitoring Additional healthcare data sources Disclaimer

This project is intended for educational and data-engineering demonstration purposes. It should not be used to make real-world medical diagnoses or treatment decisions.
