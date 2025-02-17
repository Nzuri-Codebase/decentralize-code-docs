# Ask Dave

## Overview
Highlighted below is the documentation of the source code of the application designed to process and analyze monthly conversion data from Excel files of the Ask Dave service. The application accepts a compressed folder containing Excel files organized by month, processes the data, and provides visualizations and summary reports.

## Requirements
1. Python 3.8+
2. Required Python packages:
    - streamlit
    - pandas
    - numpy
    - plotly
    - xlsxwriter
    - openpyxl

## File Structure
- The application consists of two main files:
    - `ask_dave.py` Main application logic
    - `dave_support.py` Supporting functions and utilities

## Data Requirements
1. Input must be a ZIP file containing Excel files
2. Folder structure must follow: `data-folder/month/file.xlsx`
3. Each Excel file must contain a sheet named 'Daily Break Down'
4. Expected columns in the Excel sheet:
    - Date
    - Actual Conversions
    - Airbag Conversions
    - Airbag Conversion %
    - After Hours Conversions
    - After Hours Conversion %
    - Callback Requests

## Main Functions

### **`ask_dave.py`**

#### `dave_main()`
The main function that is run by the Streamlit application.

**Functionality:**

1. Sets up the Streamlit interface
2. Accepts a ZIP file upload
3. Processes the uploaded files
4. Generates monthly summaries
5. Creates visualizations
6. Provides download option for summary data

**Key Features:**

1. Handles ZIP file extraction
2. Processes Excel files recursively
3. Generates monthly summary statistics
4. Creates interactive visualizations using Plotly
5. Provides data download functionality

### `dave_support.py`

#### `plot_bar_summary(df, column)`
Creates a bar chart visualization for a specified column.

**Parameters:**
- `df`: Pandas DataFrame containing the data
- `column`: Column name to plot

**Returns:**
- Plotly Figure object

#### `plot_line_summary(df, column)`
Creates a line chart visualization for a specified column.

**Parameters:**
- `df`: Pandas DataFrame containing the data
- `column`: Column name to plot

**Returns:**
- Plotly Figure object

#### `list_files_recursive(directory)`
Recursively lists files in a directory structure.

**Parameters:**
- `directory`: Root directory to search

**Returns:**
- Dictionary with month as key and list of file paths as value

#### `download_summary_as_excel(df, file_name)`
Creates a downloadable Excel file from a DataFrame.

**Parameters:**

- `df`: Pandas DataFrame to export
- `file_name`: Name of the output file (default: "monthly_summary.xlsx")

## Running the Application
The application can be run independent of other applications within the Honda scope.

1. Install required packages:
```bash
pip install streamlit pandas numpy plotly xlsxwriter openpyxl
```
2. Run the application:
```bash
streamlit run ask_dave.py
```
3. Access the application in your web browser at `http://localhost:8501`

## Error Handling
- The application includes basic error handling for:
    - File upload errors
    - Missing or invalid Excel sheets
    - Data processing errors
    - Visualization creation errors

## Output
- The application provides:
    - Monthly summary preview (first and last 10 months)
    - Interactive visualizations:
        - Airbag Conversion %
        - Total Actual Conversions
    - Downloadable Excel file containing full monthly summary

## Limitations
1. Requires specific file structure and naming conventions
2. Assumes consistent column names in all Excel files