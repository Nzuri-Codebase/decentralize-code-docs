# Documentation Overview
This is the documentation for automated Nzuri services.

## Decentralize Nzuri Web Application
* A comprehensive web application built with Streamlit, Flask, and InfluxDB, designed to process and analyze data for Honda and Nissan accounts.
* Key features include:
    - **Authentication**: Microsoft Azure AD integration
    - **User Tracking**: Session tracking with InfluxDB
    - **Navigation**: Access to Honda and Nissan applications
    - **Deployment**: Supports Docker and Azure deployments

### Honda Applications
- **Ask Dave**: Processes monthly conversion data from Excel files
- **High Deliverability**: Analyzes email campaign delivery metrics
- **Remedy Spikes**: Visualizes remedy data trends using moving averages
- **Informed Delivery**: Tracks email campaign performance metrics

### Nissan Applications
- **Apprentice Placement**: Tracks apprentice and graduate placement data
- **Nissan ROI**: Calculates and analyzes ROI metrics for apprentices and graduates

## Automation Pipelines

### Late Tasks Monitoring
* A Python-based pipeline that:
    - Tracks overdue tasks from Microsoft Planner
    - Sends automated email reports
    - Runs on a schedule via GitHub Actions (Mondays and Thursdays)

### Status Report Automation
* A Python tool that:
    - Creates weekly project status report templates
    - Uploads documents to SharePoint
    - Sends email notifications to team members
    - Runs on a schedule via GitHub Actions (Mondays)

## Key Technologies
- **Frontend**: Streamlit
- **Backend**: Flask API
- **Database**: InfluxDB
- **Deployment**: Docker, Azure
- **Automation**: GitHub Actions
- **APIs**: Microsoft Graph API

## Documentation Structure
* Each section includes:
    1. Overview
    2. Requirements
    3. Setup instructions
    4. Usage guides
    5. Troubleshooting tips
    6. Error handling details
    7. Limitations

## Getting Started
1. Clone the associated repository.
2. Install dependencies
3. Configure environment variables
4. Run the desired application or pipeline