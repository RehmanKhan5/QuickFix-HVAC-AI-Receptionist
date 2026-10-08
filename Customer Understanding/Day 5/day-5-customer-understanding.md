# Day 5 — Notifications, Validation & Error Handling

## Overview

Day 5 extends the QuickFix HVAC post-call automation with business notifications, SMS notification handling, payload validation, and controlled error handling.

The workflow is designed to ensure that complete service requests are recorded, business notifications are generated, and incomplete requests are identified before entering the successful processing path.

## Current Workflow

The Day 5 workflow follows this structure:

Webhook
↓
Edit Fields
↓
Validate Post-Call Payload
↓
IF
├── TRUE → Append row in sheet → Send Gmail Notification
│
└── FALSE → Prepare Validation Error

---

## Business Notifications

### Google Sheets

Valid post-call service requests are recorded in Google Sheets so that business staff have a structured record of incoming customer requests.

The workflow prepares the required customer and service information before the request is recorded.

**Evidence:** [Edit Fields Configuration](../../screenshots/Day%205/01-day-5-edit-fields.png) · [Edit Fields Test](../../screenshots/Day%205/02-day-5-edit-fields-test.png)

### Gmail Notification

A Gmail notification is generated for valid service requests.

The notification provides the business with important information about the new customer request and helps staff stay informed about incoming service requirements.

The Gmail notification workflow was configured and successfully tested.

**Evidence:** [Gmail Node Configuration](../../screenshots/Day%205/03-day-5-gmail-node.png) · [Gmail Message](../../screenshots/Day%205/04-day-5-gmail-message.png) · [Gmail Send Success](../../screenshots/Day%205/05-day-5-gmail-send-success.png) · [Received Gmail Notification](../../screenshots/Day%205/06-day-5-gmail-received-email.png)

### SMS Notification

The workflow also includes SMS notification handling for service-request alerts.

The SMS message contains key information about the customer request, including the customer name, service type, and request classification.

**Evidence:** [SMS Notification](../../screenshots/Day%205/07-day-5-sms-simulation.png)

---

## Post-Call Payload Validation

A dedicated **Validate Post-Call Payload** step checks whether all required information is available before the request continues through the successful processing path.

Required fields include:

* Call ID
* Date/time
* Customer name
* Phone
* Call summary
* Call outcome
* Request status
* Source

The validation step generates two important values:

`payloadValid`

and:

`missingFields`

For a complete request:

```json
{
  "payloadValid": true,
  "missingFields": []
}
```

For an incomplete request:

```json
{
  "payloadValid": false,
  "missingFields": ["phone"]
}
```

A valid payload was successfully processed with:

`payloadValid = true`

and:

`missingFields = []`

**Evidence:** [Valid Payload Validation](../../screenshots/Day%205/08-day-5-valid-payload-validation.png)

---

## Conditional Routing

An IF node uses the Boolean `payloadValid` value to determine how the request should be processed.

### Valid Request

When:

`payloadValid = true`

the request continues through the successful processing path:

Append row in sheet
↓
Send Gmail Notification

The TRUE route was successfully tested.

**Result: PASS**

**Evidence:** [Valid IF Routing](../../screenshots/Day%205/09-day-5-valid-if-routing.png)

### Invalid Request

When:

`payloadValid = false`

the request is routed to:

Prepare Validation Error

This prevents incomplete requests from being processed as successful service requests.

The FALSE route was successfully tested using a controlled incomplete request.

**Result: PASS**

**Evidence:** [Invalid IF Routing](../../screenshots/Day%205/10-day-5-invalid-if-routing.png)

---

## Error Handling

The **Prepare Validation Error** step creates a structured response when required information is missing.

Example:

```json
{
  "success": false,
  "message": "Post-call payload rejected: required information is missing.",
  "missingFields": ["phone"]
}
```

This provides a clear explanation of why the request could not continue through the normal processing path.

The workflow identifies the missing information and returns it through the `missingFields` value.

**Evidence:** [Validation Error Output](../../screenshots/Day%205/11-day-5-validation-error-output.png)

---

## Testing

### Valid Payload Test

A complete AC repair service request was processed with all required information.

Result:

`payloadValid = true`

The request followed the TRUE path toward Google Sheets and Gmail notification processing.

**Result: PASS**

**Evidence:** [Valid Payload Validation](../../screenshots/Day%205/08-day-5-valid-payload-validation.png) · [Valid IF Routing](../../screenshots/Day%205/09-day-5-valid-if-routing.png)

### Controlled Failure Test

An incomplete request was processed with a required phone field missing.

The validation system correctly identified the missing information.

Result:

`payloadValid = false`

`missingFields = ["phone"]`

The request followed the FALSE path and generated the structured validation error.

**Result: PASS**

**Evidence:** [Invalid IF Routing](../../screenshots/Day%205/10-day-5-invalid-if-routing.png) · [Validation Error Output](../../screenshots/Day%205/11-day-5-validation-error-output.png)

---

## Customer Value

The Day 5 automation demonstrates several important business capabilities:

* Structured post-call data processing
* Automated business notifications
* Google Sheets record keeping
* Gmail notification automation
* SMS notification handling
* Required-field validation
* Conditional workflow routing
* Controlled error handling
* Clear identification of missing information
* Separation of successful and incomplete requests

The result is a more reliable post-call automation process that helps ensure customer requests are properly recorded, communicated, validated, and handled according to their processing status.
