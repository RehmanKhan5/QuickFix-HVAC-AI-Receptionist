# Day 10 — Post-Call Recording and Notification

## Overview

Day 10 focused on the QuickFix HVAC AI receptionist's post-call recording workflow. The objective was to receive a call-summary payload, prepare and validate its information, record the accepted call summary in Google Sheets, and send an email notification through Gmail.

QuickFix HVAC & Cooling is a fictional business used for this portfolio demonstration.

## Post-Call Recording Workflow

The n8n post-call workflow receives information through a webhook and prepares the incoming fields before validating the payload. Valid information continues through the configured workflow to the recording and notification steps.

This workflow supports post-call documentation. It is separate from the customer-facing service-request workflow, and each workflow must be evaluated using its own execution results.

**Evidence — Post-call workflow:**

[![Day 10 — Post-call workflow success](../../screenshots/Day%2010/01-day-10-post-call-workflow-success.png)](../../screenshots/Day%2010/01-day-10-post-call-workflow-success.png)

[Open the post-call workflow screenshot](../../screenshots/Day%2010/01-day-10-post-call-workflow-success.png)

## Call-History Record in Google Sheets

The post-call workflow was tested with call-summary information, and the resulting call-history record was checked in the configured Google Sheets destination. Two screenshots provide complementary views of the saved record.

The record provides evidence that the tested payload reached the spreadsheet-recording stage. It does not independently prove that every live voice conversation automatically submits a service request through the separate service-request workflow.

**Evidence — Call-history record:**

[![Day 10 — Call-history record, Part A](../../screenshots/Day%2010/02a-day-10-call-history-record.png)](../../screenshots/Day%2010/02a-day-10-call-history-record.png)

[Open call-history record — Part A](../../screenshots/Day%2010/02a-day-10-call-history-record.png)

[![Day 10 — Call-history record, Part B](../../screenshots/Day%2010/02b-day-10-call-history-record.png)](../../screenshots/Day%2010/02b-day-10-call-history-record.png)

[Open call-history record — Part B](../../screenshots/Day%2010/02b-day-10-call-history-record.png)

## Gmail Notification

The workflow includes a Gmail notification step for the configured successful processing path. This provides an additional way to review a processed call summary.

The notification screenshot documents the email evidence associated with the tested workflow.

**Evidence — Gmail notification:**

[![Day 10 — Gmail notification](../../screenshots/Day%2010/03-day-10-gmail-notification.png)](../../screenshots/Day%2010/03-day-10-gmail-notification.png)

[Open the Gmail notification screenshot](../../screenshots/Day%2010/03-day-10-gmail-notification.png)

## Workflow Capabilities

The Day 10 work demonstrates the following capabilities in the tested post-call recording path:

- Receiving a post-call payload through an n8n webhook.
- Preparing and validating incoming information.
- Recording the tested call-history information in Google Sheets.
- Sending a Gmail notification through the configured workflow path.
- Maintaining visual evidence of the workflow, saved record, and email notification.

## Customer Value

For a home-service business, post-call recording can help maintain a reviewable history of customer conversations and provide an email alert when a call summary has been processed. This can support follow-up and reduce manual copying of call information.

The project remains a portfolio prototype using a fictional business and demonstration data. It is not a live HVAC dispatch system.

## Accuracy and Safety Limitations

A successful post-call workflow test does not establish that the entire live voice-to-service-request process is working end to end.

Sarah must rely on actual tool and workflow results. She must not claim that a service request was recorded, an appointment was confirmed, a technician was dispatched, or a real employee was notified unless the connected system provides confirmation of that specific action.

A call-history record is not, by itself, an appointment confirmation or proof of technician dispatch.

## Day 10 Completion Summary

Day 10 documented the post-call recording workflow, the resulting call-history record in two complementary views, and the Gmail notification evidence.

The notes distinguish the tested post-call recording path from the separate live voice-to-service-request integration, whose end-to-end success must be verified independently.

**Project limitation:** This portfolio demonstration uses a fictional HVAC business. Recorded call summaries do not independently confirm appointments or technician dispatch.