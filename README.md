# WhatsApp Workforce Automation

An n8n workflow for managing shift confirmations and employee communication over WhatsApp.

The system sends shift details to workers, handles confirmations and declines, answers work-related questions, and escalates cases that need human attention.

## Workflow Overview

![Workflow Overview](images/workflow.png)

## What it does

* Sends scheduled WhatsApp messages with shift or event details
* Lets workers confirm or decline directly from WhatsApp
* Updates assignment status in Google Sheets
* Handles free-text questions from workers
* Supports text messages, voice notes, and images
* Uses assignment data and an internal knowledge base to answer questions
* Escalates cases such as lateness, cancellations, missing information, or unresolved issues to the office
* Logs incoming and outgoing messages for tracking and review

## How it works

The workflow has two main parts.

### 1. Shift communication

```text
Schedule
   ↓
Google Sheets
   ↓
Load today's assignments
   ↓
Validate assignment data
   ↓
Send WhatsApp message
   ↓
Worker confirms / declines
   ↓
Update assignment status
```

### 2. Worker assistant

```text
WhatsApp message
   ↓
Text / Voice / Image routing
   ↓
AI Agent
   ↓
Google Sheets + Knowledge Base + Date & Time
   ↓
Answer worker
      or
Escalate to the office
```

The AI agent is used for understanding worker questions and deciding when a case should be escalated. Operational steps such as confirmations, status updates, and validation are handled directly by the workflow.

## Tech stack

* n8n
* WhatsApp Cloud API
* OpenAI API
* Google Sheets
* Google Docs (knowledge base)
* JavaScript

## Validation and escalation

Before sending shift details, the workflow checks that the required assignment data is available.

If important information is missing, the message is not sent automatically. Instead, the case is forwarded to the office for review.

The workflow can also escalate cases such as lateness, cancellations, safety issues, and questions that cannot be resolved automatically.

## Repository

`workflow.json` contains a sanitized version of the n8n workflow.

Credentials, phone numbers, document IDs, webhook IDs, and other private values were removed or replaced before publishing.
