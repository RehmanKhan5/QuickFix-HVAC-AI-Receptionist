# Day 9 — Complete System Testing & Validation

## Overview

Day 9 focused on testing the QuickFix HVAC AI receptionist and its service-request automation with a successful routine request and invalid-request scenarios.

The objective was to verify that valid customer information could be processed through the n8n production workflow, that the routine request was recorded in Google Sheets, and that validation rules could reject requests with missing required information or without the required emergency-fee consent.

QuickFix HVAC & Cooling is a fictional business used for this portfolio demonstration.

**Evidence — Production routine service-request record:**

- [Production routine record — Part 1](https://github.com/RehmanKhan5/QuickFix-HVAC-AI-Receptionist/blob/main/screenshots/Day%209/01-day-9-production-routine-record-part-1.png)
- [Production routine record — Part 2](https://github.com/RehmanKhan5/QuickFix-HVAC-AI-Receptionist/blob/main/screenshots/Day%209/02-day-9-production-routine-record-part-2.png)
- [Production routine record — Part 3](https://github.com/RehmanKhan5/QuickFix-HVAC-AI-Receptionist/blob/main/screenshots/Day%209/03-day-9-production-routine-record-part-3.png)

## ElevenLabs Tool Integration

The `submit_service_request` tool connects Sarah, the AI receptionist, to the n8n service-request workflow. The tool passes customer and service details to the configured webhook so that the workflow can validate and process the request.

The Day 9 evidence includes a successful ElevenLabs tool test.

**Evidence:** [ElevenLabs tool test success](https://github.com/RehmanKhan5/QuickFix-HVAC-AI-Receptionist/blob/main/screenshots/Day%209/05-day-9-elevenlabs-tool-test-success.png)

## Routine Service Request Integration

A routine AC repair request was processed through the production service-request workflow. The request information passed validation, and the resulting record was verified in Google Sheets.

The workflow uses the production webhook rather than relying on a temporary test webhook.

This test demonstrates the connection between the service-request intake, n8n validation and processing, and Google Sheets record creation.

**Evidence:**

- [Routine service-request record — Part 1](https://github.com/RehmanKhan5/QuickFix-HVAC-AI-Receptionist/blob/main/screenshots/Day%209/01-day-9-production-routine-record-part-1.png)
- [Routine service-request record — Part 2](https://github.com/RehmanKhan5/QuickFix-HVAC-AI-Receptionist/blob/main/screenshots/Day%209/02-day-9-production-routine-record-part-2.png)
- [Routine service-request record — Part 3](https://github.com/RehmanKhan5/QuickFix-HVAC-AI-Receptionist/blob/main/screenshots/Day%209/03-day-9-production-routine-record-part-3.png)

## n8n Workflow Processing

The service-request workflow processes incoming information through the configured webhook, field preparation, validation, routing, and response steps.

The routine request passed validation. The validation output indicated:

- `phoneValid: true`
- `serviceAreaValid: true`
- `serviceArea: austin`
- `emergencyFeeValid: true`
- `isValid: true`
- `missingFields: []`

These results indicate that the tested routine request satisfied the workflow's validation checks.

**Evidence:**

- [Production routine record — Part 2](https://github.com/RehmanKhan5/QuickFix-HVAC-AI-Receptionist/blob/main/screenshots/Day%209/02-day-9-production-routine-record-part-2.png)
- [Production routine record — Part 3](https://github.com/RehmanKhan5/QuickFix-HVAC-AI-Receptionist/blob/main/screenshots/Day%209/03-day-9-production-routine-record-part-3.png)

## Google Sheets Service Request Record

The routine request was recorded in the configured Google Sheets destination. The saved record provides evidence that the tested request reached the data-recording stage.

The record includes the submitted service details and the routine request's emergency and fee-consent values.

For this routine scenario:

- `Emergency: FALSE`
- `Fee Agreed: FALSE`

Emergency-fee consent is relevant when the emergency-fee policy applies. The workflow must not treat consent as given unless the customer explicitly agrees.

**Evidence:** [Routine service-request record — Part 3](https://github.com/RehmanKhan5/QuickFix-HVAC-AI-Receptionist/blob/main/screenshots/Day%209/03-day-9-production-routine-record-part-3.png)

## Required-Field Validation

Day 9 also included tests for requests with missing required information.

The workflow's validation rules are intended to prevent incomplete service requests from being accepted as valid submissions. This helps protect the quality of the information collected for the HVAC business.

The available evidence documents the missing-required-field rejection scenario.

**Evidence:**

- [Missing required field — Part A](https://github.com/RehmanKhan5/QuickFix-HVAC-AI-Receptionist/blob/main/screenshots/Day%209/06a-day-9-missing-required-field-rejection.png)
- [Missing required field — Part B](https://github.com/RehmanKhan5/QuickFix-HVAC-AI-Receptionist/blob/main/screenshots/Day%209/06b-day-9-missing-required-field-rejection.png)

## Emergency-Fee Consent Validation

The emergency-fee consent validation test checks that an emergency request cannot be treated as having customer approval when the required consent has not been provided.

This is an important business rule because an AI receptionist should not record or communicate fee agreement on the customer's behalf without explicit approval.

The Day 9 evidence documents the emergency-fee consent rejection scenario.

**Evidence:**

- [Emergency-fee consent rejection — Part A](https://github.com/RehmanKhan5/QuickFix-HVAC-AI-Receptionist/blob/main/screenshots/Day%209/07a-day-9-emergency-fee-consent-rejection.png)
- [Emergency-fee consent rejection — Part B](https://github.com/RehmanKhan5/QuickFix-HVAC-AI-Receptionist/blob/main/screenshots/Day%209/07b-day-9-emergency-fee-consent-rejection.png)

## Voice Conversation and Customer Confirmation

The receptionist must use the actual tool result to determine whether a service request was submitted successfully. A natural-sounding conversation alone is not proof that the underlying workflow recorded a request.

Sarah must not claim that an appointment is confirmed, a technician has been dispatched, or a real employee has been notified unless the connected system actually confirms that action.

Day 9 documentation therefore distinguishes verified workflow and Google Sheets results from conversational behavior that has not been independently confirmed.

## Customer Value

The Day 9 work demonstrates several useful capabilities for a home-service business:

- Processing and recording a valid routine service request.
- Validating incoming customer information.
- Checking the service area.
- Applying required-field rules.
- Enforcing emergency-fee consent requirements.
- Connecting the AI receptionist tool to an n8n workflow.
- Recording accepted routine requests in Google Sheets.

These capabilities can help organize incoming service requests and reduce manual data entry. The project remains a portfolio prototype using fictional business information and policies, not a live HVAC dispatch system.

## Day 9 Completion Summary

Day 9 produced evidence of a successfully recorded routine service request, an ElevenLabs tool test, and validation tests for missing required information and emergency-fee consent.

The eight selected proof-of-work screenshots were committed and pushed to GitHub. Failed emergency voice submission screenshots remain private and are not included in the public evidence set.

**Project limitation:** A recorded service request does not, by itself, confirm an appointment or guarantee technician dispatch.