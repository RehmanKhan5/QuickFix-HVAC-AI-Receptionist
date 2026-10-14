# Day 7 — ElevenLabs Tool Integration & Service Request Automation

## Overview

Day 7 focuses on connecting Sarah, the QuickFix HVAC AI receptionist, to the n8n service-request workflow. The integration was tested to verify routine request submission, emergency handling, validation rules, service-area restrictions, and honest communication when a tool call fails.

QuickFix HVAC is a fictional portfolio demonstration project.

## ElevenLabs Tool Configuration

The `submit_service_request` tool was configured to send customer service-request details to the n8n production webhook. The request includes customer contact information, service address, service type, issue description, emergency status, fee consent, and preferred service time.

**Evidence:** [ElevenLabs Tool Configuration](../../screenshots/Day%207/01-day-7-elevenlabs-tool.png) · [Live Service Request Routing](../../screenshots/Day%207/02-day-7-live-service-request-routing.png)

## Routine Service Request Integration

A routine AC repair request was submitted through Sarah. After the customer confirmed the details, the tool executed successfully and the request was recorded in Google Sheets.

The recorded request included the customer name, phone number, email, address, service area, service type, issue, emergency status, fee consent, preferred time, and request status.

The routine request was recorded with `Emergency: false`, `Fee Agreed: false`, and `Status: New`. The response indicated that the request was received for scheduling; it did not represent a confirmed appointment.

**Evidence:** [Routine Google Sheets Record — Part 1](../../screenshots/Day%207/03a-day-7-google-sheets-routine-record.png) · [Routine Google Sheets Record — Part 2](../../screenshots/Day%207/03b-day-7-google-sheets-routine-record.png) · [Routine Validation Success](../../screenshots/Day%207/04-day-7-routine-validation-success.png) · [ElevenLabs Tool Execution — Part 1](../../screenshots/Day%207/10a-day-7-elevenlabs-tool-execution.png) · [ElevenLabs Tool Execution — Part 2](../../screenshots/Day%207/10b-day-7-elevenlabs-tool-execution.png) · [ElevenLabs Tool Execution — Part 3](../../screenshots/Day%207/10c-day-7-elevenlabs-tool-execution.png) · [Routine Webhook Input](../../screenshots/Day%207/11-day-7-routine-webhook-input.png) · [Routine Execution Path](../../screenshots/Day%207/12-day-7-routine-execution-path.png)

## Emergency Service Request Handling

An emergency AC repair scenario was tested using a request describing an AC system that had completely stopped working during extreme heat. The request was accepted by the workflow with emergency status and the applicable fee-consent field recorded as true.

The emergency path was tested separately from the routine request path.

**Evidence:** [Emergency Request — Part 1](../../screenshots/Day%207/05a-day-7-emergency-request-success.png) · [Emergency Request — Part 2](../../screenshots/Day%207/05b-day-7-emergency-request-success.png) · [Emergency Request — Part 3](../../screenshots/Day%207/05c-day-7-emergency-request-success.png)

## Validation and Service-Area Restrictions

Validation tests checked that requests missing required information or containing an address outside the supported service area were rejected rather than recorded as accepted service requests.

The missing-information test used a request without a phone number. The outside-area test used an address in Dallas, Texas. Both returned a rejection response, and no corresponding customer request row was found in Google Sheets during verification.

**Evidence:** [Missing Information Rejected](../../screenshots/Day%207/06-day-7-missing-information-rejected.png) · [Outside Service Area Rejected](../../screenshots/Day%207/07-day-7-outside-area-rejected.png)

## Webhook and Tool Failure Handling

A separate webhook failure simulation demonstrated the error returned when a deliberately unregistered production webhook endpoint was called.

The ElevenLabs integration was also tested with a temporarily invalid tool URL. Sarah reported that she could not confirm successful submission, explained that the request had not been recorded, and offered the customer a retry or human assistance.

This test demonstrates the importance of checking the actual tool result instead of claiming success when submission fails. The original production webhook URL was restored after the test.

**Evidence:** [Webhook Failure Simulation](../../screenshots/Day%207/08-day-7-webhook-failure-simulation.png) · [ElevenLabs Tool Failure Handling](../../screenshots/Day%207/13-day-7-elevenlabs-tool-failure.png)

## Customer Value

Day 7 demonstrates how a conversational AI receptionist can connect to an automation workflow to process service requests, validate required information, distinguish routine and emergency requests, record accepted requests in Google Sheets, and return a response to the customer.

The tests also demonstrate rejection handling for invalid requests and honest communication when the submission tool fails. The workflow records service requests for follow-up; it does not independently confirm an appointment or guarantee that a technician has been dispatched.

This is a portfolio prototype using fictional business information and demonstration policies. Production deployment would require business-owner approval, verified service and pricing policies, and appropriate operational safeguards.