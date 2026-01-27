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
```sql
CREATE STAGE weather_s3_stage
URL = 's3://weather-raw-data-sravya/raw/'
STORAGE_INTEGRATION = s3_weather_int
FILE_FORMAT = (TYPE = JSON);
```
<img width="1710" height="918" alt="Stage" src="https://github.com/user-attachments/assets/941ec6fd-599b-4efe-a2b4-d18d460a2485" />

Step 4: Snowpipe
```sql
create or replace pipe WEATHER_DB.PUBLIC.WEATHER_PIPE auto_ingest=true as COPY INTO raw_weather (city, temperature, humidity, wind_speed, event_time)
FROM (
  SELECT 
    $1:city::STRING,
    $1:temperature::FLOAT,
    $1:humidity::INT,
    $1:wind_speed::FLOAT,
    $1:event_time::TIMESTAMP
  FROM @weather_stage
);
```
<img width="1708" height="912" alt="SNOWPIPE" src="https://github.com/user-attachments/assets/ef2d5c16-248a-47c7-8344-daef339398bd" />

