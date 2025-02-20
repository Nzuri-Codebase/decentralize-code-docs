# Informed Delivery

## Overview
Highlighted below is the documentation of the source code of the application designed to process and analyze email campaign performance data from Excel and CSV files of the Informed Delivery service. The application accepts a compressed folder containing files organized by month, processes the data, and provides visualizations of key email performance metrics including open rates and click-through rates.

## Requirements
1. Python 3.8+
2. Required Python packages:
    - streamlit
    - pandas
    - numpy
    - plotly
    - zipfile
    - tempfile

## File Structure
- The application consists of two main files:
    - `get_rates.py` - Main application logic
    - `get_rates_support.py` - Supporting functions and utilities

## Data Requirements
1. Input must be a ZIP file containing Excel or CSV files
2. Folder structure must follow: `data-folder/month/file.xlsx` or `data-folder/month/file.csv`
3. Expected columns in the files:
    - campaign_title
    - brand_display_name
    - campaign_code
    - dm_audience
    - mailpieces
    - emails
    - email_open
    - click_through

## Main Functions

### **`get_rates.py`**

#### `informed_main()`
The main function that is run by the Streamlit application.

**Functionality:**

1. Sets up the Streamlit interface
2. Accepts a ZIP file upload
3. Processes the uploaded files
4. Aggregates and analyzes data
5. Generates visualizations

**Key Features:**
1. Handles ZIP file extraction
2. Processes Excel and CSV files recursively
3. Aggregates data across multiple campaigns
4. Creates interactive visualizations using Plotly

### `get_rates_support.py`

#### `list_files_recursive(directory)`
Recursively lists files in a directory structure.

**Parameters:**
- `directory` (str): Root directory to search

**Returns:**
- Dictionary (dict) with month as key and list of file paths as value

#### `load_month_dfs(month_dirs)`
Loads and processes files into DataFrames.

**Parameters:**
- `month_dirs` (dict): Dictionary of file paths by month

**Returns:**
- Dictionary of DataFrames organized by month

#### `aggregate_data(df)`
Aggregates campaign data.

**Parameters:**
- `df` (DataFrame): Raw DataFrame to process

**Returns:**
- Aggregated DataFrame with calculated metrics (Dataframe)

#### `get_campaigns(data_frames_by_month)`
Extracts and calculates campaign metrics.

**Parameters:**
- `data_frames_by_month` (dict): Dictionary of DataFrames by month

**Returns:**
- Dictionary of campaign metrics by month

#### `get_click_open_rate(month_campaigns)`
Calculates click and open rates.

**Parameters:**
- `month_campaigns` (dict)1: Dictionary of campaign metrics

**Returns:**
- DataFrame with calculated rates

#### `plot_rates(df)`
Creates visualizations for open and click rates.

**Parameters:**
- `df` (DataFrame): DataFrame containing rate data

**Returns:**
- Two Plotly Figure objects (open rate and click rate)

## Running the Application
The application can be run independent of other applications within the Honda scope.

1. Install required packages:
```bash
pip install streamlit pandas numpy plotly
```
2. Run the application:
```bash
streamlit run get_rates.py
```
3. Access the application in your web browser at `http://localhost:8501`

## Error Handling
- The application includes basic error handling for:
    - File upload errors
    - Missing or invalid data files
    - Data processing errors
    - Visualization creation errors

## Output
- The application provides:
    - List of months found in the data
    - Interactive visualizations of click and open rates over time
    - Excel file output of processed data

## Limitations
- Requires specific file structure and naming conventions
- Assumes consistent column names in all files