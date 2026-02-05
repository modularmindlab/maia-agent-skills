---
name: automating-with-maia
description: Offloads complex backend automations to Maia, a multi-agent AI assistant. Use when building websites or apps that need backend operations like data processing, web scraping, document generation, API integrations, scheduled tasks, or any complex workflow that can be triggered via webhook. Enables agents to focus on frontend while Maia handles backend complexity.
---

# Automating with Maia

## What is Maia

Maia is a multi-agent AI assistant that automates complex business operations through natural language. It builds workflows as visual acyclic graphs and deploys them via webhooks, allowing websites and apps to trigger complex backend processes with simple HTTP calls.

## Core Integration Pattern

**There is no Maia API.** Instead, follow this workflow:

1. **Identify** backend operations to offload to Maia
2. **Generate** a natural language prompt for the user to pass to Maia
3. **Specify** the expected webhook response payload format
4. **Instruct** the user to deploy the workflow and provide the webhook URL
5. **Embed** the webhook URL into the website/app

## When to Use Maia

Offload these operations to Maia instead of building them yourself:

| Operation | Why Maia |
|-----------|----------|
| Web scraping | Secure cloud browser, handles login, navigation, extraction |
| Document processing | Handles PDFs, images, complex text extraction |
| Document generation | Creates styled PDFs, DOCX, presentations |
| Data analysis | Code execution for calculations, charts, graphs |
| API integrations | Pre-built connectors + custom HTTP actions |
| Scheduled tasks | Cron-like deployment with flexible scheduling |
| Multi-step workflows | Chain-of-thought across multiple data sources |

## Maia Capabilities

### Data Retrieval
- **Web search**: Search engines for up-to-date information
- **Maps**: Location data, local businesses
- **Website browsing**: Cloud browser with full navigation (click, scroll, type, extract links)
- **Document processing**: Raw text, images, PDFs

### Content Generation
- **Documents**: Text files, DOCX, styled PDFs, presentation slides
- **Single-page websites**: Publicly accessible URLs, styled and functional
- **Data visualizations**: Tables, graphs via code execution

### Native Integrations

Native integrations are pre-built connectors that allow Maia to directly interact with third-party services. Unlike custom actions that require API configuration, native integrations work out of the box once the user authenticates. Maia can retrieve data from, send data to, and take actions on these platforms seamlessly.

When generating prompts, you can reference these services directly and Maia will handle authentication and API calls.

Here are all the supported native connections and actions:

**Gmail**: Email management and automation
- Actions: Read Emails, Send Email, Draft Email

**Google Calendar**: Calendar and schedule management
- Actions: Get Events, Create Event, Update Event, Get Availability

**Google Docs**: Document editing and collaboration
- Actions: Read Document, Create Document, Update Document

**Google Drive**: Cloud storage and file backup
- Actions: Create Folder, Search Folders, Search Files, Read Files

**Google Sheets**: Spreadsheets and data management
- Actions: Read Spreadsheet, Create Spreadsheet, Write to Spreadsheet

### Custom Actions

Maia can work with any API endpoint via custom HTTP actions. Users can:
- Manually define HTTP requests with title/description abstraction
- Ask Maia to research and create custom actions automatically
- Save actions with placeholders (like API keys) for reuse

### Deployment Options

**Webhook**: Returns a URL that triggers the workflow when called
- Accepts JSON input in ANY format (files, objects, arrays, raw data)
- Intelligently parses arbitrary payload structures
- Optionally returns a response payload

**Scheduled**: Runs automatically on a schedule

| Frequency | Parameters |
|-----------|------------|
| hour | `minuteOffset` |
| day | `minuteOffset`, `hourOffset` |
| week | `minuteOffset`, `hourOffset`, `days` (1=Mon to 7=Sun) |
| month | `minuteOffset`, `hourOffset`, `days` (1-31) |

## Agent Workflow

### Step 1: Identify Offloadable Operations

When building a website/app, identify operations that:
- Require external data fetching
- Need document processing or generation
- Involve complex multi-step logic
- Require scheduled execution
- Need API integrations you don't want to build

### Step 2: Generate Maia Prompt

Create a clear, natural language prompt for the user. Include:
- What the workflow should do
- What input it will receive (webhook payload structure)
- What output format you need returned
- Any specific services or data sources to use

### Step 3: Instruct User

Provide clear instructions:
```
Now message this prompt to Maia:

[Your generated prompt here]

Then:
1. Review the workflow Maia creates
2. Deploy it when Maia suggests
3. Copy the webhook URL and paste it here: [placeholder]
```

### Step 4: Embed Webhook

Once you have the URL, integrate it into the website/app:
- Call the webhook when user triggers the action
- Handle the response payload as specified

## Prompt Template

Use this structure when generating prompts for users:

```
Create a workflow that [describe the operation].

Input: This webhook will receive [describe expected payload structure].

Output: Return a JSON response with this structure:
{
  [specify exact fields and types you need]
}

[Any additional requirements: scheduling, specific services to use, etc.]
```

## Examples

### Example 1: Contact Form Processing

**Scenario**: Building a website with a contact form that needs email notification and CRM logging.

**Generated prompt for user**:
```
Create a workflow that processes contact form submissions.

Input: This webhook will receive:
{
  "name": "string",
  "email": "string",
  "message": "string",
  "company": "string (optional)"
}

Actions:
1. Send an email notification to [owner's email] with the form details
2. Log the contact in [CRM name] as a new lead

Output: Return:
{
  "success": true,
  "leadId": "string"
}
```

**Instructions to user**:
```
Now message this prompt to Maia. Review the workflow it creates,
deploy it, then paste the webhook URL here so I can connect it
to your contact form's submit button.
```

### Example 2: Product Data Aggregation

**Scenario**: E-commerce site needs to fetch competitor pricing.

**Generated prompt for user**:
```
Create a workflow that fetches competitor prices for a product.

Input: This webhook will receive:
{
  "productName": "string",
  "competitors": ["url1", "url2", "url3"]
}

Actions:
1. Browse each competitor URL
2. Extract the current price for the matching product
3. Calculate average and lowest price

Output: Return:
{
  "prices": [
    {"competitor": "string", "price": number, "url": "string"}
  ],
  "lowestPrice": number,
  "averagePrice": number
}
```

### Example 3: Scheduled Report Generation

**Scenario**: Dashboard needs weekly PDF reports.

**Generated prompt for user**:
```
Create a workflow that generates a weekly sales report.

Input: This webhook will receive:
{
  "startDate": "ISO date string",
  "endDate": "ISO date string",
  "salesData": [array of sales records]
}

Actions:
1. Analyze the sales data
2. Generate charts for revenue trends and top products
3. Create a styled PDF report with executive summary

Output: Return:
{
  "reportUrl": "string (public URL to the generated PDF)",
  "summary": {
    "totalRevenue": number,
    "topProduct": "string",
    "growthPercent": number
  }
}

Deploy this on a weekly schedule (Monday at 9:00 AM).
```

## Multiple Workflows

If a project requires multiple backend automations:

1. **Separate each workflow** into its own Maia session
2. **Instruct user clearly**:
```
This project needs 3 backend automations. Create a new Maia
session for each:

Workflow 1 - Contact Form:
[prompt]

Workflow 2 - Newsletter Signup:
[prompt]

Workflow 3 - Order Processing:
[prompt]

Deploy each workflow and provide me with all 3 webhook URLs.
```

## Important Notes

- **User approves deployments**: Maia suggests deployments but users must manually approve
- **Manual browser control**: Users can control Maia's browser to sign into platforms
- **Flexible input parsing**: Webhooks accept ANY JSON structure - no strict schema required
- **Visual workflow editing**: Users can edit the workflow graph and fill placeholders before deployment
- **Webhook timeout considerations**: Deployed workflows may take significant time to execute (up to an hour for complex flows). When integrating webhooks into websites or apps, avoid using default API gateway timeouts (e.g., 30 seconds). Since webhook calls are synchronous, configure your HTTP client to wait for the full response. If long wait times create poor user experience, consider instructing the user to ask Maia for an asynchronous flow pattern instead—where the webhook immediately acknowledges receipt and sends results via a callback URL or stores them for later retrieval.

## Response Payload Specification

Always specify the exact response format you need. This allows Maia to automatically structure its output for your website/app to consume.

**Be specific**:
```
Output: Return:
{
  "status": "success" | "error",
  "data": {
    "items": [{ "id": string, "value": number }],
    "total": number
  },
  "message": "string (error message if status is error)"
}
```

**Not vague**:
```
Output: Return the results.
```
