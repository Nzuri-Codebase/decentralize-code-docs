# InfluxDB Documentation

## Overview
InfluxDB is used to store time-series data for the Decentralize Nzuri web application. It tracks user login and logout events, providing insights into user activity over time.

## Key Features
1. **Time-Series Data Storage**: Efficiently stores and retrieves time-series data.
2. **Event Tracking**: Tracks user login and logout events.
3. **Session Duration Calculation**: Calculates and stores session durations.

## Configuration
- **Token**: `INFLUXDB_TOKEN`
- **Username**: `INFLUXDB_USERNAME`
- **Password**: `INFLUXDB_PASSWORD`
- **Organization**: `NzuriStrategy`
- **Bucket**: `decentralize_nzuri_web_traffic`
- **URL**: `http://localhost:8086` (local) or `http://<container-name>.eastus.azurecontainer.io:8086` (Azure)

## Running the Application
1. Ensure InfluxDB is running locally or on Azure.
2. Configure the `.env` file/set environment variables with the correct credentials.
3. Start the Flask API to begin tracking events.

## Error Handling
- The application includes basic error handling for:
    - Connection errors
    - Authentication failures
    - Data write errors

## Output
- All events are stored in InfluxDB under the bucket `decentralize_nzuri_web_traffic`.

## Limitations
- Limited to tracking login and logout events.
