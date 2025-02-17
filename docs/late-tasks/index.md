# Late Tasks Monitoring Pipeline

## Overview
The Late Tasks Monitoring Pipeline is a Python-based automation tool designed to track and report overdue tasks from Microsoft Planner. It integrates with Microsoft Graph API to fetch tasks, processes them to identify late tasks, and sends a summary email to designated recipients. The pipeline is scheduled to run automatically via GitHub Actions on Mondays and Thursdays.

## Key Features
1. **Task Fetching**: Retrieves tasks from Microsoft Planner using Microsoft Graph API.
2. **Late Task Detection**: Identifies tasks that are overdue based on their due dates and completion status.
3. **Email Reporting**: Sends a detailed HTML email report of late tasks to specified recipients.
4. **Automation**: Runs on a scheduled basis using GitHub Actions.

## Workflow
1. **Authentication**: Uses Microsoft Graph API to authenticate and retrieve an access token.
2. **Task Retrieval**: Fetches tasks incrementally from all groups and plans.
3. **Processing**: Filters and identifies late tasks.
4. **Reporting**: Generates and sends an email report with the list of late tasks.

## Requirements
- Python 3.11+
- Required Python packages:
    - requests
    - pandas
- Microsoft Graph API access with the following permissions:
    - `Group.Read.All`
    - `Planner.Read.All`
    - `Mail.Send`

## GitHub Workflow
The pipeline is automated using GitHub Actions, which runs the script on a cron schedule. See the [Usage Guide](main.md) for details on the workflow configuration.

## Error Handling
- The pipeline includes logging for:
    - Authentication failures
    - Task retrieval errors
    - Email sending failures

## Output
- An HTML email report containing:
    - The number of late tasks
    - A table of late tasks with their plan names, task names, and due dates

## Limitations
- Requires proper configuration of environment variables.
- Assumes consistent task data structure in Microsoft Planner.