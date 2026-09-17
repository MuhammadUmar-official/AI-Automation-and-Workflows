# AI Invoice Processing Automation

An end-to-end **AI-powered invoice processing automation** built with **n8n**.

This workflow receives invoice emails, extracts PDF attachments, uses AI to extract structured invoice information, validates the extracted data, checks for duplicate invoices, applies business rules such as high-value invoice detection, stores results in Google Sheets, and sends finance notifications.

## Workflow Overview

![AI Invoice Processing Automation](workflow.png)

## What This Workflow Does

1. Monitors Gmail for new invoice emails.
2. Filters emails to identify messages containing attachments.
3. Extracts PDF attachments from the incoming email.
4. Extracts text/content from the invoice PDF.
5. Uses an AI model to extract invoice fields.
6. Parses the AI response into structured data.
7. Validates the extracted invoice information.
8. Searches Google Sheets for existing invoices.
9. Checks whether the invoice is a duplicate.
10. Routes duplicate invoices for finance notification.
11. Checks whether the invoice has a high value.
12. Logs valid invoices in Google Sheets.
13. Sends finance notifications based on the invoice status.
14. Logs invoices that require manual review.

## Workflow Architecture

```text
New Invoice Email
       ↓
Gmail Trigger
       ↓
Filter: Has Attachments
       ↓
Extract PDF Attachments
       ↓
Extract PDF Text
       ↓
AI: Extract Invoice Fields
       ↓
Parse AI JSON Response
       ↓
Validate Invoice Data
       ↓
Search Google Sheets for Duplicates
       ↓
Check Duplicate
      /     YES  NO
     ↓    ↓
Log      Check
Duplicate High-Value
     ↓      ↓
Notify   ┌──┴──┐
Finance  │     │
       High   Normal
        ↓       ↓
   Notify     Store Invoice
   Finance    in Google Sheets
                 ↓
          Send Confirmation
```

Invalid or incomplete invoices are routed to a separate review path and logged for finance follow-up.

## Tools & Technologies

| Tool / Technology | Purpose |
|---|---|
| **n8n** | Workflow orchestration and automation |
| **Gmail** | Receives invoice emails and sends finance notifications |
| **AI / OpenAI Model** | Extracts structured information from invoice content |
| **PDF Extraction** | Extracts text from invoice PDF attachments |
| **Google Sheets** | Searches, stores, and updates invoice records |
| **Code / Edit Fields Nodes** | Parses and transforms invoice data |
| **Conditional Logic** | Handles duplicate, validation, and value-based routing |

## AI Invoice Extraction

The AI processing step is used to convert unstructured invoice content into structured information.

Typical invoice fields can include:

```text
Invoice Number
Invoice Date
Vendor Name
Vendor Email
Invoice Amount
Currency
Due Date
Tax
Total Amount
Payment Information
```

The extracted result is parsed into structured data before the workflow continues.

## Invoice Validation

Before an invoice is stored as a valid record, the workflow checks the extracted information.

This helps identify invoices with missing or invalid data and routes them toward a manual-review path instead of blindly processing them.

## Duplicate Invoice Detection

The workflow searches Google Sheets for existing invoice records before storing a new invoice.

```text
Invoice Data
    ↓
Search Existing Records
    ↓
Duplicate?
   /    YES    NO
  ↓      ↓
Log    Continue
Duplicate
  ↓
Notify Finance
```

This helps reduce duplicate invoice entries and gives the finance team visibility into possible repeated submissions.

## High-Value Invoice Detection

The workflow also contains a business-rule check for high-value invoices.

```text
Valid Invoice
     ↓
High-Value Check
    /   YES  NO
   ↓    ↓
Notify  Continue
Finance Processing
```

High-value invoices can therefore receive additional finance-team attention.

## Finance Notifications

Gmail is used to notify the finance team about important invoice events, including:

- Duplicate invoices
- High-value invoices
- Validation failures
- Other invoices requiring manual review
- Processing confirmations

## Google Sheets Records

Google Sheets acts as a centralized invoice record.

The stored data can include fields such as:

```text
Invoice Number
Invoice Date
Vendor
Amount
Currency
Due Date
Validation Status
Duplicate Status
Processing Status
```

The exact fields depend on the configuration of the workflow.

## Error & Manual Review Path

Invoices that fail validation or require additional review are separated from the normal processing path.

```text
Invoice Validation
       ↓
Invalid / Needs Review
       ↓
Log Review Record
       ↓
Notify Finance
```

This provides a safer workflow for invoices that cannot be confidently processed automatically.

## Business Value

This automation can help businesses:

- Reduce manual invoice data entry
- Speed up invoice processing
- Convert PDF invoices into structured records
- Detect duplicate invoices
- Flag high-value invoices
- Centralize invoice records
- Reduce repetitive finance-team tasks
- Improve visibility into invoice processing
- Route exceptions for human review

## Example Use Case

A company receives an invoice as a PDF attachment by email.

Instead of manually opening the PDF, reading the invoice, entering the details into a spreadsheet, checking for duplicates, and notifying finance, the automation can perform these steps automatically:

```text
Invoice Email
     ↓
PDF Attachment
     ↓
AI Data Extraction
     ↓
Validation
     ↓
Duplicate Check
     ↓
Business Rules
     ↓
Google Sheets
     ↓
Finance Notification
```

## Security & Credentials

This workflow may require credentials for:

- Gmail
- Google Sheets
- AI provider

**Never commit API keys, passwords, OAuth tokens, or other secrets to GitHub.**

For client delivery, credentials should be configured in the client's own n8n environment.

## Workflow Delivery

The n8n workflow can be exported as a **JSON file** and imported into another n8n environment.

Recommended GitHub structure:

```text
AI-Invoice-Processing-Automation/
├── AI_Invoice_Processing_Automation.json
├── README.md
└── workflow.png
```

Keeping the JSON, README, and screenshot together makes each workflow easy to understand and reuse.

## Project Status

**Status:** Completed — Portfolio Project

This project demonstrates practical experience with:

`AI Automation` `n8n` `Gmail` `PDF Processing` `AI Data Extraction` `Google Sheets` `Duplicate Detection` `Business Rules` `Finance Automation`

## Author

**Muhammad Umar**

**Focus:** Data Science | AI/ML | AI Automation & Agents
