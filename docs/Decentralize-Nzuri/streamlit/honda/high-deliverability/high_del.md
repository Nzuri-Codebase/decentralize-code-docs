# High Deliverability

## Overview
Highlighted below is the documentation of the source code of the application designed to process and analyze email campaign delivery data from Excel and CSV files of the High Deliverability service. The application accepts a compressed folder containing files organized by month, processes the data, and provides visualizations of key email performance metrics.

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
    - `delivery.py` - Main application logic
    - `delivery_support.py` - Supporting functions and utilities

## Data Requirements
1. Input must be a ZIP file containing Excel or CSV files
2. Folder structure must follow: `data-folder/month/file.xlsx` or `data-folder/month/file.csv`
3. Expected columns in the files:
    - Unnamed: 0 (contains metric names)
    - Unnamed: 1 (contains metric values)
4. Required metrics in the data:
    - Opportunity Name/Company Name
    - Campaign
    - Deployment Date
    - Ordered
    - Delivered
    - Unique Opens
    - Unique Clicks To Opens

## Main Functions

### **`delivery.py`**

#### `highdel_main()`
The main function that is run by the Streamlit application.

**Functionality:**

1. Sets up the Streamlit interface
2. Accepts a ZIP file upload
3. Processes the uploaded files
4. Cleans and combines data
5. Generates visualizations

**Key Features:**

1. Handles ZIP file extraction
2. Processes Excel and CSV files recursively
3. Combines data from multiple files
4. Creates interactive visualizations using Plotly

### `delivery_support.py`

#### `list_files_recursive(directory)`
Recursively lists files in a directory structure.

**Parameters:**
- `directory`: Root directory to search

**Returns:**

- Dictionary with month as key and list of file paths as value
- Number of directories found

#### `get_df_dict(dirs)`
Reads and processes files into DataFrames.

**Parameters:**
- `dirs`: Dictionary of file paths by month

**Returns:**
- Dictionary of DataFrames with processed data

#### `clean_file(df)`
Cleans and processes individual DataFrames.

**Parameters:**
- `df`: Raw DataFrame to process

**Returns:**

- Cleaned DataFrame
- Campaign name
- Deployment date

#### `calculate_percentage(row, total, delivered_total, unique_opens_total)`
Calculates percentage metrics for email performance.

**Parameters:**

- `row`: DataFrame row to calculate
- `total`: Total number of emails
- `delivered_total`: Number of delivered emails
- `unique_opens_total`: Number of unique opens

**Returns:**
- Calculated percentage value

#### `plot_clicks(df)`
Creates a bar chart visualization for unique clicks to opens.

**Parameters:**
- `df`: DataFrame containing the data

**Returns:**
- Plotly Figure object

## Running the Application
The application can be run independent of other applications within the Honda scope.

1. Install required packages:
```bash
pip install streamlit pandas numpy plotly
```
2. Run the application:
```bash
streamlit run delivery.py
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
    - Number of files processed
    - List of months found in the data
    - Interactive visualization of Unique Clicks to Opens by month

## Limitations
- Requires specific file structure and naming conventions
- Assumes consistent metric names in all files