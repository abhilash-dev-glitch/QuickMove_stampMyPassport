# QuickMove AI Relocation Automation

> AI-powered relocation request automation built using **n8n**, **Google Forms**, **Google Sheets**, **Ollama (Local LLM)**, and **Gmail**.

---

# Overview

QuickMove is a relocation services company that manages customer requests for:

* Apartment Search
* Packers & Movers
* Utility Setup
* Address Change Assistance
* Customer Support

Currently, operations are handled manually using Google Forms, Google Sheets, WhatsApp, and Email.

This project automates the customer intake and request analysis process using AI, reducing manual effort and enabling faster operational decision-making.

---

# Problem Statement

The existing workflow requires Operations Executives to manually:

* Review each customer request
* Identify missing information
* Assess urgency
* Assign priorities
* Update tracking sheets
* Notify customers
* Coordinate with the operations team

This manual process is time-consuming, error-prone, and difficult to scale.

---

# Solution

The solution leverages **n8n** and **Ollama** to automatically analyze relocation requests, assign priorities, update operational records, and send notifications.

The workflow runs automatically whenever a customer submits a Google Form.

---

# Workflow Architecture

```text
Customer
     │
     ▼
Google Form
     │
     ▼
Google Sheets (Form Responses)
     │
     ▼
Google Sheets Trigger
     │
     ▼
Set Node
     │
     ▼
HTTP Request
(Ollama - Local LLM)
     │
     ▼
Code Node
(Parse + Merge AI Response)
     │
     ▼
IF Node
(Priority Check)
     │
     ▼
Google Sheets Update
     │
 ┌───┴─────────────┐
 ▼                 ▼
Customer Email   Operations Email
```

---

# Features

* Automated customer request processing
* AI-powered relocation analysis
* Intelligent priority assignment
* Detection of missing information
* Automated operational recommendations
* Automatic Google Sheets updates
* Customer confirmation emails
* Operations team notifications
* Low-code implementation using n8n
* Runs with a local LLM using Ollama (no paid API required)

---

# Technology Stack

| Component           | Technology                  |
| ------------------- | --------------------------- |
| Workflow Automation | n8n                         |
| AI Model            | Ollama (Phi 3B / Local LLM) |
| Forms               | Google Forms                |
| Database            | Google Sheets               |
| Email               | Gmail                       |
| Programming         | JavaScript (n8n Code Nodes) |
| API Integration     | HTTP Request Node           |

---

# Workflow Nodes

1. Google Sheets Trigger
2. Set Node
3. HTTP Request (Ollama)
4. Code Node (Parse AI Response)
5. Code Node (Merge Original + AI Data)
6. IF Node (Priority Evaluation)
7. Google Sheets Update Row
8. Gmail (Customer Notification)
9. Gmail (Operations Notification)

---

# AI Processing

The AI model analyzes customer relocation requests and generates:

* Priority Level
* Request Summary
* Recommended Next Action
* Missing Information
* Confidence Score

Example Output

```json
{
  "priority": 4,
  "summary": "Customer is relocating from Goa to Bengaluru within 7 days and requires packers and internet setup.",
  "nextAction": "Assign Operations Executive immediately.",
  "confidence": 91,
  "missingInformation": [
    "Preferred Apartment Type"
  ]
}
```

---

# Google Sheet Structure

### Customer Information

* Timestamp
* Customer Name
* Email
* Phone Number
* Current City
* Destination City
* Move Date
* Family Size
* Property Type
* Budget
* Preferred Area

### AI Generated Fields

* Priority
* Status
* AI Summary
* Next Action
* Missing Information
* Confidence Score
* Processed Timestamp

---

# Business Rules

The AI applies the following logic:

* Move within 7 days → High Priority
* Budget above ₹1,00,000 → High Priority
* Corporate relocation → High Priority
* Missing phone number → Manual Review
* Missing budget → Flag for Follow-up
* Unsupported city → Escalate to Operations
* Incomplete request → Customer Follow-up Required

---

# Email Notifications

### Customer

* Confirmation of request submission
* Priority acknowledgement
* Next steps
* Contact information

### Operations Team

* Customer details
* AI-generated priority
* Summary
* Recommended action
* Missing information

---

# Project Structure

```text
QuickMove-AI-Automation/
│
├── README.md
├── workflow/
│   └── quickmove_workflow.json
│
├── prompts/
│   └── ollama_prompt.txt
│
├── architecture/
│   └── workflow_architecture.png
│
├── screenshots/
│   ├── workflow.png
│   ├── google_sheet.png
│   ├── gmail_notification.png
│   └── demo.png
│
└── docs/
    └── Solution_Report.pdf
```

---

# Installation

## Clone Repository

```bash
git clone https://github.com/yourusername/QuickMove-AI-Automation.git
```

---

## Install Ollama

Install Ollama and pull the required model:

```bash
ollama pull phi:latest
```

Start the Ollama server:

```bash
ollama serve
```

---

## Configure n8n

1. Import the workflow JSON.
2. Configure Google OAuth credentials.
3. Configure Gmail credentials.
4. Update the HTTP Request node URL:

```text
http://host.docker.internal:11434/api/generate
```

*(If n8n is running in Docker on Windows.)*

---

## Configure Google Services

* Create a Google Form
* Link it to a Google Sheet
* Add AI-related columns to the sheet
* Connect the sheet to the n8n workflow

---

# Running the Workflow

1. Submit a relocation request using Google Form.
2. Google Sheets Trigger starts the workflow.
3. Ollama analyzes the request.
4. AI assigns a priority and recommends the next action.
5. Google Sheet is updated.
6. Customer receives a confirmation email.
7. Operations team receives a notification.

---

# Expected Business Impact

| Metric                  | Improvement                                                             |
| ----------------------- | ----------------------------------------------------------------------- |
| Manual Data Entry       | Reduced by ~80%                                                         |
| Request Processing Time | Reduced from 10–15 minutes to under 1 minute                            |
| Priority Assignment     | Automated and consistent                                                |
| Customer Response Time  | Significantly faster                                                    |
| Operational Efficiency  | Improved through AI-driven triage                                       |
| Scalability             | Supports higher request volumes without proportional staffing increases |

---

# Future Enhancements

* WhatsApp integration for customer updates
* CRM integration (Salesforce, HubSpot)
* Vendor auto-assignment
* SMS notifications
* AI chatbot for customer queries
* Dashboard with real-time analytics
* Multi-language support
* RAG-based knowledge integration for relocation policies

---

# Demo

The workflow demonstrates an end-to-end AI-powered relocation process:

1. Customer submits a relocation request.
2. AI analyzes the request.
3. Priority is assigned automatically.
4. Operational data is updated in Google Sheets.
5. Notifications are sent to the customer and operations team.

---

# Author

**Abhilash C**

AI Operations | Business Analytics | Workflow Automation | Generative AI | n8n | Ollama | MERN Stack

---

# License

This project was developed as part of an **AI Operations Engineer technical assignment** to demonstrate practical AI workflow automation using low-code tools and locally hosted large language models.
