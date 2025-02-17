# Status Report Automation

## Overview
The Status Report Automation pipeline is a Python-based tool designed to streamline the creation and distribution of weekly project status reports. It integrates with Microsoft Graph API to create a Word document template, upload it to SharePoint, and send email notifications to team members. The pipeline is automated using GitHub Actions, ensuring timely execution every Monday.

## Key Features
1. **Template Creation**: Generates a Word document template for weekly project updates.
2. **SharePoint Integration**: Uploads the template to a designated SharePoint folder and creates an organization-wide sharing link.
3. **Email Notifications**: Sends email notifications to team members with the SharePoint link to the template.
4. **Automation**: Runs on a scheduled basis using GitHub Actions.

## Workflow
1. **Authentication**: Uses Microsoft Graph API to authenticate and retrieve an access token.
2. **Template Generation**: Creates a Word document template with placeholders for project updates.
3. **SharePoint Upload**: Uploads the template to SharePoint and generates a sharing link.
4. **Email Notification**: Sends an email to team members with the SharePoint link.

## Requirements
- Python 3.x
- Required Python packages:
    - `python-docx`
    - `requests`
    - `msal`
- Microsoft Graph API access with the following permissions:
    - `User.Read.All`
    - `Sites.Read.All`
    - `Mail.Send`

## GitHub Workflow
The pipeline is automated using GitHub Actions, which runs the script on a cron schedule. See the [Usage Guide](main.md) for details on the workflow configuration.

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
