# n8n Automation: AI-Powered Email Drafting from Google Sheets (Catering Use Case)

## Overview

This repository contains a **production-ready n8n workflow** that automates the creation of **personalized first-response customer emails** for a catering company using **Google Sheets** and **Google Gemini (LLM)**.

The workflow reads customer inquiry data from a Google Sheet, generates a professional email draft using AI, and updates the **same spreadsheet row** with the drafted subject, body, and status.

The project demonstrates a real-world application of **workflow automation, data processing, and AI integration**.

---

## Business Problem

Catering companies typically receive a high volume of event inquiries via forms or spreadsheets. Writing individualized responses manually is:

- Time-consuming
- Inconsistent in tone and structure
- Difficult to track at scale

---

## Solution

This automation solves the problem by:

- Automatically drafting personalized email responses
- Ensuring consistent professional communication
- Saving time for sales and operations teams
- Keeping all drafts stored and tracked inside Google Sheets
- Preventing duplicate processing using a draft status flag

---

## Key Features

- Reads inquiries directly from Google Sheets  
- Processes rows **one at a time** (safe, predictable execution)  
- Skips rows already marked as *Drafted*  
- Builds a structured prompt from available customer & event data  
- Uses **Google Gemini via HTTP API** to generate email drafts  
- Extracts and stores:
  - Email subject
  - Email body
- Updates the **same spreadsheet row** using a unique identifier  

---

## Technology Stack

- **n8n** – Workflow automation
- **Google Sheets API** – Data source and updates
- **Google Gemini API (HTTP)** – AI text generation
- **JavaScript** – Parsing and transformation in n8n Code nodes

---

## Google Sheet Requirements

The workflow expects a Google Sheet with a **unique identifier column**:

Customer ID


This column is used to ensure the correct row is updated.

### Recommended Column Structure

| Column Name | Description |
|------------|-------------|
| Customer ID | Unique identifier (required for updates) |
| Customer Name | Used for personalization |
| Email | Customer email address |
| Phone | Contact number |
| Company/Organization | Company name |
| Event Type | Event context |
| Event Date | Event context |
| Event Start Time | Event context |
| Event End Time | Event context |
| Guest Count | Event size |
| Venue Name | Event location |
| Venue Address | Event location |
| Service Style | Buffet / plated / stations |
| Cuisine Preference | Food preference |
| Dietary/Allergy Notes | Dietary constraints |
| Menu Package Interest | Menu selection |
| Beverage Needs | Beverage requirements |
| Estimated Budget (USD) | Budget context |
| Delivery/Setup | Service details |
| Lead Source | Marketing source |
| Preferred Contact Method | Communication preference |
| Best Time to Reach | Availability |
| Notes | Internal notes |
| Draft Email Subject (Generated) | AI-generated subject |
| Draft Email Body (Generated) | AI-generated email body |
| Draft Status | Drafted / Not Drafted |
| Workflow Notes | Automation metadata |

⚠️ **Customer ID must be unique for every row.**

---

## Workflow Logic (High Level)

1. Read rows from Google Sheets  
2. Loop through rows sequentially  
3. Skip rows where `Draft Status = Drafted`  
4. Build a clean customer & event context  
5. Send prompt to Google Gemini (HTTP API)  
6. Parse the AI response into SUBJECT and BODY  
7. Update the same Google Sheet row using `Customer ID`  

---

## How to Use the Workflow

### 1️⃣ Import the Workflow into n8n

1. Open your n8n instance  
2. Click **Import workflow**  
3. Upload `workflow.json` from this repository  

---

### 2️⃣ Configure Google Sheets Access

1. Create or select a **Google Sheets credential** in n8n  
2. Attach it to all Google Sheets nodes  
3. Replace the placeholder value in the workflow:

REPLACE_WITH_YOUR_SHEET_ID


with your actual Google Sheet ID.

---

### 3️⃣ Add Your Gemini API Key (IMPORTANT)

This repository does **NOT** contain any API keys.

You must provide your Gemini API key via an **environment variable**:

```bash
GEMINI_API_KEY=your_actual_api_key_here

Example (Docker)
docker run -e GEMINI_API_KEY=your_key_here n8nio/n8n

Example (n8n Cloud / Hosted)
Add the environment variable:
GEMINI_API_KEY