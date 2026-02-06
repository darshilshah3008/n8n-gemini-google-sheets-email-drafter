# n8n Gemini Email Drafting from Google Sheets

This project is an **n8n automation workflow** for catering companies that:

- Reads customer inquiries from Google Sheets
- Uses **Google Gemini (via HTTP API)** to draft personalized response emails
- Updates the same Google Sheet row with:
  - Draft Email Subject
  - Draft Email Body
  - Draft Status

## 🧠 Use Case

Designed for catering companies that receive event inquiries via forms or spreadsheets and want to:

- Save time drafting first-response emails
- Keep all drafts inside Google Sheets
- Ensure consistent, professional communication

## 🛠 Tech Stack

- **n8n** (workflow automation)
- **Google Sheets API**
- **Google Gemini API (HTTP)**
- JavaScript (n8n Code nodes)

## 📊 Google Sheet Structure

Your Google Sheet should include columns like:

- Customer ID (used for row matching)
- Customer Name
- Email
- Event Type
- Event Date
- Guest Count
- Venue Name
- Draft Email Subject (Generated)
- Draft Email Body (Generated)
- Draft Status

⚠️ `Customer ID` must be unique and is used to update the correct row.

## 🔁 Workflow Overview

1. Read rows from Google Sheets
2. Process rows one by one
3. Skip rows already marked as "Drafted"
4. Build a clean customer context
5. Generate email draft using Gemini
6. Parse SUBJECT and BODY
7. Update the same row in Google Sheets

## 🚀 How to Use

1. Import the JSON file into n8n  
   **Settings → Import workflow**
2. Connect your Google Sheets credentials
3. Add your Gemini API key in the HTTP node
4. Update the Google Sheet ID if needed
5. Execute the workflow

## 🔐 Security Notes

- API keys are NOT included
- Google credentials must be configured locally
- Do not commit secrets to GitHub

## 📄 License

MIT License
