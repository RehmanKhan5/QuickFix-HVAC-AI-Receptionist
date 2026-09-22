# QuickFix HVAC — AI Voice Receptionist & Service Request Automation

## Project Overview

QuickFix HVAC & Cooling is a fictional HVAC company created for this portfolio project.

The goal of this project is to build a professional AI voice receptionist that can handle inbound customer calls, understand HVAC service requests, collect required customer information, identify potentially urgent situations, and submit service requests through an automated workflow.

The project demonstrates how AI voice technology can be combined with workflow automation to create an AI system that does more than simply have a conversation.

---

## Project Type

Portfolio Prototype / Demonstration Project

---

## Industry

HVAC — Heating, Ventilation and Air Conditioning

---

## Fictional Company

QuickFix HVAC & Cooling

Location: Austin, Texas, USA

Service Area:

- Austin
- Round Rock
- Pflugerville
- Cedar Park

---

## Project Objective

The main objective is to create a 24/7 AI voice receptionist that can:

- Answer inbound customer calls.
- Understand the customer's request.
- Identify the requested HVAC service.
- Check whether the customer is within the service area.
- Identify potentially urgent situations.
- Collect the required customer information.
- Confirm important information with the customer.
- Submit a service request through n8n.
- Store the service request in Google Sheets.
- Return the actual workflow result to the AI voice agent.
- Record completed calls.
- Send post-call notifications.
- Handle errors without falsely claiming that an action succeeded.

---

## Technologies Used

- ElevenLabs Conversational AI
- n8n
- Twilio
- Google Sheets
- Gmail
- Optional SMS
- Postman
- GitHub
- Cloudflare Tunnel where applicable during local development

---

## Main Architecture

Customer

↓

Twilio

↓

ElevenLabs AI Voice Agent

↓

submit_service_request Tool

↓

n8n Webhook

↓

Data Normalization

↓

Validation

↓

Emergency / Routine Routing

↓

Google Sheets

↓

Respond to Webhook

↓

ElevenLabs

↓

Customer

---

## Post-Call Architecture

ElevenLabs Post-Call Webhook

↓

n8n

↓

Data Normalization

↓

Google Sheets — Call History

↓

Gmail

↓

Optional SMS

---

## Main n8n Workflows

### 1. Live Service Request Workflow

The live workflow handles service requests during the customer conversation.

Main flow:

Webhook

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

---

### 2. Post-Call Recording Workflow

The post-call workflow handles information after the call has ended.

Main flow:

ElevenLabs Post-Call Webhook

↓

Edit Fields

↓

Google Sheets — Call History

↓

Gmail

↓

Optional SMS

---

## AI Voice Agent

The AI receptionist is named Sarah.

First message:

"Thank you for calling QuickFix HVAC & Cooling. This is Sarah. How can I help you today?"

The AI is designed to communicate in a:

- Friendly
- Professional
- Calm
- Clear
- Concise
- Natural

manner.

---

## HVAC Services

The fictional company provides:

- AC repair
- Heating repair
- HVAC maintenance
- HVAC tune-ups

---

## Demonstration Pricing

The following prices are fictional values created only for this portfolio demonstration.

### Standard Diagnostic Fee

$89

### Emergency Dispatch Fee

$180

The AI must never present these demonstration prices as real-world company pricing.

---

## Service Request Information

### Emergency Request

The AI should collect:

- Full name
- Phone number
- Service address
- Brief issue description
- Emergency classification
- Fee agreement when applicable

### Routine Request

The AI should collect:

- Full name
- Phone number
- Email when required
- Service type
- Preferred appointment time

---

## Emergency Examples

Potentially urgent examples include:

- AC not cooling
- System blowing warm air
- HVAC system stopped working
- Furnace not turning on
- Heating system not working
- Heating system blowing cold air
- Unusual HVAC noises
- Indoor water leak associated with AC

These examples are used for request classification only.

The AI does not perform professional HVAC diagnosis.

---

## Safety Rules

### Suspected Gas Smell

The AI should prioritize customer safety.

It should:

- Encourage the customer to move away from danger.
- Follow appropriate emergency safety guidance.
- Encourage contacting emergency services or the gas utility when appropriate.
- Avoid telling the customer to investigate a suspected leak.
- Avoid telling the customer to operate electrical switches.
- Avoid providing dangerous DIY instructions.
- Never claim that a technician has been dispatched unless this is actually confirmed.

### Fire, Smoke, Sparks or Electrical Danger

The AI should prioritize immediate safety and emergency services.

It should not provide unsafe repair instructions.

### Water Leakage

The AI should consider possible electrical hazards and avoid unsafe instructions.

### Extreme Heat or Cold

The AI should treat the situation as potentially urgent without making unsupported technician arrival promises.

---

## Business Rules

The AI must:

- Never invent prices.
- Never invent services.
- Never invent availability.
- Never claim payment was completed unless confirmed.
- Never claim a technician was dispatched unless confirmed.
- Never claim an appointment was confirmed unless the booking system actually confirms it.
- Never claim an email or SMS was sent unless confirmed.
- Never promise an exact technician arrival time unless confirmed.
- Never provide professional HVAC diagnosis.
- Never provide unsafe repair instructions.
- Never collect unnecessary personal information.

---

## Google Sheets

The main spreadsheet is:

QuickFix HVAC — Customer Service Requests

### Service Requests

The Service Requests sheet contains:

- Request ID
- Date/Time
- Customer Name
- Phone
- Email
- Address
- Service Area
- Service Type
- Issue
- Emergency
- Fee Agreed
- Preferred Time
- Status
- Notification Status
- Source
- Notes

### Call History

The Call History sheet contains:

- Call ID
- Date/Time
- Customer Name
- Phone
- Call Summary
- Call Outcome
- Request Status
- Source

---

## Important Architecture Decision

The live voice workflow must not tell the customer that a request was successfully submitted before Google Sheets has actually accepted the request.

The live workflow therefore follows:

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

Only after the required action succeeds should the AI receive a successful result.

Gmail and SMS notifications are handled outside the main live voice path whenever possible to reduce unnecessary call latency.

---

## Error Handling

The system will be tested for:

- Missing customer information
- Invalid request data
- Outside service area
- Fee declined
- Tool failure
- Google Sheets failure
- Gmail failure
- Invalid payload
- Other workflow errors

The AI must not falsely tell the customer that an action succeeded when the automation failed.

---

## Testing

The project will include tests for:

- Routine HVAC request
- Emergency HVAC request
- Missing information
- Outside service area
- Fee declined
- Request for human assistance
- Suspected gas smell
- Tool failure
- Google Sheets failure
- Gmail failure
- Post-call processing
- Duplicate request behavior
- Complete telephone call

---

## Portfolio Deliverables

The completed project will contain:

- AI voice agent
- n8n workflows
- Google Sheets database
- Gmail notification workflow
- Optional SMS notification
- System prompt
- Knowledge base
- Sample test data
- Testing documentation
- Architecture documentation
- Screenshots
- Workflow JSON exports
- GitHub repository
- Demo video
- Project README

---

## Project Limitations

This is a fictional portfolio demonstration.

It does not represent a real QuickFix HVAC business.

The project does not include:

- Real technician dispatch
- Real payment processing
- Professional HVAC diagnosis
- Guaranteed technician arrival times
- Real appointment confirmation unless a real booking system is connected
- Enterprise-level monitoring
- Full production-grade security infrastructure

Google Sheets is used as the MVP data storage layer.

---

## Project Status

Current Status:

Project Foundation

The project is being built step by step over a 10-day development plan.

---

## Development Approach

The project is being developed in the following order:

1. Project foundation
2. Data normalization and validation
3. Emergency and routine routing
4. Google Sheets service requests
5. Post-call recording
6. Gmail and optional SMS notifications
7. ElevenLabs AI voice agent
8. ElevenLabs tool integration
9. Twilio telephone integration
10. Complete testing and portfolio preparation

---

## Project Philosophy

The goal of this project is not simply to create an AI chatbot.

The goal is to demonstrate an AI system that can:

Understand → Validate → Execute → Record → Notify → Handle Failure

The AI voice agent handles the conversation while n8n performs the automation and business logic.