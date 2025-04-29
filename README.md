# Autonomous AI Sales Agent

## Overview
This project implements a fully autonomous AI sales agent that handles the entire sales process from lead discovery to email outreach and follow-ups. The system runs on Google Colab, uses Google Sheets as a database, and leverages GPT models for personalized communication.

## Features

- **Automated Lead Discovery**: Scrapes potential clients from various sources based on industry keywords
- **Company Analysis**: Analyzes company websites to identify pain points and opportunities
- **Personalized Email Generation**: Creates custom cold emails and follow-ups using GPT
- **Automated Outreach**: Sends and tracks emails via Gmail API
- **Systematic Follow-ups**: Automatically follows up with non-responsive leads
- **Complete Data Tracking**: Stores all lead information and communications in Google Sheets

## Requirements

- Google account (for Colab, Sheets, and Gmail)
- OpenAI API key
- Python 3.6+ (handled by Colab)

## Setup Instructions

### 1. Copy the Notebook
Create a new Google Colab notebook and copy the entire code into it.

### 2. Configure API Keys and Settings
Update the configuration variables at the top of the notebook:

```python
# Configuration - Update these variables
OPENAI_API_KEY = "your-openai-api-key"  # Your OpenAI API key
GOOGLE_SHEET_NAME = "AI_Sales_Agent_DB"  # Name of your Google Sheet
MAX_EMAILS_PER_DAY = 15                  # Limit emails to avoid spam flags
EMAIL_WAIT_MIN = 5                       # Minimum minutes between emails
EMAIL_WAIT_MAX = 15                      # Maximum minutes between emails
FOLLOW_UP_DAYS = 5                       # Days to wait before follow-up
YOUR_NAME = "Your Name"                  # Your name for the email signature
YOUR_COMPANY = "Your Company"            # Your company name
YOUR_EMAIL = "your.email@gmail.com"      # Your Gmail address
```

### 3. Select Run Mode
Choose which mode to run by setting the MODE variable:

```python
# Choose which mode to run:
# - "quick_test": Just test the OpenAI API connection (no Google auth needed)
# - "test": Run all diagnostics (requires Google auth)
# - "main": Run the full system (requires Google auth)
MODE = "quick_test"
```

### 4. Run the Notebook
Run the notebook and follow the authentication prompts when requested.

### 5. Monitor Your Google Sheet
Once the system is running, you can monitor lead discovery and email outreach in the created Google Sheet.

## Usage Guide

### Testing the System
Start with `MODE = "quick_test"` to verify your OpenAI API key is working correctly.

Once confirmed, switch to `MODE = "test"` to run full diagnostics on all connections (Google Sheets, Gmail, and OpenAI).

### Running the Full System
Set `MODE = "main"` to run the complete sales pipeline:
1. Discovers new leads from specified industries
2. Enriches lead data
3. Sends initial cold emails
4. Follows up with non-responsive leads

### Customizing Lead Discovery
Modify the keywords list in the main() function to target specific industries:

```python
# Discover new leads from specific industries
keywords = ["saas", "fintech", "healthtech", "ecommerce", "ai"]
discover_new_leads(keywords, results_per_keyword=3)
```

### Email Rate Limiting
The system includes built-in rate limiting to avoid triggering spam filters:

```python
MAX_EMAILS_PER_DAY = 15  # Maximum emails to send per day
EMAIL_WAIT_MIN = 5       # Minimum minutes between emails
EMAIL_WAIT_MAX = 15      # Maximum minutes between emails
```

Adjust these values based on your email sending limits and requirements.

## Data Structure

The system creates a Google Sheet with two worksheets:

### Leads
Tracks all discovered companies with the following columns:
- Company
- Website
- Industry
- Contact Name
- Contact Email
- Pain Points
- Status
- Last Contact
- Notes
- Source

### Emails
Records all sent emails with the following columns:
- Timestamp
- Company
- Recipient
- Subject
- Email Body
- Email Type
- Status
- Reply Date
- Reply Content
- Notes

## Scheduling Automation

For complete automation, you can set up scheduled runs:

1. **Google Colab Pro**: Use scheduled executions feature
2. **External Service**: Use a cloud function or service like pythonanywhere to trigger your notebook
3. **Local Script**: Run a local script that accesses the Google Sheets API

## Important Notes

- Respect email sending limits and best practices to avoid being flagged as spam
- Keep your API keys secure and don't share the notebook with your keys included
- Regularly monitor the system to ensure it's functioning as expected
- Periodically review and refine your email templates based on response rates

## Troubleshooting

### Common Issues

1. **OpenAI API errors**: Verify your API key is correct and has sufficient credits
2. **Google authentication errors**: Make sure you've completed the authentication flow and granted the necessary permissions
3. **Scraping failures**: The system includes fallback to sample data if scraping fails
4. **Email sending limits**: Gmail may have additional limitations on sending volume

## Future Enhancements

- Response detection and automated reply handling
- A/B testing of different email templates
- Integration with CRM systems
- More sophisticated lead scoring
- Web interface for monitoring and control

## Disclaimer

This tool is designed for legitimate business outreach. Always comply with:
- Email spam laws (like CAN-SPAM and GDPR)
- Website terms of service
- API usage policies

Always include unsubscribe options in your emails and honor opt-out requests promptly.
