# Streamlit Applications

## Overview
The Streamlit applications are designed to process and analyze data for both Honda and Nissan accounts. They handle tasks such as email campaign analysis, remedy data trends, and ROI calculations.

## Applications
1. **Honda**:
    - Ask Dave: Processes monthly conversion data.
    - High Deliverability: Analyzes email campaign delivery data.
    - Remedy Spikes: Visualizes remedy data trends.
    - Informed Delivery: Tracks email campaign performance metrics.
2. **Nissan**:
    - Apprentice Placement: Tracks apprentice and graduate placement data.
    - Nissan ROI: Calculates and analyzes ROI metrics.

## Requirements
- Python 3.8+
- Required Python packages:
  - streamlit
  - pandas
  - numpy
  - plotly
  - openpyxl

## Running the Applications
1. Install required packages:
   ```bash
   pip install -r requirements.txt
   ```
2. Run the application:
   ```bash
   streamlit run <application_name>.py
   ```
3. Access the application in your web browser at `http://localhost:8501`

## Error Handling
- The applications include basic error handling for:
    - File upload errors
    - Data processing errors
    - Visualization creation errors

## Output
- The applications provide:
    - Interactive visualizations
    - Summary reports
    - Downloadable Excel files

## Limitations
- Requires specific file structure and naming conventions.
- Assumes consistent column names in all files.