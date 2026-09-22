# QuickFix HVAC — Day 1 Notes

## 1. Day 1 Overview

Day 1 is the foundation and documentation setup day for the QuickFix HVAC AI Voice Receptionist project.

The main purpose of Day 1 was to organize the project properly before starting the actual technical build.

The project is a portfolio prototype for learning and demonstration purposes.

It is not connected to a real HVAC company or real customers.

---

## 2. Project Name

**QuickFix HVAC — 24/7 AI Voice Receptionist & Service Request Automation**

### Fictional Company

**QuickFix HVAC & Cooling**

### Location

Austin, Texas, USA

### Project Type

Portfolio prototype / learning project

### Main Goal

Build an AI voice receptionist that can:

* Answer customer calls.
* Understand HVAC service requests.
* Collect customer information.
* Identify routine and emergency situations.
* Submit valid service requests to n8n.
* Save service requests to Google Sheets.
* Return the correct result to the AI agent.
* Create post-call records.
* Send Gmail notifications.
* Handle errors and unsafe situations safely.

---

## 3. Project Folder Structure

The main project folder was created:

```text
QuickFix-HVAC-AI-Receptionist/
├── workflows/
├── prompts/
├── knowledge/
├── sample-data/
├── screenshots/
├── docs/
└── notes/
```

The purpose of these folders is:

### workflows/

Used for exported n8n workflow JSON files.

### prompts/

Used for ElevenLabs AI agent prompts.

### knowledge/

Used for business knowledge files such as services, pricing, FAQs, business hours, and service area.

### sample-data/

Used for sample JSON files for testing.

### screenshots/

Used to store important project screenshots and milestone evidence.

### docs/

Used for project documentation such as architecture and testing documentation.

### notes/

Used for daily learning and development notes.

---

## 4. Documentation Files Created

The following documentation files were created on Day 1:

### README.md

The main project documentation file.

It explains the project, its purpose, technology stack, architecture, and important information for understanding the project.

### docs/architecture.md

This file documents the system architecture and explains how the different components work together.

The main architecture is:

```text
Customer
   ↓
Twilio
   ↓
ElevenLabs AI Voice Agent
   ↓
submit_service_request
   ↓
n8n
   ↓
Validation / Business Logic
   ↓
Google Sheets
   ↓
Respond to Webhook
   ↓
ElevenLabs
   ↓
Customer
```

A separate post-call workflow will process call information after the conversation.

---

## 5. Testing Documentation Created

The following file was also created:

```text
docs/testing.md
```

This document explains how the complete system will be tested.

Testing will be performed gradually instead of immediately making real telephone calls.

The planned testing sequence is:

```text
Sample JSON
↓
Postman
↓
n8n Webhook
↓
n8n Workflow
↓
ElevenLabs Text Testing
↓
ElevenLabs Browser Voice Testing
↓
Twilio Telephone Testing
```

The purpose of this sequence is to identify problems at the simplest level first.

This helps reduce:

* Unnecessary API usage.
* Unnecessary telephone usage.
* Debugging difficulty.
* Repeated voice calls.
* Unnecessary Twilio costs.

---

## 6. Important Testing Areas Documented

The testing documentation covers:

1. Normal service requests.
2. Emergency service requests.
3. Missing customer information.
4. Invalid information.
5. Customers outside the service area.
6. Emergency fee declined.
7. Safety-related situations.
8. Human assistance requests.
9. Tool or webhook failure.
10. Google Sheets service-request records.
11. Google Sheets call-history records.
12. Gmail notifications.
13. Optional SMS notifications.
14. Conversation context continuity.
15. Final voice-call behavior.
16. Final acceptance criteria.

---

## 7. Test Cases Documented

The following test cases were documented:

### TC-001

Normal AC repair request.

### TC-002

HVAC maintenance request.

### TC-003

Heating repair request.

### TC-004

Customer requests a quote.

### TC-005

Service request with missing information.

### TC-006

Emergency AC failure.

### TC-007

Suspected gas smell.

### TC-008

Fire, smoke, sparks, or electrical danger.

### TC-009

Indoor AC water leak.

### TC-010

Emergency fee declined.

### TC-011

Customer outside the service area.

### TC-012

Customer requests a human.

### TC-013

Invalid customer information.

### TC-014

Service request tool failure.

### TC-015

Google Sheets service-request record.

### TC-016

Google Sheets call-history record.

### TC-017

Gmail notification.

### TC-018

Optional SMS notification.

### TC-019

Conversation context continuity.

These tests are documented but have not yet been performed.

Their initial status is:

**NOT TESTED**

The status will be changed after the actual tests are performed.

---

## 8. Important Architecture Decision

One important design principle established during Day 1 is that Google Sheets should not be written on every conversation turn.

The AI agent should maintain the context of the current conversation.

The service request should be written to Google Sheets when the required information has been collected and the request is ready to be submitted.

The basic flow is:

```text
Customer Conversation
        ↓
Information Collection
        ↓
Information Confirmation
        ↓
Service Request Tool
        ↓
n8n Validation
        ↓
Google Sheets
```

This helps avoid unnecessary workflow executions and unnecessary database writes during the conversation.

---

## 9. Important Business Rules

The AI receptionist must not:

* Invent prices.
* Invent services.
* Invent appointment availability.
* Promise a technician arrival time without confirmation.
* Claim that a booking is confirmed without an actual booking confirmation.
* Claim that an email or SMS was successfully sent unless the workflow confirms it.
* Claim that a service request was successfully submitted before n8n confirms success.
* Provide professional HVAC diagnoses.
* Give unsafe repair instructions.
* Collect unnecessary personal information.

The AI receptionist should provide truthful responses based on the available business information and tool results.

---

## 10. Emergency and Safety Principle

Safety situations require different handling from normal HVAC requests.

Examples include:

* Suspected gas smell.
* Fire.
* Smoke.
* Sparks.
* Electrical danger.
* Serious water leakage involving electrical equipment.
* Extreme heat or cold situations.

The AI agent must not provide unsafe DIY instructions.

The agent should follow the defined emergency and safety procedures and must not falsely claim that a technician or emergency service has been dispatched.

---

## 11. Documentation Principle

This project is intentionally being documented in detail because it is both:

* A learning project.
* A portfolio project.

The documentation will make it easier to:

* Understand what was built.
* Remember what was learned.
* Troubleshoot problems.
* Demonstrate the project to potential clients.
* Create a GitHub portfolio repository.
* Explain the project during an Upwork proposal or client discussion.

Future real client projects do not necessarily need this same level of documentation.

The documentation can be lighter when the workflow and requirements are already understood.

---

## 12. Day 1 Completion Status

### Completed

* [x] Main project folder created.
* [x] Project subfolders created.
* [x] `README.md` created.
* [x] `docs/architecture.md` created.
* [x] `docs/testing.md` created.
* [x] Testing strategy documented.
* [x] Test cases documented.
* [x] Final testing checklist documented.
* [x] Important architecture and business rules documented.

### Not Yet Completed

The following technical implementation tasks will be completed on later days:

* [ ] Create the actual n8n workflows.
* [ ] Configure n8n Webhook.
* [ ] Create validation logic.
* [ ] Connect Google Sheets.
* [ ] Configure Respond to Webhook.
* [ ] Create the ElevenLabs agent.
* [ ] Configure the service-request tool.
* [ ] Configure the post-call webhook.
* [ ] Configure Gmail notification.
* [ ] Prepare sample JSON files.
* [ ] Test with Postman.
* [ ] Perform ElevenLabs testing.
* [ ] Perform Twilio testing.
* [ ] Complete final testing.
* [ ] Prepare GitHub portfolio repository.
* [ ] Record the final demonstration.

---

## 13. Lessons Learned on Day 1

The main lesson from Day 1 is that an AI voice receptionist is not only a voice chatbot.

The complete system contains:

```text
Voice Agent
     +
Automation
     +
Business Logic
     +
Data Storage
     +
Notifications
     +
Error Handling
     +
Safety Rules
```

A successful AI receptionist should therefore be designed as a complete business workflow rather than only as a conversation.

---

## 14. Day 1 Final Summary

Day 1 established the foundation of the QuickFix HVAC project.

The project structure and main documentation were created before starting the technical implementation.

The architecture, testing strategy, test cases, business rules, safety principles, and acceptance criteria have been documented.

The next stage of the project will move from documentation into the actual technical implementation.

**Day 1 Status: FOUNDATION COMPLETE**

# 4. Git Repository Setup

## 4.1 Purpose

The project was initialized as a Git repository so that the project files can be tracked, organized, versioned, and later backed up to GitHub.

Git will also make it easier to see what has changed during the development of the QuickFix HVAC AI Receptionist project.

## 4.2 Initialize Git

The project folder was opened in the terminal.

The following command was used:

```bash
git init
```

This created a local Git repository inside the project folder.

## 4.3 Create `.gitignore`

A `.gitignore` file was created in the root of the project.

Its purpose is to tell Git which files and folders should not be included in the repository.

The `.gitignore` file includes items such as:

```text
.env
node_modules/
.vscode/
.idea/
```

### Why these files are ignored

* `.env` — may contain private API keys, passwords, tokens, or other secrets.
* `node_modules/` — contains installed dependencies and normally does not need to be uploaded to GitHub.
* `.vscode/` — contains Visual Studio Code settings that are generally specific to the local computer.
* `.idea/` — contains JetBrains IDE settings that are generally specific to the local computer.

## 4.4 Create `.env.example`

An `.env.example` file was also created.

This file is used as a safe template showing which environment variables the project may need.

It can contain variable names such as:

```text
GEMINI_API_KEY=
AIRTABLE_API_KEY=
```

or other required configuration names as the project develops.

The `.env.example` file must **not** contain the real secret values.

For example:

```text
GEMINI_API_KEY=your_api_key_here
```

is acceptable as an example, while an actual API key must remain private.

## 4.5 Important Security Rule

**Never place real API keys, passwords, access tokens, webhook secrets, or other private credentials inside GitHub.**

Real secrets should remain in the local `.env` file or another appropriate secure secret-management system.

The `.env` file is included in `.gitignore` so that Git does not normally track it.

The `.env.example` file is safe to use as a template because it contains variable names and placeholders rather than real credentials.

## 4.6 Day 1 Git Setup Result

The QuickFix HVAC project now has a local Git repository with basic protection against accidentally committing sensitive information.

The repository will later be used to organize and back up project files such as:

* n8n workflow exports
* ElevenLabs prompts
* Knowledge files
* Sample test data
* Documentation
* Testing records
* Screenshots
* Project notes
* README.md

GitHub backup will be completed as part of the appropriate later project step.
