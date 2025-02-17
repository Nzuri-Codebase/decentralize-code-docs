# Decentralize Nzuri Web App

## Overview
This is the source code documentation of the Decentralize Nzuri Web app. The app can run as a unit or it could be run using the independent services that it automates (Nissan and Honda).

## Set up
The first thing to do is to ensure that all the python packages are installed. To do this, from the root of the repository, one would run the following command on your terminal:
```bash
pip install -r requirements.txt
```

## Running the app
To run the app itself it as a unit, one would need to change the directory from the root of the repository to the src repository then run the following command on your terminal:
```bash
streamlit run main.py
```

# Decentralize Nzuri Web App

## Overview
This is the source code documentation of the Decentralize Nzuri Web app. The app can run as a unit or it could be run using the independent services that it automates (Nissan and Honda). The main application (`main.py`) serves as the entry point for the Streamlit-based web interface, integrating authentication, user tracking, and navigation to various Honda and Nissan applications.

## Key Features
1. **Authentication**: Integrates Microsoft Azure AD for secure user login and logout.
2. **User Tracking**: Tracks user sessions and stores login/logout data in InfluxDB.
3. **Navigation**: Provides access to Honda and Nissan applications:
    - Honda: Ask Dave, High Deliverability, Remedy Spikes, Informed Delivery.
    - Nissan: Apprentice Placement, ROI.

## Set up
* Fist ensure that you have cloned the repository using the terminal command:
 ```bash
git clone https://github.com/Nzuri-Codebase/decentralize-nzuri.git
```
* The next thing to do is to ensure that all the python packages are installed. To do this, from the root of the repository, one would run the following command on your terminal:
```bash
pip install -r requirements.txt
```

## Running the App
To run the app as a unit, change the directory from the root of the repository to the `src` directory and run the following command:
```bash
streamlit run main.py
```

The app can work locally, but since the authentication process relies on internet connectivity, ensure that the Flask API URL is correctly configured in the `.env` file.

## Main Application (`main.py`) Summary
The `main.py` file is the central entry point for the Decentralize Nzuri web application. It includes the following functionality:
1. **Authentication**:
   - Uses Microsoft Azure AD for secure login.
   - Validates user emails against organizational records.
2. **User Tracking**:
   - Logs user login and logout events.
   - Calculates session durations and stores data in InfluxDB.
3. **Navigation**:
   - Provides a user interface to access Honda and Nissan applications.
   - Displays a welcome message and session information for logged-in users.
4. **Error Handling**:
   - Handles authentication failures, file upload errors, and data processing issues.

## Requirements
- Python 3.8+
- Required Python packages:
    - streamlit
    - pandas
    - numpy
    - msal
    - influxdb-client
    - python-dotenv

## Error Handling
- The application includes basic error handling for:
    - Authentication failures
    - File upload errors
    - Data processing errors

## Output
- The application provides:
    - Secure user authentication
    - Session tracking and logging
    - Navigation to Honda and Nissan applications

## Limitations
- Requires internet connectivity for authentication.
- Assumes consistent column names in all input files.