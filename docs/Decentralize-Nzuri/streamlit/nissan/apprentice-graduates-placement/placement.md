# Apprentice Placement

## Overview
Highlighted below is the documentation of the source code of the application designed to process and analyze apprentice and graduate placement data. It tracks student transitions, identifies new students, and generates updated placement reports. The application accepts Excel files containing weekly status reports and placement trackers, processes the data, and provides downloadable updated Excel files.

## Requirements
1. Python 3.8+
2. Required Python packages:
    - streamlit
    - pandas
    - numpy
    - openpyxl

## File Structure
- The application consists of two main files:
    - `apprentice_dev.py` - Main application logic
    - `apprentice_support.py` - Supporting functions and utilities

## Data Requirements
1. Input must be Excel files (.xlsx)
2. Expected files:
    - NTTA Status Report (two weeks: previous and current)
    - Apprentice Placement Over Time tracker
    - Fulltime Graduates Hired Tracker
3. Expected columns in the files:
    - LMSID (unique student identifier)
    - First_Name
    - Last_Name
    - Employee_Student_Full_Name
    - Date columns in format `mm-dd-yyyy`

## Main Functions

### **`apprentice_dev.py`**

#### `apprentice_main()`
The main function that runs the Streamlit application.

**Functionality:**

1. Sets up the Streamlit interface
2. Accepts file uploads for:
    - NTTA Status Reports (two weeks)
    - Apprentice Placement Over Time tracker
    - Fulltime Graduates Hired Tracker
3. Processes and cleans the uploaded files
4. Identifies:
    - New students
    - Dropped apprentices
    - Transitioned students (apprentice to graduate)
    - New graduates
5. Updates placement trackers with the latest data
6. Generates downloadable Excel files

**Key Features:**

1. Handles Excel file uploads
2. Tracks student status changes week-over-week
3. Updates placement trackers with new data
4. Generates downloadable Excel files with frozen panes

### `apprentice_support.py`

#### `extract_date(file_name)`
Extracts and formats the date from the file name.

**Parameters:**

- `file_name`: Name of the uploaded file

**Returns:**

- Formatted date string (`mm-dd-yyyy`)

#### `add_new_col(df, new_col_name)`
Adds a new column to a DataFrame.

**Parameters:**
- `df`: DataFrame to modify
- `new_col_name`: Name of the new column

#### `write_to_excel_with_frozen_panes_app(df, freeze_panes="M2")`
Writes a DataFrame to an Excel file with frozen panes.

**Parameters:**

- `df`: DataFrame to export
- `freeze_panes`: Cell position to freeze panes (default: "M2")

**Returns:**

- Excel file as bytes

#### `write_to_excel_with_frozen_panes_grad(df, freeze_panes="O2")`
Writes a DataFrame to an Excel file with frozen panes.

**Parameters:**

- `df`: DataFrame to export
- `freeze_panes`: Cell position to freeze panes (default: "O2")

**Returns:**

- Excel file as bytes

## Running the Application
The application can be run independent of other applications within the Nissan scope.

1. Install required packages:
```bash
pip install streamlit pandas numpy openpyxl
```
2. Run the application:
```bash
streamlit run apprentice_dev.py
```
3. Access the application in your web browser at `http://localhost:8501`

## Error Handling
- The application includes basic error handling for:
    - File upload errors
    - Missing or invalid Excel sheets
    - Data processing errors
    - File format errors

## Output
- The application provides:
    - Updated Apprentice Placement Over Time Excel file
    - Updated Fulltime Graduates Hired Tracker Excel file
    - Both files include:
        - Latest student status updates
        - Frozen panes for better navigation

## Limitations
- Requires specific file structure and naming conventions
- Assumes consistent column names in all Excel files