# aws-snowflake-weather-pipeline

🌩️ Cloud-Native Weather Data Pipeline (AWS + Snowflake)

📌 Overview

This project implements an end-to-end cloud data engineering pipeline that ingests real-time weather data from an external API, stages it in AWS S3, and automatically loads it into Snowflake using Snowpipe.

The pipeline demonstrates production-grade ELT design, secure cloud integrations, and automated ingestion patterns commonly used in large-scale data platforms.

🏗️ Architecture

Flow:

<img width="906" height="338" alt="image" src="https://github.com/user-attachments/assets/80ab248f-6e93-4167-9009-ee071350c7fc" />


Key Design Principles:
	•	Serverless ingestion
	•	Immutable raw data storage
	•	Automated, event-driven loading
	•	Secure IAM-based access

⸻

⚙️ Tech Stack
	•	AWS Lambda (Python)
	•	Amazon S3
	•	Snowflake (Snowpipe, External Stage, Storage Integration)
	•	SQL
	•	IAM (AWS Security)
	•	JSON Data Format

⸻

📂 Data Flow Breakdown
	1.	AWS Lambda fetches weather data from an external API
	2.	Raw JSON files are written to an S3 raw/ folder
	3.	Snowflake Storage Integration securely connects to S3
	4.	External Stage references the S3 raw location
	5.	Snowpipe automatically ingests new files into Snowflake
	6.	Data is stored in a structured Snowflake table for analytics


  🔐 Security & Governance
	•	IAM Role-based access between AWS and Snowflake
	•	Explicit S3 location whitelisting
	•	Separation of compute, storage, and ingestion layers
	•	Raw data preserved for reproducibility

⸻

🎯 Why This Project Matters
	•	Demonstrates real-world data engineering workflows
	•	Shows ability to work across cloud platforms
	•	Emphasizes reproducibility and data provenance
	•	Designed to scale for ML and analytics workloads

⸻

🚀 Future Enhancements
	•	Add data quality checks
	•	Partitioned Snowflake tables
	•	dbt transformations
	•	ML feature extraction layer
	•	Monitoring & alerting


