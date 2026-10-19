# Day 8 — ElevenLabs Voice Experience & Service Request Integration

## Overview

Day 8 focuses on the voice experience of Sarah, the QuickFix HVAC AI receptionist, and verifying the connection between the conversational agent, the n8n automation workflow, and Google Sheets.

The voice interaction was demonstrated through an **ElevenLabs shareable conversation link**. During the successful routine service-request conversation, Sarah collected the customer's information, confirmed the details, submitted the request, and communicated the result.

QuickFix HVAC is a fictional portfolio demonstration project.

## ElevenLabs Voice Configuration

The ElevenLabs agent was configured with a selected voice and text-to-speech settings for the QuickFix HVAC receptionist experience. The opening greeting identifies Sarah as the AI receptionist for QuickFix HVAC & Cooling.

The browser-based greeting test provided an initial check of the agent's voice experience.

**Evidence:** [Current Voice Configuration](https://github.com/RehmanKhan5/QuickFix-HVAC-AI-Receptionist/blob/main/screenshots/Day%208/01-day-8-elevenlabs-current-voice.png) · [Browser Voice Greeting](https://github.com/RehmanKhan5/QuickFix-HVAC-AI-Receptionist/blob/main/screenshots/Day%208/02-day-8-browser-voice-greeting-test.png)

## Routine Service Request Integration

A routine AC repair request was submitted through Sarah using the ElevenLabs shareable conversation link. The customer provided a name, phone number, email address, service address, issue description, service type, and preferred service time.

Sarah repeated the details for confirmation before submitting the request. The conversation then returned a successful submission message.

The request was for an AC system blowing warm air and was classified as routine rather than an emergency.

**Evidence:** [Successful Voice-to-n8n Execution](https://github.com/RehmanKhan5/QuickFix-HVAC-AI-Receptionist/blob/main/screenshots/Day%208/03-day-8-voice-to-n8n-success.png)

## n8n Workflow Processing

The successful execution showed the service request entering the n8n workflow and proceeding through the data transformation, validation, routine-request routing, Google Sheets recording, and response stages.

The workflow execution completed successfully. This demonstrates the connection between the voice agent and the service-request automation workflow for the recorded routine request.

**Evidence:** [Successful Voice-to-n8n Execution](https://github.com/RehmanKhan5/QuickFix-HVAC-AI-Receptionist/blob/main/screenshots/Day%208/03-day-8-voice-to-n8n-success.png)

## Google Sheets Service Request Record

The routine service request was recorded in Google Sheets with its customer details, service information, emergency status, fee-consent field, preferred time, and request status.

The record showed `Emergency: FALSE`, `Fee Agreed: FALSE`, and a status of `New` with the request pending follow-up.

The response indicated that the request had been received for scheduling. It did not represent a confirmed appointment or a completed technician dispatch.

**Evidence:** [Routine Google Sheets Record — Part 1](https://github.com/RehmanKhan5/QuickFix-HVAC-AI-Receptionist/blob/main/screenshots/Day%208/04a-day-8-google-sheets-routine-record.png) · [Routine Google Sheets Record — Part 2](https://github.com/RehmanKhan5/QuickFix-HVAC-AI-Receptionist/blob/main/screenshots/Day%208/04b-day-8-google-sheets-routine-record.png) · [Routine Google Sheets Record — Part 3](https://github.com/RehmanKhan5/QuickFix-HVAC-AI-Receptionist/blob/main/screenshots/Day%208/04c-day-8-google-sheets-routine-record.png)

## Voice Conversation and Customer Confirmation

The completed voice conversation showed Sarah greeting the customer, collecting and confirming the service details, submitting the routine request, and communicating the successful result.

Sarah explained that the request had been received for scheduling and ended the conversation politely.

The conversation demonstrates a connected voice-to-automation experience for this routine scenario. The successful result was supported by the n8n execution and the corresponding Google Sheets record.

**Evidence:** [Voice Conversation — Part 1](https://github.com/RehmanKhan5/QuickFix-HVAC-AI-Receptionist/blob/main/screenshots/Day%208/05a-day-8-voice-conversation-success.png) · [Voice Conversation — Part 2](https://github.com/RehmanKhan5/QuickFix-HVAC-AI-Receptionist/blob/main/screenshots/Day%208/05b-day-8-voice-conversation-success.png) · [Voice Conversation — Part 3](https://github.com/RehmanKhan5/QuickFix-HVAC-AI-Receptionist/blob/main/screenshots/Day%208/05c-day-8-voice-conversation-success.png) · [Voice Conversation — Part 4](https://github.com/RehmanKhan5/QuickFix-HVAC-AI-Receptionist/blob/main/screenshots/Day%208/05d-day-8-voice-conversation-success.png) · [Voice Conversation — Part 5](https://github.com/RehmanKhan5/QuickFix-HVAC-AI-Receptionist/blob/main/screenshots/Day%208/05e-day-8-voice-conversation-success.png)

## Customer Value

Day 8 demonstrates how a conversational AI receptionist can collect and confirm HVAC service information, submit a routine request to an automation workflow, record the request in Google Sheets, and communicate the submission result to the customer.

The demonstrated process reduces the need to manually transfer routine request details between a conversation and a tracking sheet. The request remains pending follow-up rather than being represented as a confirmed appointment.

This is a portfolio prototype using fictional business information and demonstration policies. Production deployment would require business-owner approval, verified service and pricing policies, appropriate privacy safeguards, and operational validation.