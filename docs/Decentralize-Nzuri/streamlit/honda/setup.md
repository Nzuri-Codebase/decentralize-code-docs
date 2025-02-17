# Honda Setup Guide

## Prerequisites
- Python 3.8+
- Required Python packages:
  - streamlit
  - pandas
  - numpy
  - plotly
  - openpyxl

## Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/your-repo/decentralize-nzuri.git
   ```
2. Navigate to the Honda directory:
   ```bash
   cd decentralize-nzuri/src/apps/streamlit/honda
   ```
3. Install the required packages:
   ```bash
   pip install -r requirements.txt
   ```

## Running the Applications
To run any Honda application, use the following command:
```bash
streamlit run <application_name>.py
```
Replace `<application_name>` with the specific application file (e.g., `ask_dave.py`, `high_del.py`) for a file specific service or use `main.py` to run the whole streamlit application.

## Configuration
- Ensure input files follow the required structure and naming conventions.
- Place input files in the appropriate directory before running the application.
