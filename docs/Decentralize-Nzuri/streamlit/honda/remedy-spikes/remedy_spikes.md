# Remedy Spikes

## Overview
Highlighted below is the documentation of the source code of the application designed to analyze and visualize remedy data trends using moving averages. The application processes Excel files containing remedy data and generates interactive visualizations of the moving averages over time.

## Requirements
1. Python 3.8+
2. Required Python packages:
    - streamlit
    - pandas
    - numpy
    - plotly

## File Structure
- The application consists of two main files:
    - `pg.py` - Main application logic
    - `pg_support.py` - Supporting functions and utilities

## Data Requirements
1. Input must be an Excel file (.xlsx)
2. Expected columns in the file:
    - VEH_RECALL_CMPLTN_DT (date column)
    - GRAND_TOTAL (will be dropped)
    - Other columns containing remedy data

## Main Functions

### **`pg.py`**

#### `pg_main()`
The main function that is run by the Streamlit application.

**Functionality:**

1. Sets up the Streamlit interface
2. Accepts an Excel file upload
3. Processes the uploaded file
4. Calculates moving averages
5. Generates visualizations

**Key Features:**

1. Handles Excel file upload
2. Calculates 7-day moving averages
3. Allows date range filtering
4. Creates interactive visualizations using Plotly

### `pg_support.py`

#### `calculate_moving_average(df, window=7)`
Calculates moving averages for each column in the DataFrame.

**Parameters:**

- `df`: Input DataFrame
- `window`: Window size for moving average (default: 7)

**Returns:** 

- DataFrame with moving averages

#### `slice_df(df, start_date, end_date)`
Filters DataFrame based on date range.

**Parameters:**

- `df`: Input DataFrame
- `start_date`: Start date for filtering (optional)
- `end_date`: End date for filtering (optional)

**Returns:** 

- Filtered DataFrame

#### `plot_ma(df)`
Creates a line chart visualization of moving averages.

**Parameters:** 

- `df`: DataFrame containing moving average data

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
streamlit run pg.py
```
3. Access the application in your web browser at `http://localhost:8501`

## Error Handling
- The application includes basic error handling for:
    - File upload errors
    - Data processing errors
    - Visualization creation errors

## Output
- The application provides:
    - Preview of processed data
    - Interactive visualization of moving averages
    - Ability to filter data by date range

## Limitations
- Requires specific column names in the input file
- Limited to Excel file format