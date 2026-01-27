# Snowflake Commands Used (Reference)

This project was executed using Snowflake Worksheets.  
Below are the key SQL commands used during the pipeline setup.

Step 1: Create Database & Table

```sql
CREATE DATABASE WEATHER_DB;
USE DATABASE WEATHER_DB;
USE SCHEMA PUBLIC;

CREATE TABLE RAW_WEATHER (
  city STRING,
  temperature FLOAT,
  humidity INT,
  wind_speed FLOAT,
  event_time TIMESTAMP,
  ingestion_time TIMESTAMP DEFAULT CURRENT_TIMESTAMP()
);
```

<img width="1698" height="922" alt="WeatherDB_SF" src="https://github.com/user-attachments/assets/35785125-5d0c-42fc-8ae3-0b71acbcc2ff" />

#
Step 2: Storage Integration
```sql
CREATE STORAGE INTEGRATION s3_weather_int
TYPE = EXTERNAL_STAGE
STORAGE_PROVIDER = S3
ENABLED = TRUE
STORAGE_ALLOWED_LOCATIONS = ('s3://weather-raw-data-sravya/raw/');
```
<img width="1703" height="916" alt="StorageIntegration" src="https://github.com/user-attachments/assets/d0c7658e-e73c-4eed-8842-f1cee8a33c65" />


Step 3: External Stage

Step 4: Snowpipe
