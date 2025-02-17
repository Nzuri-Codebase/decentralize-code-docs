# Flask API Documentation

## Overview
The Flask API is designed to track user login and logout events, storing the data in InfluxDB for analysis. It provides endpoints for tracking user sessions and calculating session durations.

## Key Features
1. **Login Tracking**: Records user login events with timestamps.
2. **Logout Tracking**: Records user logout events and calculates session durations.
3. **InfluxDB Integration**: Stores all events in InfluxDB for time-series analysis.

## Endpoints
1. **`/track_login`**: Tracks user login events.
2. **`/track_logout`**: Tracks user logout events and calculates session durations.

## Requirements
- Python 3.8+
- Required Python packages:
    - flask
    - influxdb-client
    - python-dotenv
    - flask-cors

## Running the Application
By design, the application runs within the streamlit app but it can also run independently (albeit not very useful because it gets its meaning from the streamlit app) via the following terminal commands:
1. Install required packages:
```bash
pip install -r requirements.txt
```
2. Run the application:
```bash
python flask_api.py
```
3. Access the API at `http://localhost:5000`

## Error Handling
- The API includes basic error handling for:
    - Missing or invalid fields
    - InfluxDB connection errors
    - Unauthorized email domains

## Output
- All events are stored in InfluxDB under the bucket `decentralize_nzuri_web_traffic`.

## Limitations
- Requires specific email domain for login tracking.