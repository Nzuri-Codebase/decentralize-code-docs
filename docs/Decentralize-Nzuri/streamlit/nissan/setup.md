# Nissan Setup Guide

## Prerequisites
- Python 3.8+
- Required Python packages:
    - streamlit
    - pandas
    - numpy
    - openpyxl

## Installation
- Clone the repository:
```bash
git clone https://github.com/your-repo/decentralize-nzuri.git
```
- Navigate to the Nissan directory:
```bash
cd decentralize-nzuri/src/apps/streamlit/nissan
```
- Install the required packages:
```bash
pip install -r requirements.txt
```

## Running the Applications
To run any Nissan application, use the following command:
```bash
streamlit run <application_name>.py
```
Replace `<application_name>` with the specific application file (e.g., `apprentice_dev.py`, `nissan_roi.py`) to run a specific file or use `main.py` to run the whole streamlit application.

## Configuration
- Ensure input files follow the required structure and naming conventions.
- Place input files in the appropriate directory before running the application.