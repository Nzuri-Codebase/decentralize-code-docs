# Late Tasks Monitoring Pipeline - Usage Guide

## Running the Pipeline
The pipeline is designed to run automatically via GitHub Actions on a cron schedule. It can also be run manually for testing or debugging purposes.

## Setting up
- The first thing one needs to do is to clone the repository via the terminal command:
```bash
git clone https://github.com/Nzuri-Codebase/tasks-monitor.git
```
- The next thing one ought to do is to install the required packages via the terminal command:
```bash
pip install pandas requests
```
- Create an app registration via the azure portal using the Nzuri Strategy email.
- Copy and store securely the `client ID` and the `tenant ID` as it is used with the Microsoft Graph API in the pipeline.
- The next step is to create a `client secret` which will also be used in the Microsoft Graph API. For security purposes, it is advisable to use a client secret for not more than 1 year.
- In this particular instance though, all these have been created because this is an ongoing pipeline. An important thing that can be monitored is the expiration of the client secret.


### GitHub Workflow
The pipeline is configured to run on Mondays and Thursdays at 5:50 AM UTC. The workflow is defined in the `.github/workflows/task-monitor.yml` file:

```yaml
name: Task Monitor

on:
  schedule:
    - cron: '50 5 * * 1,4'  # Runs at 5:50 AM UTC on Mondays and Thursdays

jobs:
  monitor-tasks:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up Python
        uses: actions/setup-python@v3
        with:
          python-version: '3.11'

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install requests pandas

      - name: Run Task Monitor Script
        env:
          TENANT_ID: ${{ secrets.TENANT_ID }}
          CLIENT_ID: ${{ secrets.CLIENT_ID }}
          CLIENT_SECRET: ${{ secrets.CLIENT_SECRET }}
          SENDER: ${{ secrets.SENDER }}
          RECIPIENT1: ${{ secrets.RECIPIENT1 }}
          RECIPIENT2: ${{ secrets.RECIPIENT2 }}
          RECIPIENT3: ${{ secrets.RECIPIENT3 }}
          RECIPIENT4: ${{ secrets.RECIPIENT4 }}
        run: |
          python monitor.py
```

### Manual Execution
To run the pipeline manually:
1. Install the required Python packages:
```bash
pip install requests pandas
```
2. Set the required environment variables:
```bash
export TENANT_ID=<your-tenant-id>
export CLIENT_ID=<your-client-id>
export CLIENT_SECRET=<your-client-secret>
export SENDER=<sender-email>
export RECIPIENT1=<recipient1-email>
export RECIPIENT2=<recipient2-email>
export RECIPIENT3=<recipient3-email>
export RECIPIENT4=<recipient4-email>
```
3. Run the script:
```bash
python monitor.py
```

## Code Overview
The pipeline consists of the following key functions:

### `get_access_token`
- Retrieves an access token from Microsoft Graph API using client credentials.

### `get_tasks`
- Fetches tasks incrementally from all groups and plans using Microsoft Graph API.

### `fetch_tasks_for_group`
- Fetches tasks for a specific group.

### `fetch_tasks_for_plan`
- Fetches tasks for a specific plan.

### `process_tasks`
- Processes tasks to identify late ones based on due dates and completion status.

### `send_email`
- Sends an HTML email report with the list of late tasks.

### `main`
- The main function that orchestrates the pipeline.

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
