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
- To integrate the pipeline with the Microsoft Graph API, start by registering an application through the Azure portal using the Nzuri Strategy email. This registration process will generate a unique `client ID` and `tenant ID`, which are essential for authenticating API requests. Ensure these credentials are stored securely to prevent unauthorized access.
- Next, create a `client secret` for the registered application. This secret is used in conjunction with the client ID and tenant ID to authenticate API requests. For enhanced security, it is recommended to set a limited lifespan for the client secret, ideally not exceeding 1 year. This ensures that even if the secret is compromised, its impact is minimized due to its short validity period.
- Since this pipeline is designed for ongoing use, it is crucial to monitor the expiration date of the client secret to ensure uninterrupted operation. This can be achieved by setting reminders or implementing automated checks to alert the maintenance team when the secret is nearing expiration, allowing for timely renewal or rotation.


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
- Install the required Python packages:
```bash
pip install requests pandas
```
- Set the required environment variables:
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
- Run the script:
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
