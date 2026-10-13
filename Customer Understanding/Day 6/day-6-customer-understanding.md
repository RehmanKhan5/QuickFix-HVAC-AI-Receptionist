# Day 6 — ElevenLabs AI Receptionist Configuration & Testing

## Overview

Day 6 focuses on configuring and testing Sarah, the QuickFix HVAC AI receptionist. The agent was tested with routine service inquiries, customer information collection, booking rules, pricing questions, and emergency situations.

## AI Receptionist Configuration

Sarah was configured to answer routine HVAC questions, collect and confirm customer information, follow service-area rules, and identify missing information.

**Evidence:** [Routine AC Tune-Up](../../screenshots/Day%206/01-day-6-routine-ac-tune-up.png) · [Customer Information](../../screenshots/Day%206/02-day-6-customer-information.png) · [Customer Details Acknowledged](../../screenshots/Day%206/03-day-6-customer-details-acknowledged.png) · [Service Area and Booking Rules](../../screenshots/Day%206/04-day-6-service-area-and-booking-rules.png) · [Customer Details Confirmation](../../screenshots/Day%206/05-day-6-customer-details-confirmation.png)

## Customer Request Handling

The agent was tested with emergency handling, out-of-area inquiries, missing information, and a routine AC repair request. These scenarios help evaluate how Sarah responds to different customer needs.

**Evidence:** [Emergency Handling](../../screenshots/Day%206/06-day-6-emergency-handling-test.png) · [Outside Service Area](../../screenshots/Day%206/07-day-6-outside-service-area-test.png) · [Missing Information](../../screenshots/Day%206/08-day-6-missing-information-test.png) · [Routine Request — Customer Details](../../screenshots/Day%206/09a-day-6-routine-request-confirmation-test.png) · [Routine Request — Follow-Up](../../screenshots/Day%206/09b-day-6-routine-request-confirmation-test.png) · [Routine Request — Response](../../screenshots/Day%206/09c-day-6-routine-request-confirmation-test.png) · [Routine Request — Confirmation](../../screenshots/Day%206/09d-day-6-routine-request-confirmation-test.png)

## Pricing and Fee Policies

Testing identified an incorrect diagnostic-fee answer. The pricing and FAQ knowledge files were updated to establish consistent demonstration policies.

- Standard AC diagnostic fee: $89.
- Standard heating diagnostic fee: $89.
- The diagnostic fee is waived when the customer approves the repair after diagnosis.
- Example emergency service fee: $180, with explicit customer agreement required when applicable.

These prices and policies are fictional and are provided for portfolio demonstration purposes. Final repair costs depend on the actual problem and work required.

**Evidence:** [Corrected Diagnostic Fee](../../screenshots/Day%206/10a-day-6-normal-diagnostic-fee-corrected.png) · [Corrected Diagnostic Fee Waiver](../../screenshots/Day%206/10b-day-6-diagnostic-fee-waiver-corrected.png) · [Emergency Fee Policy](../../screenshots/Day%206/10c-day-6-emergency-service-fee-policy-corrected.png)

## Conversation Quality and Safety

Sarah was tested for polite conversation endings, gas-smell safety handling, and requests for human assistance.

The gas-smell response prioritized immediate safety and emergency assistance. For human requests, Sarah explained her transfer limitations and did not falsely confirm that a team member had been notified or a callback arranged.

**Evidence:** [Polite Conversation Ending](../../screenshots/Day%206/10d-day-6-polite-conversation-ending.png) · [Gas-Smell Safety Response](../../screenshots/Day%206/11-day-6-gas-smell-safety-response.png) · [Human Handoff Request](../../screenshots/Day%206/12-day-6-human-handoff-request.png) · [Human Callback Confirmation](../../screenshots/Day%206/13-day-6-human-callback-confirmation.png)

## Customer Value

Day 6 demonstrates business knowledge configuration, structured customer information collection, consistent pricing responses, service-area handling, emergency safety guidance, fee-consent rules, and honest communication about system capabilities.

The ElevenLabs text tests evaluate Sarah's conversational behavior. Actual service-request submission through ElevenLabs and n8n, including workflow execution and data recording, remains to be verified in Day 7.