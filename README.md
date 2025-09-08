# LeadGen AI Flow

AI-powered lead gen workflow built on **n8n**. It accepts GET requests on a webhook, filters seed companies by query params, generates industry-tailored insights, asks an LLM to draft a consultative outreach email, appends results to Google Sheets, and returns JSON.

## What it does
1. **Webhook (GET)** at path `leadgen`.  
2. **Seed Companies**: sample data for 3 companies.  
3. **Filter by Query Params (Python)**: supports `industry`, `location`, `sizeMin`, `sizeMax`.  
4. **Mock Insights (Python)**: adds 2–3 industry/location/size-based bullets.  
5. **AI Agent**: builds an outreach email from details + insights (JSON-only output).  
6. **Google Sheets Append**: writes Company/Subject/Body.  
7. **Respond JSON**: returns the parsed fields.

## Endpoints
- **Production**: `https://<your-n8n-host>/webhook/leadgen`  
- **Test mode**: `https://<your-n8n-host>/webhook-test/leadgen` (only while workflow is executing in Test)

### Examples
- All items:  
  `.../webhook/leadgen`
- Software in India (min 100 employees):  
  `.../webhook/leadgen?industry=software&location=IN&sizeMin=100`
- Manufacturing, <=100 employees in Pune:  
  `.../webhook/leadgen?industry=manufact&location=pune&sizeMax=100`
- Logistics in Hyderabad:  
  `.../webhook/leadgen?industry=logistic&location=hyderabad`

## Response shape
The workflow returns JSON per matched company, including the AI-generated content:
```json
{
  "company": "string",
  "subject": "string",
  "body": "string",
  "tone": "string",
  "wordCount": 108
}
