# QuickFix HVAC — System Architecture

## 1. Project Overview

QuickFix HVAC & Cooling is a fictional HVAC company used for this portfolio project.

The project demonstrates how an AI voice receptionist can be connected to workflow automation so that the AI does not only communicate with customers but can also execute business actions.

The system combines:

- ElevenLabs Conversational AI
- Twilio
- n8n
- Google Sheets
- Gmail
- Optional SMS
- Postman
- GitHub

---

# 2. Main System Architecture

The overall system is divided into two major workflows:

1. Live Service Request Workflow
2. Post-Call Recording and Notification Workflow

The live workflow is responsible for actions that the AI needs during the active customer conversation.

The post-call workflow handles information after the call has ended.

---

# 3. Complete High-Level Architecture

```text
                         ┌─────────────────┐
                         │    CUSTOMER     │
                         └────────┬────────┘
                                  │
                                  ▼
                         ┌─────────────────┐
                         │     TWILIO      │
                         └────────┬────────┘
                                  │
                                  ▼
                    ┌─────────────────────────┐
                    │ ELEVENLABS AI AGENT     │
                    │        "SARAH"          │
                    └────────────┬────────────┘
                                 │
                       Tool: submit_service_request
                                 │
                                 ▼
                    ┌─────────────────────────┐
                    │       N8N WEBHOOK        │
                    └────────────┬────────────┘
                                 │
                                 ▼
                    ┌─────────────────────────┐
                    │     EDIT / NORMALIZE     │
                    └────────────┬────────────┘
                                 │
                                 ▼
                    ┌─────────────────────────┐
                    │       VALIDATION         │
                    └────────────┬────────────┘
                                 │
                                 ▼
                    ┌─────────────────────────┐
                    │      VALID / INVALID     │
                    └────────────┬────────────┘
                                 │
                                 ▼
                    ┌─────────────────────────┐
                    │  EMERGENCY / ROUTINE    │
                    └────────────┬────────────┘
                                 │
                                 ▼
                    ┌─────────────────────────┐
                    │     GOOGLE SHEETS        │
                    │    SERVICE REQUESTS      │
                    └────────────┬────────────┘
                                 │
                                 ▼
                    ┌─────────────────────────┐
                    │  RESPOND TO WEBHOOK      │
                    └────────────┬────────────┘
                                 │
                                 ▼
                    ┌─────────────────────────┐
                    │    ELEVENLABS AGENT      │
                    └────────────┬────────────┘
                                 │
                                 ▼
                         ┌─────────────────┐
                         │    CUSTOMER     │

                         └─────────────────┘




4. Live Service Request Workflow

The live workflow handles service requests while the customer is still talking to the AI receptionist.

The main workflow is:

Customer
↓
Twilio
↓
ElevenLabs
↓
submit_service_request
↓
n8n Webhook
↓
Edit Fields
↓
Code Validation
↓
IF
↓
Switch
↓
Google Sheets
↓
Respond to Webhook
↓
ElevenLabs
↓
Customer
5. Customer

The customer starts an inbound telephone call.

The customer may say things such as:

"My AC is not cooling."
"I need an HVAC tune-up."
"My furnace stopped working."
"I need a repair."
"Can someone come tomorrow?"

The AI receptionist is responsible for understanding the customer's request.

6. Twilio

Twilio provides the telephone connectivity for the demonstration.

The basic connection is:

Customer Phone
      ↓
    Twilio
      ↓
ElevenLabs Agent

Twilio is responsible for connecting the telephone call to the AI voice system.

Twilio is not responsible for the business logic.

7. ElevenLabs AI Voice Agent

The ElevenLabs agent acts as the AI receptionist.

The fictional receptionist is named:

Sarah

The first message is:

Thank you for calling QuickFix HVAC & Cooling. This is Sarah. How can I help you today?

The AI is responsible for:

Greeting the customer.
Understanding the request.
Checking the service area.
Performing a safety check.
Classifying the request.
Collecting required information.
Confirming important information.
Calling the appropriate tool.
Understanding the tool result.
Communicating the result to the customer.
Ending the call appropriately.
8. submit_service_request Tool

The ElevenLabs agent uses a custom tool:

submit_service_request

The tool uses:

POST

The tool sends structured customer information to the n8n webhook.

Example information:

customerName
phone
email
address
serviceType
issue
emergency
feeAgreed
preferredTime

The important concept is:

AI Conversation
       ↓
Structured Tool Call
       ↓
n8n Automation

The AI does not directly write to Google Sheets.

n8n performs the business logic and database operation.

9. n8n Webhook

The n8n Webhook receives the request from ElevenLabs.

The webhook acts as the entry point into the automation workflow.

Example:

ElevenLabs
     ↓
POST
     ↓
n8n Webhook

The incoming information is then processed by n8n.

10. Edit Fields / Normalization

The Edit Fields node organizes incoming information into consistent fields.

Example:

customerName
phone
email
address
serviceType
issue
emergency
feeAgreed
preferredTime

Normalization helps keep the data consistent before validation and storage.

11. Code Validation

The Code node checks whether the request contains the required information.

For example, an emergency request may require:

customerName
phone
address
issue
emergency

A routine request may require:

customerName
phone
serviceType
preferredTime

The validation stage helps prevent incomplete data from reaching Google Sheets.

12. IF Node

The IF node separates valid and invalid requests.

Architecture:

                 Validation
                     │
             ┌───────┴───────┐
             │               │
           Valid           Invalid
             │               │
             ▼               ▼
          Switch       Respond to Webhook

If the request is invalid, the AI receives an appropriate response.

If the request is valid, it continues through the business logic.

13. Switch Node

The Switch node separates requests into different business paths.

Main paths:

Emergency
Routine

Example:

                 Valid Request
                       │
                       ▼
                    Switch
                   /      \
                  /        \
                 ▼          ▼
            Emergency     Routine
14. Emergency Path

An emergency request should be handled carefully.

The AI should:

Identify the potentially urgent situation.
Perform appropriate safety screening.
Collect required customer information.
Explain applicable fictional demonstration fee when appropriate.
Obtain fee agreement when required.
Submit the request.
Wait for the actual workflow result.
Communicate the result without inventing dispatch or arrival information.

The AI must not provide professional HVAC diagnosis.

15. Routine Path

A routine request may include:

HVAC maintenance
Tune-up
AC repair
Heating repair

The AI collects the required information and preferred time.

The AI must not claim that an appointment is confirmed unless an actual booking/availability system confirms it.

16. Google Sheets

Google Sheets acts as the MVP data storage layer.

Spreadsheet:

QuickFix HVAC — Customer Service Requests

The main sheet is:

Service Requests

The columns are:

Request ID
Date/Time
Customer Name
Phone
Email
Address
Service Area
Service Type
Issue
Emergency
Fee Agreed
Preferred Time
Status
Notification Status
Source
Notes
17. Service Request Status

Possible statuses include:

New
Pending Review
Notification Sent
Awaiting Confirmation
Confirmed
Closed
Failed
Incomplete

The system must only use a status that accurately represents what has actually happened.

For example:

A request should not be marked:

Confirmed

unless the required booking or action has actually been confirmed.

18. Respond to Webhook

After the Google Sheets operation succeeds, n8n returns the actual result through:

Respond to Webhook

The important sequence is:

Validation
↓
Routing
↓
Google Sheets
↓
Respond to Webhook

This prevents the AI from being told that an action succeeded before the database operation has actually succeeded.

19. Important Live Workflow Rule

The system must not do this:

Webhook
↓
Respond "Success"
↓
Google Sheets

because Google Sheets could fail after the customer has already been told that the request succeeded.

Instead:

Webhook
↓
Edit Fields
↓
Validation
↓
IF
↓
Switch
↓
Google Sheets
↓
Respond to Webhook

The customer receives a success result only after the required action has actually succeeded.

20. Post-Call Workflow

The second workflow runs after the call.

Architecture:

ElevenLabs Post-Call Webhook
              ↓
             n8n
              ↓
        Edit / Normalize
              ↓
        Google Sheets
              ↓
         Call History
              ↓
            Gmail
              ↓
         Optional SMS
21. ElevenLabs Post-Call Webhook

The post-call webhook receives information after the call has finished.

It can be used for:

Call ID
Customer name
Phone
Call summary
Call outcome
Request status
Other post-call information

The post-call workflow is separate from the live service-request tool.

22. Call History

The second Google Sheets tab is:

Call History

Columns:

Call ID
Date/Time
Customer Name
Phone
Call Summary
Call Outcome
Request Status
Source

This provides a historical record of AI calls.

23. Gmail Notification

Gmail is used as a post-call notification system.

Example subject:

QuickFix HVAC — New AI Call Summary

The email can contain:

Customer Name
Phone
Service Type
Issue
Emergency Status
Request Status
Call Summary
Call ID

Gmail is intentionally kept outside the main live voice workflow whenever possible.

24. Optional SMS Notification

An optional SMS notification can be sent after the call.

Example:

QuickFix HVAC Alert: New service request from John Smith.
AC Repair — Emergency.
Check Google Sheets for details.

SMS is a notification layer.

It should not unnecessarily delay the live AI conversation.

25. Why Gmail and SMS Are Outside the Live Path

The live voice conversation should remain responsive.

Therefore:

Live Call
   ↓
AI
   ↓
n8n
   ↓
Google Sheets
   ↓
Response

is the important synchronous path.

Post-call notifications can then happen separately:

Call Ends
   ↓
Post-Call Workflow
   ↓
Gmail
   ↓
Optional SMS

This reduces unnecessary latency during the conversation.

26. Error Handling Architecture

The system must handle failures safely.

Examples:

Invalid Payload
Missing Customer Information
Google Sheets Failure
Gmail Failure
Tool Failure
API Failure

When an action fails, the AI should not falsely tell the customer that it succeeded.

27. Example Error Flow
Customer Request
       ↓
ElevenLabs
       ↓
n8n
       ↓
Validation
       ↓
Google Sheets
       ↓
       X
    FAILURE
       ↓
Respond to Webhook
       ↓
ElevenLabs
       ↓
Friendly Fallback

Example customer-facing behavior:

I'm sorry, I'm having trouble submitting that request right now.

The AI should not say:

Your request has been submitted.

unless the system actually confirms it.

28. Safety Architecture

Certain situations require safety-first behavior.

Examples:

Suspected gas smell
Fire
Smoke
Sparks
Electrical danger
Extreme heat
Extreme cold
Water leakage with possible electrical hazards

The AI should prioritize appropriate safety guidance and emergency services when necessary.

It should not provide dangerous DIY instructions.

29. Data Flow

The main data flow is:

Customer Information
        ↓
ElevenLabs
        ↓
Tool Parameters
        ↓
n8n Webhook
        ↓
Normalization
        ↓
Validation
        ↓
Business Logic
        ↓
Google Sheets
        ↓
Actual Result
        ↓
ElevenLabs
        ↓
Customer
30. Separation of Responsibilities

Each technology has a specific responsibility.

Twilio

Telephone connectivity.

ElevenLabs

AI voice conversation.

n8n

Automation and business logic.

Google Sheets

MVP data storage.

Gmail

Post-call email notification.

SMS

Optional post-call notification.

Postman

Testing API/webhook requests.

GitHub

Version control and project backup.

31. Credit-Saving Development Strategy

The project should not rely on repeated expensive voice calls during development.

The recommended testing progression is:

Sample JSON
      ↓
Postman
      ↓
n8n
      ↓
ElevenLabs Text Testing
      ↓
ElevenLabs Browser Voice
      ↓
Twilio Telephone Call

This allows most bugs to be discovered before telephone testing.

32. Testing Architecture

The project will test:

Routine Request

Normal HVAC service request.

Emergency Request

Potentially urgent HVAC situation.

Missing Information

Required information is missing.

Outside Service Area

Customer is outside the supported area.

Fee Declined

Customer does not agree to the applicable demonstration fee.

Human Request

Customer requests a human.

Safety Situation

Gas smell, fire, smoke, sparks or electrical danger.

Tool Failure

The ElevenLabs tool fails.

Google Sheets Failure

The database operation fails.

Gmail Failure

Post-call notification fails.

Duplicate Request

The same request is accidentally submitted more than once.

33. Project Security and Privacy Considerations

The portfolio prototype should avoid exposing credentials.

Do not store:

API keys
Passwords
Private credentials
Secret tokens

inside GitHub.

Use environment variables or secure credential storage where appropriate.

34. Production vs Portfolio Prototype

This project is a portfolio prototype.

A production system would require additional controls such as:

Authentication
Authorization
Rate limiting
Retry strategies
Idempotency
Monitoring
Logging
Alerting
Secure secret management
Failure queues
Stronger data protection
Production database
More robust booking integration
Advanced observability

These are outside the main 10-day MVP scope.

35. Final Architecture Summary

The complete system can be summarized as:

                         CUSTOMER
                            │
                            ▼
                          TWILIO
                            │
                            ▼
                    ELEVENLABS AI
                       "SARAH"
                            │
                            │
                  submit_service_request
                            │
                            ▼
                       N8N WEBHOOK
                            │
                            ▼
                     NORMALIZATION
                            │
                            ▼
                       VALIDATION
                            │
                            ▼
                    VALID / INVALID
                            │
                            ▼
                    EMERGENCY / ROUTINE
                            │
                            ▼
                     GOOGLE SHEETS
                            │
                            ▼
                  RESPOND TO WEBHOOK
                            │
                            ▼
                    ELEVENLABS AI
                            │
                            ▼
                         CUSTOMER


                       POST-CALL
                            │
                            ▼
                ELEVENLABS POST-CALL
                            │
                            ▼
                           N8N
                            │
                            ▼
                      CALL HISTORY
                            │
                            ▼
                          GMAIL
                            │
                            ▼
                       OPTIONAL SMS
36. Core Design Principle

The main principle of this project is:

AI should not only talk.

AI should understand → validate → execute → record → notify → handle failure.

ElevenLabs provides the conversational interface.

n8n provides the automation and business logic.

Google Sheets provides the MVP data storage.

Twilio provides telephone connectivity.

Gmail and optional SMS provide post-call notifications.