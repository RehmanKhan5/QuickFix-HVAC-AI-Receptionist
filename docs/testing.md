# QuickFix HVAC — Testing Documentation

## 1. Purpose

This document explains how the QuickFix HVAC AI Voice Receptionist will be tested.

The purpose of testing is to make sure that the system can:

- Understand customer requests correctly.
- Collect the required customer information.
- Identify emergency situations.
- Follow the correct business rules.
- Validate incoming data.
- Save valid service requests to Google Sheets.
- Return the correct result to the ElevenLabs AI agent.
- Handle invalid or incomplete information safely.
- Handle workflow and integration failures.
- Create post-call records correctly.
- Send the required notifications.
- Avoid making false promises to customers.

This is a portfolio prototype for learning and demonstration purposes.

It is not connected to a real HVAC company or real customers.

## 2. Testing Philosophy

Testing will be performed gradually instead of immediately making real phone calls.

The testing sequence is:

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

Each stage should work correctly before moving to the next stage.

This approach reduces unnecessary API usage, phone charges, debugging difficulty, and repeated testing.

## 3. Main Testing Areas

The project will be tested in the following areas:

1. Normal service requests
2. Emergency service requests
3. Missing customer information
4. Invalid information
5. Outside service area
6. Fee declined
7. Safety-related situations
8. Human handoff requests
9. Tool or webhook failure
10. Google Sheets recording
11. Post-call processing
12. Gmail notification
13. Optional SMS notification
14. Conversation context continuity
15. Final voice-call behavior


## 4. Test Environment

The project will initially be tested in a controlled development environment.

The main testing tools are:

- n8n Cloud for the main automation workflow.
- ElevenLabs Conversational AI for the AI voice agent.
- Twilio for telephone testing.
- Google Sheets for service request and call-history records.
- Gmail for email notification testing.
- Postman for webhook/API testing.
- Sample JSON files for repeatable test cases.
- GitHub for storing project files and workflow backups.

The development process will begin with non-voice testing.

Real telephone testing will be performed only after the n8n workflow, ElevenLabs agent, and webhook tool are working correctly.

## 5. Testing Order

Testing will follow this order:

### Stage 1 — Sample JSON Testing

Use prepared JSON files to simulate customer requests.

Example:

```json
{
  "clientName": "John Smith",
  "phone": "+15125550123",
  "email": "john@example.com",
  "address": "123 Main Street, Austin, TX",
  "serviceType": "AC Repair",
  "issue": "The AC is blowing warm air.",
  "emergency": false,
  "feeAgreed": true,
  "preferredTime": "Tomorrow morning"
}


The purpose is to verify that the expected data can enter the workflow.

Stage 2 — Postman Testing

Send test requests from Postman to the n8n webhook.

Check:

HTTP request is received.
JSON data is received correctly.
Fields are mapped correctly.
Validation works.
Invalid data is rejected.
The correct response is returned.
Stage 3 — n8n Workflow Testing

Run the complete n8n workflow.

Verify:

Webhook receives the request.
Edit Fields normalizes the data.
Code validation checks required fields.
IF node handles validation results.
Switch node routes the request correctly.
Google Sheets receives valid requests.
Respond to Webhook returns the correct result.
Stage 4 — ElevenLabs Text Testing

Test the AI agent without immediately using a real telephone call.

Verify:

Greeting is correct.
Agent understands the customer request.
Agent asks for required information.
Agent follows the safety rules.
Agent uses the service request tool correctly.
Agent handles the tool response correctly.
Agent does not claim success before receiving confirmation.
Stage 5 — ElevenLabs Browser Voice Testing

Test the agent using a browser microphone.

Check:

Speech recognition.
Voice response.
Conversation flow.
Interruptions.
Customer information collection.
Tool execution.
Response timing.
End-of-call behavior.
Stage 6 — Twilio Telephone Testing

Only after the previous stages work correctly, test the system through a real telephone call.

Check:

Customer calls the Twilio number.
Call reaches the ElevenLabs agent.
Agent greets the customer.
Customer explains the problem.
Agent collects the required information.
Agent calls the service-request tool.
n8n processes the request.
Google Sheets records the request.
The result returns to the agent.
Agent gives the correct response.
Post-call workflow runs correctly.


## 6. Test Case Format

Each test will be documented using a consistent format.

This makes it easier to understand:

* What was tested.
* What information was provided.
* What the system was expected to do.
* What actually happened.
* Whether the test passed or failed.

Each test case should contain the following information:

### Test Case ID

A unique identification number for the test.

Example:

`TC-001`

### Test Scenario

A short description of what is being tested.

Example:

`Customer requests a normal AC repair.`

### Test Input

The information provided to the AI agent or n8n webhook.

This may include:

* Customer name
* Phone number
* Email
* Address
* Service type
* Issue
* Emergency status
* Fee agreement
* Preferred time

### Expected Result

The behavior that should occur if the system is working correctly.

Example:

`The request is validated and saved to Google Sheets with the correct status.`

### Actual Result

The behavior that actually occurred during testing.

This will be written after the test has been performed.

Example:

`Request was saved correctly and the expected response was returned.`

### Test Status

Each test will have one of the following statuses:

* PASS — The system behaved as expected.
* FAIL — The system did not behave as expected.
* BLOCKED — The test could not be completed because another component was not ready.
* NOT TESTED — The test has not yet been performed.

### Notes

Additional information about the test.

For example:

* Error message received.
* Response was slow.
* Data was missing.
* Google Sheets record was incorrect.
* Agent asked an unnecessary question.
* Tool failed.
* Test needs to be repeated.

This format will be used throughout the QuickFix HVAC testing process.



## 7. Normal Service Request Test Cases

### TC-001 — Normal AC Repair Request

**Test Scenario:**

A customer calls QuickFix HVAC because their air conditioner is not working properly.

**Test Input:**

* Customer Name: John Smith
* Phone: +15125550123
* Email: [john@example.com](mailto:john@example.com)
* Address: 123 Main Street, Austin, TX
* Service Type: AC Repair
* Issue: AC is blowing warm air.
* Emergency: No
* Fee Agreed: Yes
* Preferred Time: Tomorrow morning

**Expected Result:**

* The AI agent understands that the customer needs AC repair.
* The required customer information is collected.
* The request is identified as a routine service request.
* The information is sent to the `submit_service_request` tool.
* n8n receives the request.
* The data passes validation.
* The request is saved to Google Sheets.
* The correct result is returned to ElevenLabs.
* The AI agent tells the customer that the service request was successfully submitted.
* The customer is not given an unsupported confirmed appointment time.

**Test Status:**

NOT TESTED

**Notes:**

To be completed after the test is performed.

---

### TC-002 — HVAC Maintenance Request

**Test Scenario:**

A customer wants to schedule routine HVAC maintenance.

**Test Input:**

* Customer Name: Sarah Johnson
* Phone: +15125550124
* Email: [sarah@example.com](mailto:sarah@example.com)
* Address: 456 Oak Street, Austin, TX
* Service Type: HVAC Maintenance
* Issue: Customer wants routine maintenance and a system check.
* Emergency: No
* Fee Agreed: Yes
* Preferred Time: Friday afternoon

**Expected Result:**

* The AI agent identifies the request as routine maintenance.
* The required information is collected.
* The service request tool is called with the correct information.
* n8n validates the request.
* Google Sheets receives one service request record.
* The request status is appropriate for a request that has been submitted but not actually booked.
* The AI agent does not claim that the appointment is confirmed unless an actual booking system confirms it.

**Test Status:**

NOT TESTED

**Notes:**

To be completed after the test is performed.

---

### TC-003 — Heating Repair Request

**Test Scenario:**

A customer reports that their heating system is not working.

**Test Input:**

* Customer Name: Michael Brown
* Phone: +15125550125
* Email: [michael@example.com](mailto:michael@example.com)
* Address: 789 Pine Street, Round Rock, TX
* Service Type: Heating Repair
* Issue: Furnace is not turning on.
* Emergency: No
* Fee Agreed: Yes
* Preferred Time: Monday morning

**Expected Result:**

* The AI agent identifies the request as heating repair.
* The agent collects the required customer information.
* The request is sent to the service-request tool.
* n8n validates the information.
* The request is successfully recorded in Google Sheets.
* The correct tool response is returned to the AI agent.
* The agent provides a truthful response without promising a technician arrival time.

**Test Status:**

NOT TESTED

**Notes:**

To be completed after the test is performed.

---

### TC-004 — Customer Requests a Quote

**Test Scenario:**

A customer wants information about the cost of an HVAC service.

**Test Input:**

* Customer Name: David Wilson
* Phone: +15125550126
* Email: [david@example.com](mailto:david@example.com)
* Address: 321 Cedar Avenue, Cedar Park, TX
* Service Type: AC Repair
* Issue: Customer wants to know the cost of diagnosing an AC problem.
* Emergency: No
* Fee Agreed: Yes
* Preferred Time: Not specified

**Expected Result:**

* The AI agent provides only the approved fictional demonstration pricing information.
* The agent does not invent additional prices.
* If a service request is submitted, the information is validated before being saved.
* The customer is not given a guaranteed final repair price because the AI agent cannot professionally diagnose the problem or determine the final repair cost.

**Test Status:**

NOT TESTED

**Notes:**

To be completed after the test is performed.

---

### TC-005 — Service Request With Missing Information

**Test Scenario:**

A customer wants to request AC repair but does not provide all required information.

**Test Input:**

* Customer Name: Emily Davis
* Phone: Not provided
* Email: Not provided
* Address: 555 Maple Street, Austin, TX
* Service Type: AC Repair
* Issue: AC is not cooling.
* Emergency: No
* Fee Agreed: Yes
* Preferred Time: Tomorrow

**Expected Result:**

* The AI agent identifies the missing required information.
* The agent asks the customer for the missing information.
* The request is not submitted with incomplete required data.
* n8n validation prevents an incomplete request from being treated as valid.
* Google Sheets does not receive an incorrectly completed service request.
* The agent explains what information is still needed in a clear and polite way.

**Test Status:**

NOT TESTED

**Notes:**

To be completed after the test is performed.


## 8. Emergency and Safety Test Cases

### TC-006 — Emergency AC Failure

**Test Scenario:**

A customer reports that their AC has completely stopped working during very hot weather.

**Test Input:**

* Customer Name: Robert Miller
* Phone: +15125550127
* Email: [robert@example.com](mailto:robert@example.com)
* Address: 100 Congress Avenue, Austin, TX
* Service Type: AC Repair
* Issue: AC has stopped working and the house is becoming extremely hot.
* Emergency: Yes
* Fee Agreed: Yes
* Preferred Time: As soon as possible

**Expected Result:**

* The AI agent recognizes that the situation may be urgent.
* The agent does not diagnose the HVAC system professionally.
* The agent explains the applicable fictional emergency dispatch fee when appropriate.
* The agent obtains agreement to the fee before submitting the emergency request.
* The agent collects the required customer information.
* The request is submitted through the service-request tool.
* n8n validates the request.
* Google Sheets records the emergency request.
* The agent does not promise a specific technician arrival time unless an actual system confirms it.
* The agent provides a truthful response based on the tool result.

**Test Status:**

NOT TESTED

**Notes:**

To be completed after the test is performed.

---

### TC-007 — Suspected Gas Smell

**Test Scenario:**

A customer reports smelling gas near their heating system.

**Test Input:**

* Customer Name: James Anderson
* Phone: +15125550128
* Address: 200 Elm Street, Austin, TX
* Service Type: Heating Repair
* Issue: Customer reports a suspected gas smell.
* Emergency: Yes

**Expected Result:**

* The AI agent treats the situation as a safety emergency.
* The agent tells the customer to move away from the suspected danger.
* The agent does not provide DIY instructions for investigating or repairing the gas system.
* The agent does not tell the customer to operate electrical switches near the suspected gas leak.
* The agent directs the customer toward appropriate emergency or gas-utility assistance according to the situation.
* The agent does not continue normal HVAC troubleshooting when an immediate safety risk is reported.
* The agent does not falsely claim that QuickFix HVAC has dispatched a technician unless that action is actually confirmed.

**Test Status:**

NOT TESTED

**Notes:**

To be completed after the test is performed.

---

### TC-008 — Fire, Smoke, Sparks, or Electrical Danger

**Test Scenario:**

A customer reports smoke or sparks coming from an HVAC system.

**Test Input:**

* Customer Name: Linda Taylor
* Phone: +15125550129
* Address: 300 Walnut Street, Austin, TX
* Service Type: AC Repair
* Issue: Customer reports smoke and sparks coming from the HVAC equipment.
* Emergency: Yes

**Expected Result:**

* The AI agent recognizes the situation as a potential immediate safety hazard.
* The agent does not provide repair instructions.
* The agent does not ask the customer to open or investigate the equipment.
* The agent advises the customer to move away from the danger.
* The agent directs the customer toward appropriate emergency assistance when necessary.
* The agent does not claim that a technician has been dispatched unless the system confirms it.
* The conversation follows the emergency safety path rather than the normal service-request path.

**Test Status:**

NOT TESTED

**Notes:**

To be completed after the test is performed.

---

### TC-009 — Indoor AC Water Leak

**Test Scenario:**

A customer reports water leaking from an indoor AC unit.

**Test Input:**

* Customer Name: Daniel Thomas
* Phone: +15125550130
* Address: 400 Lakeview Drive, Pflugerville, TX
* Service Type: AC Repair
* Issue: Water is leaking from the indoor AC unit.
* Emergency: No
* Fee Agreed: Yes
* Preferred Time: Today afternoon

**Expected Result:**

* The AI agent recognizes the issue as a possible HVAC service problem.
* The agent avoids giving unsafe electrical instructions.
* The agent advises the customer to avoid electrical hazards around water.
* The agent collects the required information.
* The request is submitted through the service-request tool when appropriate.
* n8n validates the request.
* Google Sheets records the request if valid.
* The agent does not claim that the issue has been professionally diagnosed.

**Test Status:**

NOT TESTED

**Notes:**

To be completed after the test is performed.

---

### TC-010 — Emergency Fee Declined

**Test Scenario:**

A customer requests emergency service but does not agree to the applicable fictional emergency dispatch fee.

**Test Input:**

* Customer Name: William Harris
* Phone: +15125550131
* Address: 500 Main Street, Austin, TX
* Service Type: AC Repair
* Issue: AC stopped working.
* Emergency: Yes
* Fee Agreed: No
* Preferred Time: As soon as possible

**Expected Result:**

* The AI agent explains the applicable fictional emergency dispatch fee clearly.
* The customer is allowed to decline.
* The service request is not submitted as an approved emergency request when fee agreement is required.
* The agent does not pretend that emergency dispatch has been arranged.
* The agent provides an appropriate next step based on the business rules.
* No false success message is given.

**Test Status:**

NOT TESTED

**Notes:**

To be completed after the test is performed.

## 9. Edge Case and Failure Test Cases

### TC-011 — Customer Outside Service Area

**Test Scenario:**

A customer requests HVAC service but their address is outside the QuickFix HVAC service area.

**Test Input:**

* Customer Name: Christopher Moore
* Phone: +15125550132
* Email: [christopher@example.com](mailto:christopher@example.com)
* Address: 1500 West Avenue, San Antonio, TX
* Service Type: AC Repair
* Issue: AC is not cooling.
* Emergency: No
* Fee Agreed: Yes
* Preferred Time: Tomorrow

**Expected Result:**

* The AI agent identifies that the customer's address is outside the supported service area.
* The agent does not submit the request as a normal service request.
* The agent does not pretend that QuickFix HVAC will send a technician.
* The agent politely explains that the requested address is outside the current service area.
* No incorrect service request is written to Google Sheets.
* The conversation ends or continues according to the defined fallback behavior.

**Test Status:**

NOT TESTED

**Notes:**

To be completed after the test is performed.

---

### TC-012 — Customer Requests a Human

**Test Scenario:**

The customer does not want to continue with the AI receptionist and asks to speak with a human.

**Test Input:**

* Customer Name: Jennifer Wilson
* Phone: +15125550133
* Address: 600 6th Street, Austin, TX
* Service Type: AC Repair
* Issue: Customer wants to discuss an AC problem with a human representative.
* Emergency: No
* Preferred Time: Not specified

**Expected Result:**

* The AI agent recognizes the request for human assistance.
* The agent does not argue with the customer or repeatedly continue the automated conversation.
* The agent follows the defined human-handoff or callback process.
* If no live transfer system exists in the prototype, the agent clearly explains the available fallback.
* The agent does not falsely claim that a human representative has been connected.
* Any service request or callback information is recorded only when the required information and workflow allow it.

**Test Status:**

NOT TESTED

**Notes:**

To be completed after the test is performed.

---

### TC-013 — Invalid Customer Information

**Test Scenario:**

A customer provides information that is invalid or incorrectly formatted.

**Test Input:**

* Customer Name: Test Customer
* Phone: `abc123`
* Email: `not-an-email`
* Address: Austin
* Service Type: AC Repair
* Issue: AC is not cooling.
* Emergency: No
* Fee Agreed: Yes
* Preferred Time: Tomorrow morning

**Expected Result:**

* n8n receives the request.
* The Code validation node checks the information.
* Invalid information is detected.
* The request is not treated as a valid service request.
* The request is not incorrectly written to Google Sheets as a valid record.
* The workflow returns an appropriate error response.
* The AI agent does not tell the customer that the request was successfully submitted.
* The customer is asked for corrected information when appropriate.

**Test Status:**

NOT TESTED

**Notes:**

To be completed after the test is performed.

---

### TC-014 — Service Request Tool Failure

**Test Scenario:**

The ElevenLabs agent attempts to submit a service request, but the n8n webhook or service-request workflow is unavailable.

**Test Input:**

* Customer Name: Thomas Martin
* Phone: +15125550134
* Email: [thomas@example.com](mailto:thomas@example.com)
* Address: 700 Red River Street, Austin, TX
* Service Type: AC Repair
* Issue: AC is blowing warm air.
* Emergency: No
* Fee Agreed: Yes
* Preferred Time: Tomorrow afternoon

**Expected Result:**

* The AI agent attempts to use the `submit_service_request` tool.
* The webhook or workflow failure is detected.
* The agent does not claim that the request was successfully submitted.
* The customer receives a polite and truthful fallback response.
* The workflow records the failure when the error-handling design allows it.
* No incomplete or false service request is marked as successfully submitted.
* The failure can be identified during troubleshooting.

**Test Status:**

NOT TESTED

**Notes:**

To be completed after the test is performed.


## 10. Automation and Integration Test Cases

### TC-015 — Google Sheets Service Request Record

**Test Scenario:**

Verify that a valid service request is correctly recorded in the Google Sheets `Service Requests` sheet.

**Test Input:**

Use a valid request such as TC-001.

**Expected Result:**

* n8n successfully processes the request.
* One new row is created in the `Service Requests` sheet.
* The following information is mapped to the correct columns:

  * Request ID
  * Date/Time
  * Customer Name
  * Phone
  * Email
  * Address
  * Service Area
  * Service Type
  * Issue
  * Emergency
  * Fee Agreed
  * Preferred Time
  * Status
  * Notification Status
  * Source
  * Notes
* No important customer information is placed in the wrong column.
* The request is not duplicated.
* The status accurately represents the current state of the request.

**Test Status:**

NOT TESTED

**Notes:**

To be completed after the test is performed.

---

### TC-016 — Google Sheets Call History Record

**Test Scenario:**

Verify that a completed AI call creates the correct record in the `Call History` sheet.

**Test Input:**

Complete a test conversation using ElevenLabs.

**Expected Result:**

* The post-call webhook is received by n8n.
* The call information is processed correctly.
* One new row is created in the `Call History` sheet.
* The record contains:

  * Call ID
  * Date/Time
  * Customer Name
  * Phone
  * Call Summary
  * Call Outcome
  * Request Status
  * Source
* The call record is associated with the correct customer/request information.
* The record is not unnecessarily duplicated.

**Test Status:**

NOT TESTED

**Notes:**

To be completed after the test is performed.

---

### TC-017 — Gmail Notification

**Test Scenario:**

Verify that a valid service request generates the required Gmail notification.

**Test Input:**

Use a valid service request such as TC-001.

**Expected Result:**

* The post-call or notification workflow processes the request.
* Gmail receives the notification.
* The email subject follows the defined format:

`QuickFix HVAC — New AI Call Summary`

* The email contains the relevant information, such as:

  * Customer name
  * Phone
  * Service type
  * Issue
  * Emergency status
  * Request status
  * Call summary
  * Call ID
* The notification does not contain API keys, passwords, or other secret credentials.
* The notification status is updated appropriately when the workflow supports this.

**Test Status:**

NOT TESTED

**Notes:**

To be completed after the test is performed.

---

### TC-018 — Optional SMS Notification

**Test Scenario:**

Verify the optional SMS notification workflow if SMS has been included in the prototype.

**Test Input:**

Use a valid service request such as TC-001.

**Expected Result:**

* The notification workflow processes the request.
* The SMS is sent only when the SMS integration is enabled and configured.
* The message contains the important request information.
* Example message:

`QuickFix HVAC Alert: New service request from John Smith. AC Repair — Emergency. Check Google Sheets for details.`

* The SMS does not claim that an appointment has been confirmed unless an actual booking system confirms it.
* If SMS is not enabled in the prototype, the test is marked `NOT TESTED` rather than treated as a failure.

**Test Status:**

NOT TESTED

**Notes:**

To be completed after the test is performed.

---

### TC-019 — Conversation Context Continuity

**Test Scenario:**

Verify that the AI agent remembers information provided earlier in the same conversation.

**Test Input:**

The customer provides information gradually.

Example:

1. Customer first gives their name.
2. Customer then explains the HVAC problem.
3. Customer later provides their address.
4. Customer later provides their preferred time.
5. Customer asks the agent to repeat or confirm the information.

**Expected Result:**

* The AI agent maintains the information from the same conversation.
* The customer does not have to repeatedly provide the same information unnecessarily.
* The agent uses the previously provided information when completing the service request.
* The final information sent to the `submit_service_request` tool is consistent with the conversation.
* The agent confirms important information before submission.
* The system does not write to Google Sheets on every conversation turn.
* The service request is written when the required information has been collected and the request is ready to be submitted.

**Test Status:**

NOT TESTED

**Notes:**

To be completed after the test is performed.

## 11. Final Acceptance Criteria

The QuickFix HVAC AI Voice Receptionist will be considered ready for portfolio demonstration when the main workflows have been tested successfully.

The system should be able to:

* Receive a customer request through the AI voice agent.
* Understand the customer's HVAC service requirement.
* Collect the required customer information.
* Identify routine and emergency requests correctly.
* Recognize important safety situations.
* Respect the defined service area.
* Explain applicable fictional demonstration fees when required.
* Obtain fee agreement when required.
* Use the `submit_service_request` tool correctly.
* Send valid information to the n8n webhook.
* Validate incoming information.
* Reject invalid or incomplete requests appropriately.
* Route requests through the correct n8n branch.
* Save valid service requests to Google Sheets.
* Return the correct result from n8n to the AI agent.
* Prevent the AI agent from claiming success before the workflow confirms success.
* Create the appropriate post-call record.
* Send the Gmail notification correctly.
* Handle optional SMS notification when enabled.
* Maintain conversation context during the same call.
* Handle tool or webhook failures safely.
* Avoid making unsupported appointment, technician-arrival, payment, or dispatch claims.

## 12. Final Testing Checklist

Before presenting the project as a portfolio demonstration, verify the following checklist.

### AI Agent

* [ ] Greeting is correct.
* [ ] Agent identity is correct.
* [ ] Agent understands common HVAC requests.
* [ ] Agent asks appropriate questions.
* [ ] Agent collects required information.
* [ ] Agent maintains conversation context.
* [ ] Agent follows safety rules.
* [ ] Agent does not provide unsupported professional diagnoses.
* [ ] Agent does not make false promises.

### n8n Workflow

* [ ] Webhook receives requests.
* [ ] Data is normalized correctly.
* [ ] Validation works correctly.
* [ ] Invalid requests are handled safely.
* [ ] IF node works correctly.
* [ ] Switch node routes requests correctly.
* [ ] Google Sheets receives valid requests.
* [ ] Respond to Webhook returns the correct result.
* [ ] Workflow handles errors appropriately.

### Google Sheets

* [ ] Service Requests sheet contains the correct columns.
* [ ] Valid requests create the correct record.
* [ ] Customer information is mapped correctly.
* [ ] Status is correct.
* [ ] Notification Status is correct.
* [ ] Call History records are created correctly.
* [ ] Duplicate records are avoided where applicable.

### Gmail

* [ ] Notification email is received.
* [ ] Subject is correct.
* [ ] Customer information is correct.
* [ ] Service information is correct.
* [ ] Emergency status is correct.
* [ ] Request status is correct.
* [ ] Call summary is included.
* [ ] No secrets or API keys are exposed.

### ElevenLabs

* [ ] Agent receives the correct first message.
* [ ] Agent can use the service-request tool.
* [ ] Tool parameters are mapped correctly.
* [ ] Tool result is handled correctly.
* [ ] Agent does not claim success before receiving confirmation.
* [ ] Browser voice testing works correctly.
* [ ] Response timing is acceptable.
* [ ] Call termination works correctly.

### Twilio

* [ ] Telephone call reaches the AI agent.
* [ ] Audio quality is acceptable.
* [ ] Customer speech is recognized correctly.
* [ ] Agent voice response works correctly.
* [ ] Service-request tool works during the call.
* [ ] n8n processes the request.
* [ ] Google Sheets receives the request.
* [ ] Post-call processing works.
* [ ] Gmail notification is generated.

## 13. Testing Completion Rule

A test should not be marked as `PASS` simply because the conversation sounded correct.

A test is considered successful only when the complete expected behavior has been verified.

For example, if a customer asks for AC repair:

Customer conversation
↓
Information collected
↓
Service request submitted
↓
n8n receives request
↓
Validation succeeds
↓
Google Sheets record created
↓
Correct response returned
↓
AI agent gives truthful response
↓
Post-call record created
↓
Gmail notification received

The complete chain should be verified where applicable.

If one important component fails, the test should be marked `FAIL`, `BLOCKED`, or `NOT TESTED` according to the actual situation.

## 14. Testing Record

After each real test is performed, update the corresponding test case.

Replace:

`NOT TESTED`

with:

`PASS`

or:

`FAIL`

or:

`BLOCKED`

and add the actual result and relevant notes.

Example:

**Actual Result:**

The request was successfully received by n8n, validated, written to Google Sheets, and the correct response was returned to the ElevenLabs agent.

**Test Status:**

PASS

**Notes:**

No issues observed during testing.

## 15. Final Principle

Testing is not only about checking whether the AI can talk.

The main purpose of this project is to demonstrate that the AI receptionist can:

**Understand → Collect → Validate → Execute → Record → Notify → Respond**

The voice conversation is only one part of the system.

The automation behind the conversation is what demonstrates the practical business value of the project.


