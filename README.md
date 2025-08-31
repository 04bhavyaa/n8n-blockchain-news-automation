# n8n Blockchain News Automation Workflow

## Overview

This n8n workflow automates the process of finding, rewriting, and publishing blockchain news content to LinkedIn and X (formerly Twitter). It leverages RSS feeds for content sourcing, Google Sheets for data management and human approval, and Google's Gemini AI for content rewriting.

The core idea is to create a semi-automated content pipeline that ensures quality control and brand voice consistency while significantly reducing manual effort.

## How It Works

1. **RSS Feed Reader**: Reads the latest news from a blockchain news RSS feed (e.g., https://crypto.news/feed/).
2. **Google Sheets Integration**: Saves raw news data to a Google Sheet, acting as a central database and staging area.
3. **AI-Powered Rewriting**: Uses Google Gemini to rewrite news headlines and content into engaging, platform-specific posts for LinkedIn and X.
4. **Approval System**: Saves generated posts to separate Google Sheets. You receive an email with a link to these sheets, where you can review and approve each post by marking "yes" in the "approve" column.
5. **Automated Posting**: Publishes approved posts to LinkedIn and X, and updates the original Google Sheet to "completed" for tracking.

## Features

- **RSS Feed Integration**: Automatically fetches the latest news from a specified RSS feed.
- **Google Sheets as a Database**:
  - Saves raw news data to a primary Google Sheet for record-keeping.
  - Generates AI-rewritten posts and saves them to separate Google Sheets for LinkedIn and X, awaiting approval.
- **AI Content Rewriting**: Utilizes the Google Gemini Chat Model to rewrite articles into engaging, platform-specific posts for social media.
- **Human-in-the-Loop Approval**: Sends an email notification with a link to the Google Sheets. Posts are only published once a user marks them as "yes" in the approve column.
- **Automated Publishing**: Publishes approved posts to LinkedIn and X via their respective APIs.
- **Status Tracking**: Updates the status of each news item in the Google Sheets to "completed" after a successful post, providing a clear overview of the content pipeline.

## Workflow Breakdown

The workflow is designed to be executed manually or on a schedule.

**Steps:**

1. **RSS Read**: Reads the latest articles from https://crypto.news/feed/.
2. **Limit**: Limits the number of items to process (e.g., 10), preventing the sheet from being overwhelmed.
3. **Google Sheets**: Appends the raw news data to a Google Sheet named "Blockchain-News."
4. **Gmail**: Sends an email to notify the user that new news items are ready for review and tagging for social media.
5. **Google Sheets1**: Filters the "Blockchain-News" sheet for items tagged for LinkedIn (linkedin: yes) or X (twitter: yes) and have a status of "to post."
6. **Filter and Filter1**: Splits the workflow path for LinkedIn and X processing.
7. **AI Agent and AI Agent1**: Uses Google Gemini to rewrite the content for LinkedIn and X, respectively.
8. **Google Sheets2 and Google Sheets9**: Saves the AI-generated posts to separate "to post" sheets (Linkedin-Post and X-Posts).
9. **Gmail1 and Gmail2**: Sends emails to notify the user that the posts are ready for final approval.
10. **Google Sheets3 and Google Sheets8**: Reads approved posts (approve: yes) from the "to post" sheets.
11. **Code and Code1**: Prepares the data payload for the LinkedIn and X APIs.
12. **HTTP Request (LinkedIn) and X (Twitter)**: Publishes the content to the respective social media platforms.
13. **Merge and Merge1**: Combines the output from the social media nodes with the original data.
14. **Google Sheets4 and Google Sheets6**: Updates the "to post" sheets, marking the status as "completed."
15. **Merge2 and Google Sheets5**: Updates the master "Blockchain-News" sheet, marking the original news item as "completed."

## Prerequisites

- An n8n instance (self-hosted or cloud)
- API credentials for:
  - Google Sheets (OAuth2)
  - Google Gemini (API Key)
  - LinkedIn (OAuth2)
  - X (Twitter) (OAuth2)
  - Gmail (OAuth2)

## Setup and Configuration

1. Create a new workflow in n8n and import the provided `workflow.json`.
2. The `workflow.json` file has all sensitive information (emails, Google Sheet IDs, credential IDs, LinkedIn URN, etc.) replaced with placeholders for safe public sharing.
3. Before running the workflow, replace all placeholder values with your actual credentials and resource IDs:

- `<YOUR_EMAIL>`: Your email address for notifications and approvals
- `<YOUR_BLOCKCHAIN_NEWS_SHEET_ID>`, `<YOUR_LINKEDIN_POST_SHEET_ID>`, `<YOUR_X_POST_SHEET_ID>`: Your Google Sheet IDs
- `<YOUR_GOOGLE_SHEETS_CREDENTIAL_ID>`, `<YOUR_GMAIL_CREDENTIAL_ID>`, `<YOUR_X_CREDENTIAL_ID>`, `<YOUR_LINKEDIN_CREDENTIAL_ID>`, `<YOUR_BEARER_AUTH_CREDENTIAL_ID>`, `<YOUR_GOOGLE_GEMINI_API_CREDENTIAL_ID>`: Your n8n credential IDs
- `<YOUR_LINKEDIN_PERSON_URN>`: Your LinkedIn person URN

4. Ensure the sheet names and column headers in your spreadsheets match the configuration in the workflow.
5. Customize the AI Agent and AI Agent1 prompts to fine-tune the tone and style of the social media posts.
6. Activate the workflow and execute it to begin the process.

## File Structure

- `workflow.json`: The exported n8n workflow definition.
- `README.md`: Project documentation and usage instructions.

## Gallery
<img width="553" height="309" alt="Screenshot 2025-08-31 110527" src="https://github.com/user-attachments/assets/15edf191-0299-4938-94a4-57ba0cffbeda" />
<img width="1920" height="849" alt="Screenshot 2025-06-11 162730" src="https://github.com/user-attachments/assets/525adf92-7fe3-4e19-bf63-0432aae21d84" />


## License

This project is provided for educational and personal use. Please check the terms of service for any APIs or news sources you use.

## Support

For help with n8n workflows, visit the [n8n documentation](https://docs.n8n.io/) or the [community forum](https://community.n8n.io/).
