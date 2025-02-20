# Status Report Automation - Usage Guide

## Running the Pipeline
The pipeline is designed to run automatically via GitHub Actions on a cron schedule. It can also be run manually for testing or debugging purposes.

## Setting up
- The first thing one needs to do is to clone the repository via the terminal command:
```bash
git clone https://github.com/Nzuri-Codebase/nzuri-status-updates.git
```
- The next thing one ought to do is to install the required packages via the terminal command:
```bash
pip install -r requirements.txt
```
- To integrate the pipeline with the Microsoft Graph API, start by registering an application through the Azure portal using the Nzuri Strategy email. This registration process will generate a unique `client ID` and `tenant ID`, which are essential for authenticating API requests. Ensure these credentials are stored securely to prevent unauthorized access.
- Next, create a `client secret` for the registered application. This secret is used in conjunction with the client ID and tenant ID to authenticate API requests. For enhanced security, it is recommended to set a limited lifespan for the client secret, ideally not exceeding 1 year. This ensures that even if the secret is compromised, its impact is minimized due to its short validity period.
- Since this pipeline is designed for ongoing use, it is crucial to monitor the expiration date of the client secret to ensure uninterrupted operation. This can be achieved by setting reminders or implementing automated checks to alert the maintenance team when the secret is nearing expiration, allowing for timely renewal or rotation.

### GitHub Workflow
The pipeline is configured to run on Mondays at 7:50 AM UTC for template creation and at 2:50 PM UTC for sending compiled document notifications. The workflows are defined in the `.github/workflows/` directory:

#### Template Creation Workflow (`rollout_template.yml`):
```yaml
name: Rollout Template

on:
  schedule:
    - cron: '50 7 * * 1'  # Runs at 7:50 AM UTC on Mondays
  workflow_dispatch:

jobs:
  run-template-script:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v2

      - name: Set up Python 3.x
        uses: actions/setup-python@v2
        with:
          python-version: 3.x

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt

      - name: Run create_template.py script
        env:
          CLIENT_ID: ${{ secrets.CLIENT_ID }}
          CLIENT_SECRET: ${{ secrets.CLIENT_SECRET }}
          M1: ${{ secrets.M1 }}
          M2: ${{ secrets.M2 }}
          M3: ${{ secrets.M3 }}
          M4: ${{ secrets.M4 }}
          M5: ${{ secrets.M5 }}
          M6: ${{ secrets.M6 }}
          M7: ${{ secrets.M7 }}
          M8: ${{ secrets.M8 }}
          M9: ${{ secrets.M9 }}
          SENDER_ID: ${{ secrets.SENDER_ID }}
          TENANT_ID: ${{ secrets.TENANT_ID }}
        run: |
          python create_template.py
```

#### Notification Workflow (`send_compiled_doc.yml`):
```yaml
name: Send Compiled document

on:
  schedule:
    - cron: '50 14 * * 1'  # Runs at 2:50 PM UTC on Mondays
  workflow_dispatch:

jobs:
  run-template-script:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v2

      - name: Set up Python 3.x
        uses: actions/setup-python@v2
        with:
          python-version: 3.x

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt

      - name: Run send_compiled_doc.py script
        env:
          CLIENT_ID: ${{ secrets.CLIENT_ID }}
          CLIENT_SECRET: ${{ secrets.CLIENT_SECRET }}
          M1: ${{ secrets.M1 }}
          M2: ${{ secrets.M2 }}
          M3: ${{ secrets.M3 }}
          M4: ${{ secrets.M4 }}
          M5: ${{ secrets.M5 }}
          M6: ${{ secrets.M6 }}
          M7: ${{ secrets.M7 }}
          M8: ${{ secrets.M8 }}
          M9: ${{ secrets.M9 }}
          SENDER_ID: ${{ secrets.SENDER_ID }}
          TENANT_ID: ${{ secrets.TENANT_ID }}
        run: |
          python send_compiled_doc.py
```

### Manual Execution
- Install the required Python packages:
```bash
pip install python-docx requests msal python-dotenv
```
- Set the required environment variables:
```bash
export CLIENT_ID=<your-client-id>
export CLIENT_SECRET=<your-client-secret>
export TENANT_ID=<your-tenant-id>
export SENDER_ID=<sender-email>
export M1=<member1-email>
export M2=<member2-email>
export M3=<member3-email>
export M4=<member4-email>
export M5=<member5-email>
export M6=<member6-email>
export M7=<member7-email>
export M8=<member8-email>
export M9=<member9-email>
```
- Run the script for template creation:
```bash
python create_template.py
```
- Run the script for sending notifications:
```bash
python send_compiled_doc.py
```

## Code Overview
The pipeline consists of the following key functions:

### `get_team_members`
- Retrieves team members' details from Microsoft Graph API.

### `create_document_template`
- Generates a Word document template with placeholders for project updates.

### `upload_to_sharepoint`
- Uploads the template to SharePoint and generates a sharing link.

### `send_email_notification`
- Sends an email notification with the SharePoint link to team members.

### `clean_document`
- Modifies the document to remove sections with placeholder text.

### `send_email_with_link`
- Sends an email with the SharePoint document link using Microsoft Graph API.

## Error Handling
- The pipeline includes logging for:
    - Authentication failures
    - Template creation errors
    - SharePoint upload errors
    - Email sending failures

## Output
- A Word document template uploaded to SharePoint.
- An email notification with the SharePoint link sent to team members.

## Limitations
- Requires proper configuration of environment variables.
- Assumes consistent SharePoint folder structure and permissions.
