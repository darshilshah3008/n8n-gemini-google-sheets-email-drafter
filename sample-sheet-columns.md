# Sample Google Sheet Structure

This workflow expects a Google Sheet with the following columns.
You may add additional columns, but these are the recommended minimum.

| Column Name | Description |
|------------|-------------|
| Customer ID | Unique identifier for each customer (required) |
| Customer Name | Full name of the customer |
| Email | Customer email address |
| Event Type | Type of event (e.g., Corporate Lunch, Wedding) |
| Event Date | Date of the event |
| Guest Count | Estimated number of guests |
| Draft Email Subject (Generated) | AI-generated email subject |
| Draft Email Body (Generated) | AI-generated email body |
| Draft Status | Status flag (Drafted / Not Generated) |

## Notes
- **Customer ID** is used to match and update the correct row.
- Generated columns are automatically filled by the n8n workflow.
- Draft Status helps prevent duplicate email generation.
