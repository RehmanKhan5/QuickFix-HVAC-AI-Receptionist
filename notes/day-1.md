QuickFix HVAC — Day 1 Notes
1. Day 1 Overview

Day 1 is the foundation and documentation setup day for the QuickFix HVAC AI Voice Receptionist project.

The main purpose of Day 1 was to organize the project properly, establish the project structure, document the system architecture and testing strategy, and begin the first technical implementation.

The project is a portfolio prototype for learning and demonstration purposes.

It is not connected to a real HVAC company or real customers.

2. Project Name

QuickFix HVAC — 24/7 AI Voice Receptionist & Service Request Automation

Fictional Company

QuickFix HVAC & Cooling

Location

Austin, Texas, USA

Project Type

Portfolio prototype / learning project

Main Goal

Build an AI voice receptionist that can:

Answer customer calls.
Understand HVAC service requests.
Collect customer information.
Identify routine and emergency situations.
Submit valid service requests to n8n.
Validate incoming service-request information.
Save service requests to Google Sheets.
Return the correct result to the AI agent.
Create post-call records.
Send Gmail notifications.
Handle errors and unsafe situations safely.
3. Project Folder Structure

The main project folder was created:

QuickFix-HVAC-AI-Receptionist/
├── workflows/
├── prompts/
├── knowledge/
├── sample-data/
├── screenshots/
├── docs/
└── notes/

The purpose of these folders is:

workflows/

Used for exported n8n workflow JSON files.

prompts/

Used for ElevenLabs AI agent prompts.

knowledge/

Used for business knowledge files such as services, pricing, FAQs, business hours, and service area.

sample-data/

Used for sample JSON files and structured test scenarios.

screenshots/

Used to store important project screenshots and milestone evidence.

docs/

Used for project documentation such as architecture and testing documentation.

notes/

Used for daily learning and development notes.

4. Documentation Files Created

The following documentation files were created during the initial project setup.

README.md

The main project documentation file.

It explains the project, its purpose, technology stack, architecture, and important information for understanding the project.

docs/architecture.md

This file documents the system architecture and explains how the different components work together.

The planned main architecture is:

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

A separate post-call workflow will process call information after the conversation.

5. Testing Documentation

The following file was created:

docs/testing.md

This document explains how the complete system will be tested.

Testing will be performed gradually so that individual components can be verified before moving to the next stage.

The planned testing sequence is:

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

The purpose of this sequence is to identify problems at the simplest level first.

This makes troubleshooting easier because each part of the system can be tested separately.

6. Important Testing Areas Documented

The testing documentation covers:

Normal service requests.
Emergency service requests.
Missing customer information.
Invalid information.
Customers outside the service area.
Emergency fee declined.
Safety-related situations.
Human assistance requests.
Tool or webhook failure.
Google Sheets service-request records.
Google Sheets call-history records.
Gmail notifications.
Optional SMS notifications.
Conversation context continuity.
Final voice-call behavior.
Final acceptance criteria.
7. Test Cases Documented

The following test cases were documented:

TC-001

Normal AC repair request.

TC-002

HVAC maintenance request.

TC-003

Heating repair request.

TC-004

Customer requests a quote.

TC-005

Service request with missing information.

TC-006

Emergency AC failure.

TC-007

Suspected gas smell.

TC-008

Fire, smoke, sparks, or electrical danger.

TC-009

Indoor AC water leak.

TC-010

Emergency fee declined.

TC-011

Customer outside the service area.

TC-012

Customer requests a human.

TC-013

Invalid customer information.

TC-014

Service request tool failure.

TC-015

Google Sheets service-request record.

TC-016

Google Sheets call-history record.

TC-017

Gmail notification.

TC-018

Optional SMS notification.

TC-019

Conversation context continuity.

These tests are documented but have not all been performed yet.

Their initial status is:

NOT TESTED

The status will be changed after the actual tests are performed.

8. Important Architecture Decision

One important design principle established during Day 1 is that Google Sheets should not be written on every conversation turn.

The AI agent should maintain the context of the current conversation.

The service request should be written to Google Sheets when the required information has been collected and the request is ready to be submitted.

The basic flow is:

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

This helps keep the workflow organized and avoids unnecessary database writes during the conversation.

9. Important Business Rules

The AI receptionist must not:

Invent prices.
Invent services.
Invent appointment availability.
Promise a technician arrival time without confirmation.
Claim that a booking is confirmed without an actual booking confirmation.
Claim that an email or SMS was successfully sent unless the workflow confirms it.
Claim that a service request was successfully submitted before n8n confirms success.
Provide professional HVAC diagnoses.
Give unsafe repair instructions.
Collect unnecessary personal information.

The AI receptionist should provide truthful responses based on the available business information and tool results.

10. Emergency and Safety Principle

Safety situations require different handling from normal HVAC requests.

Examples include:

Suspected gas smell.
Fire.
Smoke.
Sparks.
Electrical danger.
Serious water leakage involving electrical equipment.
Extreme heat or cold situations.

The AI agent must not provide unsafe DIY instructions.

The agent should follow the defined emergency and safety procedures and must not falsely claim that a technician or emergency service has been dispatched.

11. Git Repository Setup

The project was initialized as a Git repository so that project files can be tracked, organized, versioned, and backed up to GitHub.

Git also makes it easier to see what has changed during development.

11.1 Initialize Git

The project folder was opened in the terminal and the following command was used:

git init

This created a local Git repository inside the project folder.

11.2 Create .gitignore

A .gitignore file was created in the root of the project.

Its purpose is to tell Git which files and folders should not be included in the repository.

The .gitignore file includes:

.env
node_modules/
.vscode/
.idea/
Why these files are ignored
.env — may contain private API keys, passwords, tokens, or other secrets.
node_modules/ — contains installed dependencies and normally does not need to be uploaded to GitHub.
.vscode/ — contains local Visual Studio Code settings.
.idea/ — contains local JetBrains IDE settings.
12. .env.example

An .env.example file was also created.

This file is used as a safe template showing which environment variables the project may need.

It should contain variable names and placeholders rather than real secret values.

For example:

API_KEY=your_api_key_here

The .env.example file must not contain real API keys or other private credentials.

13. Important Security Rule

Never place real API keys, passwords, access tokens, webhook secrets, or other private credentials inside GitHub.

Real secrets should remain in an appropriate secure location.

The .env file is included in .gitignore so that Git does not normally track it.

The .env.example file can be used as a template because it contains variable names and placeholders rather than real credentials.

14. Sample Data

The sample-data/ folder was prepared for structured HVAC test scenarios.

The sample data is used to test different situations before performing complete voice-based testing.

The project contains multiple HVAC scenarios covering normal requests, emergencies, missing information, safety situations, human requests, and tool failures.

These JSON files provide consistent test data for the project.

15. n8n Test Webhook

The first n8n technical implementation was started during Day 1.

An n8n Webhook node was created for receiving service-request information.

Webhook Name

Test Webhook

HTTP Method

POST

Webhook Path
quickfix-hvac-service-request

The webhook path becomes part of the webhook URL.

The purpose of the webhook is to receive structured JSON data from an external source such as Postman or, later, the ElevenLabs service-request tool.

Development Testing

The Test URL is being used during development and testing.

The production URL will be used later when the workflow is ready for the appropriate integration.

16. n8n Webhook Testing Flow

The current basic testing flow is:

Postman
   ↓
POST Request
   ↓
n8n Test Webhook
   ↓
Receive JSON

The purpose of this test is to confirm that n8n can correctly receive structured service-request data.

17. Sample Service Request JSON

A sample service-request structure was prepared for testing:

{
  "customerName": "John Smith",
  "phone": "+15125550123",
  "email": "john@example.com",
  "address": "123 Austin Street, Austin, TX",
  "serviceType": "AC Repair",
  "issue": "AC is blowing warm air",
  "emergency": false,
  "feeAgreed": true,
  "preferredTime": "As soon as possible"
}

This sample data represents a normal HVAC service request.

18. Postman Testing

Postman will be used to send sample JSON data to the n8n Test Webhook.

The planned request configuration is:

Method
POST
Body
raw
Data Type
JSON
Header
Content-Type: application/json

The purpose of the Postman test is to verify that the n8n Webhook receives the JSON correctly.

Current Status

PENDING

The Postman request has not yet been completed.

19. Screenshot Documentation

Important development screenshots are stored in:

screenshots/

The n8n Test Webhook screenshot was captured and saved as:

screenshots/n8n-test-webhook.png

The screenshot was added to Git and pushed to the GitHub repository.

This provides visual evidence of the development milestone.

20. GitHub Backup and Version Control

The project is connected to GitHub.

Repository:

QuickFix-HVAC-AI-Receptionist

GitHub account/handle:

RehmanKhan5

The project uses Git to track changes and GitHub to store the project repository remotely.

A typical Git workflow is:

git status
git add .
git commit -m "Describe what was added"
git push

For a specific file, for example:

git add notes/day-1.md
git commit -m "Update Day 1 project notes"
git push
21. Screenshot GitHub Commit

The n8n Test Webhook screenshot was successfully committed and pushed to GitHub.

The file is:

screenshots/n8n-test-webhook.png

The successful push confirmed that the screenshot is now stored in the remote GitHub repository.

22. Documentation Principle

This project is intentionally being documented in detail because it is both:

A learning project.
A portfolio project.

The documentation will make it easier to:

Understand what was built.
Remember what was learned.
Troubleshoot problems.
Demonstrate the project to potential clients.
Maintain the GitHub portfolio repository.
Explain the project during an Upwork proposal or client discussion.

Future real client projects do not necessarily need this same level of documentation.

The documentation can be lighter when the workflow and requirements are already understood.

23. Day 1 Completion Status
Completed

Main project folder created.

Project subfolders created.

Git repository initialized.

.gitignore created.

.env.example created.

README.md created.

docs/architecture.md created.

docs/testing.md created.

Testing strategy documented.

Test cases documented.

Important architecture decisions documented.

Important business rules documented.

Safety principles documented.

sample-data/ prepared.

n8n Cloud project started.

n8n Test Webhook created.

Webhook HTTP method configured as POST.

Webhook path configured.

Test Webhook screenshot captured.

Screenshot saved in screenshots/.

Screenshot committed to Git.

Screenshot pushed to GitHub.

Not Yet Completed

Complete Postman test.

Confirm JSON reception in n8n.

Create Edit Fields / data preparation step.

Create validation logic.

Create IF / routing logic.

Configure Google Sheets.

Configure Respond to Webhook.

Create the ElevenLabs agent.

Configure the submit_service_request tool.

Configure the post-call webhook.

Configure Gmail notification.

Perform ElevenLabs testing.

Perform browser voice testing.

Perform Twilio telephone testing.

Complete final end-to-end testing.

Prepare final GitHub portfolio documentation.

Record the final demonstration.

24. Lessons Learned on Day 1

The main lesson from Day 1 is that an AI voice receptionist is not only a voice chatbot.

The complete system contains:

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

A complete AI receptionist should therefore be designed as a business workflow rather than only as a conversation.

Another important lesson is that structured testing makes a complex automation easier to understand and troubleshoot.

The project is being developed step by step:

Project Foundation
        ↓
Documentation
        ↓
Sample Data
        ↓
n8n Webhook
        ↓
Postman
        ↓
n8n Workflow
        ↓
ElevenLabs
        ↓
Telephone Integration
        ↓
Final End-to-End Test
25. Day 1 Final Summary

Day 1 established the foundation of the QuickFix HVAC project.

The project structure and main documentation were created before moving deeper into the technical implementation.

The architecture, testing strategy, test cases, business rules, safety principles, Git repository, sample data structure, and n8n Test Webhook were established.

The Test Webhook screenshot was also documented and pushed to GitHub.

The next stage of the project will continue with the Postman test and then proceed to the remaining n8n workflow implementation.

Day 1 Status: FOUNDATION AND INITIAL WEBHOOK SETUP COMPLETE