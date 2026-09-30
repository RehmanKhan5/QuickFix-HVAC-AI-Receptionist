# QuickFix HVAC — Day 2 Notes

## 1. Day 2 Overview

Day 2 continued the technical implementation of the QuickFix HVAC AI Voice Receptionist project.

The main purpose of Day 2 was to continue building the n8n service-request workflow after the initial webhook setup created on Day 1.

During Day 2, the incoming webhook data was connected to an **Edit Fields** node, cleaned and normalized using a **Code** node, validated using JavaScript validation logic, and then routed through an **IF** node according to whether the service request was valid or invalid.

Day 2 also included structured testing of the validation logic using valid and invalid service-request information.

The project is a portfolio prototype for learning and demonstration purposes.

It is not connected to a real HVAC company or real customers.

---

# 2. Project Name

**QuickFix HVAC — 24/7 AI Voice Receptionist & Service Request Automation**

### Fictional Company

QuickFix HVAC & Cooling

### Location

Austin, Texas, USA

### Project Type

Portfolio prototype / learning project

---

# 3. Day 2 Main Objective

The main objective of Day 2 was to transform the basic webhook receiver created during Day 1 into a more useful service-request processing workflow.

The workflow developed during Day 2 is:

```text
Test Webhook
      ↓
Edit Fields
      ↓
Code in JavaScript
      ↓
IF
   ↙     ↘
Valid   Invalid
```

The workflow is designed to:

* Receive service-request information.
* Extract the required fields.
* Prepare the data.
* Normalize the incoming values.
* Validate important information.
* Identify missing or invalid information.
* Determine whether the request is valid.
* Route valid and invalid requests separately.
* Prepare the workflow for later Google Sheets integration.
* Prepare the workflow for later connection with the AI voice agent.

---

# 4. Day 1 Items Continued During Day 2

Several items that were listed as **Not Yet Completed** in the Day 1 notes were completed or substantially implemented during Day 2.

These included:

* Postman testing.
* Confirmation of JSON reception in n8n.
* Edit Fields / data preparation.
* Data normalization.
* Validation logic.
* IF / routing logic.
* Valid-request testing.
* Invalid-request testing.
* Screenshot documentation.
* GitHub documentation and screenshot organization.

The remaining components will be implemented during the following development stages.

---

# 5. Postman Testing

Postman was used to send structured JSON data to the n8n webhook.

The basic testing flow became:

```text
Postman
   ↓
HTTP POST Request
   ↓
n8n Webhook
   ↓
Edit Fields
   ↓
Code
   ↓
Validation
```

The Postman request uses:

### Method

```text
POST
```

### Body

```text
raw
```

### Data Type

```text
JSON
```

### Content Type

```text
application/json
```

A sample request was used to test the workflow.

---

# 6. Important n8n Webhook Data Structure

One important technical lesson was learned during Postman testing.

When Postman sends JSON data to an n8n Webhook, the incoming request data is available under:

```text
$json.body
```

For example:

```text
$json.body.address
```

can be used to access the address.

The data should not automatically be assumed to exist directly at:

```text
$json.address
```

This distinction is important when mapping webhook data into later n8n nodes.

---

# 7. Sample Service Request

The following sample request was used during testing:

```json
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
```

This represents a normal HVAC service request.

The request contains the main information required by the workflow:

* Customer name.
* Phone number.
* Email.
* Service address.
* Service type.
* Description of the issue.
* Emergency status.
* Emergency-fee agreement.
* Preferred service time.

---

# 8. Edit Fields Node

An **Edit Fields** node was added after the Webhook.

The purpose of this node is to prepare and organize the incoming service-request information before it enters the validation logic.

The configured fields include:

```text
customerName
phone
email
address
serviceType
issue
emergency
feeAgreed
preferredTime
```

The basic workflow became:

```text
Test Webhook
      ↓
Edit Fields
```

This creates a cleaner and more controlled structure for the information used by the following nodes.

---

# 9. Why Edit Fields Is Important

The Webhook receives the complete HTTP request.

The Edit Fields node provides a controlled way of selecting and preparing the fields needed by the service-request workflow.

Instead of allowing unnecessary request information to flow through every stage, the workflow can work with the specific business fields required for processing.

This improves:

* Data organization.
* Readability.
* Workflow maintenance.
* Validation.
* Debugging.
* Future integration with Google Sheets.

---

# 10. Data Normalization

After the Edit Fields node, a Code node was added.

The incoming values were not always perfectly clean.

For example, some values appeared with unwanted newline characters:

```text
"\nJohn Smith"
```

or:

```text
"+15125550123\n"
```

Boolean values and other fields could also contain formatting differences.

The goal of normalization is to convert incoming information into consistent values before validation.

For example:

### Before normalization

```text
"\nJohn Smith"
"+15125550123\n"
"As soon as possible\n"
```

### After normalization

```text
"John Smith"
"+15125550123"
"As soon as possible"
```

Boolean values should also remain actual Boolean values:

```text
false
```

and:

```text
true
```

rather than incorrectly treating them as text.

---

# 11. Code Node

The Code node was configured to use:

```text
JavaScript
```

JavaScript was selected for the validation and normalization logic.

The Code node is used because it allows the workflow to perform custom data processing and business validation that would be difficult to express using only simple field mappings.

The workflow therefore became:

```text
Test Webhook
      ↓
Edit Fields
      ↓
Code in JavaScript
```

---

# 12. Validation Logic

After the incoming information was normalized, validation logic was implemented.

The purpose of validation is to determine whether a service request contains the required information and follows the basic business rules.

The validation process checks important information such as:

* Phone number.
* Service address.
* Service area.
* Emergency fee agreement when required.
* Required service-request fields.

The validation process produces information that can be used by the next routing stage.

---

# 13. Phone Validation

The workflow checks whether the submitted phone number is valid according to the defined validation rules.

A valid request produces:

```text
phoneValid: true
```

If the phone information is missing or does not satisfy the validation rules, the result can become:

```text
phoneValid: false
```

This allows the workflow to identify requests that require additional information or correction.

---

# 14. Service Area Validation

The QuickFix HVAC prototype has defined service areas.

The supported areas are:

```text
Austin
Round Rock
Pflugerville
Cedar Park
```

The validation logic checks the submitted address to determine whether it belongs to the supported service area.

The validation result can include:

```text
serviceAreaValid: true
```

and:

```text
serviceArea: "austin"
```

for a valid Austin request.

For an address outside the supported area, the service-area validation can fail.

---

# 15. Emergency Fee Validation

Emergency requests require additional business-rule handling.

The workflow checks the emergency status and the emergency-fee agreement.

For example:

```text
emergency: true
feeAgreed: true
```

can satisfy the emergency-fee requirement.

If an emergency request requires the fee agreement but the customer has not agreed to it, the validation should fail.

The validation result includes:

```text
emergencyFeeValid
```

This separates emergency business rules from ordinary service requests.

---

# 16. Required Field Validation

The workflow also checks whether required information exists.

Important fields include:

```text
customerName
phone
address
serviceType
issue
```

If required information is missing, the request should not be treated as a valid service request.

The validation logic can identify missing information using:

```text
missingFields
```

For example:

```text
missingFields: []
```

means no required fields are missing.

If the phone number is missing, the result can identify the phone field as missing.

---

# 17. Overall Validation Result

The validation process produces an overall result:

```text
isValid
```

For a valid service request:

```text
isValid: true
```

For an invalid service request:

```text
isValid: false
```

The validation output can contain information such as:

```text
phoneValid: true
serviceAreaValid: true
serviceArea: "austin"
emergencyFeeValid: true
isValid: true
missingFields: []
```

This provides the IF node with the information it needs to determine which branch should process the request.

---

# 18. Valid Request Example

A valid request can produce:

```text
phoneValid: true
serviceAreaValid: true
serviceArea: "austin"
emergencyFeeValid: true
isValid: true
missingFields: []
```

This means:

* The phone number passed validation.
* The address is within the supported service area.
* The service area was identified.
* Emergency-fee requirements were satisfied.
* No required fields are missing.
* The overall request is valid.

The request can therefore continue through the **Valid** branch.

---

# 19. Invalid Request Example

An invalid request can occur when required information is missing or when a business rule fails.

Examples include:

* Missing phone number.
* Missing service address.
* Missing issue description.
* Address outside the supported service area.
* Required emergency fee agreement not provided.
* Invalid customer information.

In these cases:

```text
isValid: false
```

The request should therefore be routed through the **Invalid** branch.

---

# 20. IF Node

An **IF** node was added after the validation Code node.

The purpose of the IF node is to separate valid and invalid service requests.

The workflow is:

```text
Test Webhook
      ↓
Edit Fields
      ↓
Code in JavaScript
      ↓
IF
   ↙     ↘
Valid   Invalid
```

The IF node uses the validation result to determine which branch should receive the request.

---

# 21. Valid Branch

If:

```text
isValid = true
```

the request follows the valid branch.

The valid branch is intended for service requests that contain the required information and satisfy the defined business rules.

The valid request can later continue to:

```text
Business Logic
      ↓
Google Sheets
      ↓
Respond to Webhook
```

The exact downstream workflow will continue to be developed.

---

# 22. Invalid Branch

If:

```text
isValid = false
```

the request follows the invalid branch.

The purpose of the invalid branch is to prevent incomplete or invalid service requests from being treated as successfully submitted.

The workflow can later return an appropriate response explaining that additional information or correction is required.

---

# 23. Switch Node Preparation

A Switch node is present in the planned workflow structure for additional business routing.

The Switch node can later be used to separate different valid request categories.

For example, service requests could eventually be routed according to:

```text
Routine
Emergency
Safety-related
Other
```

The exact routing logic will be implemented as the workflow develops.

---

# 24. Respond to Webhook

A **Respond to Webhook** node is included as part of the planned workflow.

Its purpose is to return the final processing result to the system that called the webhook.

The eventual flow will be:

```text
Request
   ↓
n8n Processing
   ↓
Validation
   ↓
Business Logic
   ↓
Response
```

The returned result can later be consumed by the AI voice agent.

The complete response structure will be finalized during the later workflow stages.

---

# 25. Testing Performed During Day 2

The validation workflow was tested using different request conditions.

The purpose was to verify that the validation logic correctly distinguishes valid requests from invalid requests.

Important validation tests included:

### Valid Request

All required information is present.

Expected result:

```text
Valid
```

### Missing Phone

Phone number is empty or missing.

Expected result:

```text
Invalid
```

### Missing Address

Address is empty or missing.

Expected result:

```text
Invalid
```

### Missing Issue

Issue description is empty or missing.

Expected result:

```text
Invalid
```

These tests help verify that the validation logic is actually controlling the workflow rather than simply passing every request through.

---

# 26. Structured Test Scenarios

The project sample-data collection was also expanded with structured HVAC receptionist scenarios.

The scenarios cover different situations, including:

* Routine AC repair.
* Emergency AC failure.
* Heating failure.
* Missing information.
* Customer outside the service area.
* Emergency fee declined.
* Suspected gas smell.
* Customer requesting a human.
* Tool failure.

These scenarios provide repeatable test data for future workflow and AI-agent testing.

---

# 27. Importance of Structured Test Data

Structured JSON scenarios make testing more consistent.

Instead of manually creating a different request every time, the same scenario can be tested repeatedly.

For example:

```text
missing_information.json
```

can be used whenever the missing-information workflow needs to be tested.

Similarly:

```text
outside_service_area.json
```

can be used to test service-area validation.

This makes debugging easier because the input remains consistent.

---

# 28. Day 2 Screenshot Documentation

Important Day 2 screenshots were captured and organized in the project.

The screenshot folder was reorganized by development day.

The structure is:

```text
screenshots/
├── Day 1/
└── Day 2/
```

Day 1 screenshots were moved into:

```text
screenshots/Day 1/
```

Day 2 screenshots were placed into:

```text
screenshots/Day 2/
```

---

# 29. Day 1 Screenshot Organization

The Day 1 screenshots are now stored as:

```text
screenshots/Day 1/
├── n8n-test-webhook.png
└── postman-test.png
```

These screenshots provide visual evidence of the early project development.

---

# 30. Day 2 Screenshot Organization

The Day 2 screenshots are stored as:

```text
screenshots/Day 2/
├── 00-workflow-overview.png
├── 01-edit-fields.png
├── 02-code-validation.png
├── 03-if-node.png
├── 04-valid-execution.png
└── 05-invalid-execution.png
```

The numbered naming system makes the screenshots easy to understand in development order.

---

# 31. Why Screenshots Are Important

The screenshots provide visual evidence of the development process.

They can be used to:

* Remember how the workflow was built.
* Review individual configuration steps.
* Troubleshoot problems later.
* Document project milestones.
* Demonstrate the development process.
* Support the GitHub portfolio.
* Explain the project during client discussions.

---

# 32. Git Organization

The screenshot organization was tracked using Git.

Initially, the Day 1 screenshots existed directly inside:

```text
screenshots/
```

They were then moved into:

```text
screenshots/Day 1/
```

The Day 2 screenshots were added into:

```text
screenshots/Day 2/
```

Git correctly detected the Day 1 files as renamed/moved files and detected the Day 2 screenshots as new files.

The changes were committed and pushed successfully.

---

# 33. Git Commit

The screenshot organization and Day 2 screenshots were committed with the message:

```text
Organize Day 1 and add Day 2 screenshots
```

The local Git status then showed:

```text
Your branch is ahead of 'origin/main' by 1 commit.
```

After pushing, Git reported:

```text
Everything up-to-date
```

This confirmed that the local repository and the GitHub repository were synchronized.

---

# 34. Current GitHub Screenshot Structure

The GitHub repository now contains the organized screenshot structure:

```text
QuickFix-HVAC-AI-Receptionist
└── screenshots
    ├── Day 1
    │   ├── n8n-test-webhook.png
    │   └── postman-test.png
    │
    └── Day 2
        ├── 00-workflow-overview.png
        ├── 01-edit-fields.png
        ├── 02-code-validation.png
        ├── 03-if-node.png
        ├── 04-valid-execution.png
        └── 05-invalid-execution.png
```

---

# 35. Important Technical Lessons Learned on Day 2

## Lesson 1 — Webhook data location matters

When using an n8n Webhook with Postman, incoming request information can be located under:

```text
$json.body
```

Understanding the structure of incoming data is important when connecting nodes together.

---

## Lesson 2 — Data should be normalized before validation

Raw incoming values may contain unwanted whitespace or formatting.

Cleaning the data before validation makes the validation logic more reliable.

The basic principle is:

```text
Raw Data
   ↓
Normalization
   ↓
Validation
   ↓
Routing
```

---

## Lesson 3 — Validation should happen before database writing

A request should be validated before it is written to the final business data storage.

The intended principle is:

```text
Receive Request
      ↓
Prepare Data
      ↓
Validate
      ↓
Business Logic
      ↓
Save Valid Request
```

This helps prevent incomplete or invalid information from being treated as a completed service request.

---

## Lesson 4 — IF nodes are useful for business decisions

The IF node allows the workflow to make a simple business decision:

```text
Is the request valid?
       ↓
   Yes / No
```

This creates separate processing paths for valid and invalid requests.

---

## Lesson 5 — Testing should include both successful and failed conditions

Testing only a successful request is not enough.

A reliable workflow should also test:

* Missing information.
* Invalid information.
* Unsupported service areas.
* Emergency business rules.
* Safety-related scenarios.
* Tool failures.

This helps reveal problems before the system is used in a complete voice workflow.

---

# 36. Day 2 Business Logic Principles

The same business rules established during Day 1 continue to apply.

The AI receptionist must not:

* Invent prices.
* Invent services.
* Invent appointment availability.
* Promise technician arrival times without confirmation.
* Claim that a booking is confirmed without actual confirmation.
* Claim that a request was successfully submitted before n8n confirms it.
* Provide professional HVAC diagnoses.
* Give unsafe repair instructions.
* Claim that a notification was successfully sent without workflow confirmation.
* Collect unnecessary personal information.

The n8n workflow should therefore provide reliable backend validation rather than trusting every incoming request.

---

# 37. Emergency and Safety Handling

Emergency and safety situations continue to require special handling.

Examples include:

```text
Gas smell
Fire
Smoke
Sparks
Electrical danger
Serious water leakage involving electrical equipment
Extreme heat or cold situations
```

The AI receptionist should follow the defined safety procedures.

The automation should not falsely report that a technician, emergency service, or other responder has been dispatched unless the system has actually confirmed that action.

---

# 38. Day 2 Current Workflow

At the end of the Day 2 implementation, the main workflow structure is:

```text
Customer / Test Request
        ↓
Test Webhook
        ↓
Edit Fields
        ↓
Code in JavaScript
        ↓
Validation
        ↓
IF
   ↙        ↘
Valid      Invalid
   ↓          ↓
Switch     Response
```

The workflow is now significantly more structured than the initial Day 1 webhook.

---

# 39. Day 2 Completion Status

## Completed

* Continued the QuickFix HVAC n8n workflow.
* Completed Postman webhook testing.
* Confirmed JSON reception in n8n.
* Identified the correct webhook data structure.
* Added Edit Fields node.
* Configured service-request fields.
* Added JavaScript Code node.
* Implemented data normalization.
* Implemented validation logic.
* Added phone validation.
* Added service-area validation.
* Defined supported service areas.
* Added emergency-fee validation.
* Added required-field validation.
* Added missing-field detection.
* Created overall `isValid` result.
* Added IF node.
* Created valid and invalid routing logic.
* Tested valid requests.
* Tested missing-phone requests.
* Tested missing-address requests.
* Tested missing-issue requests.
* Prepared Switch routing.
* Prepared Respond to Webhook.
* Expanded structured HVAC test scenarios.
* Captured Day 2 workflow screenshots.
* Organized screenshots into Day 1 and Day 2 folders.
* Corrected screenshot filenames.
* Committed screenshot changes to Git.
* Pushed the screenshot changes to GitHub.
* Confirmed GitHub synchronization.

---

# 40. Not Yet Completed

The following parts remain for later stages:

* Complete Google Sheets integration.
* Configure final service-request record structure.
* Configure final Respond to Webhook response.
* Create the ElevenLabs AI agent.
* Configure the `submit_service_request` tool.
* Connect the ElevenLabs tool to the n8n webhook.
* Configure post-call processing.
* Create Google Sheets call-history records.
* Configure Gmail notifications.
* Configure optional SMS notifications.
* Test the complete ElevenLabs text workflow.
* Perform browser voice testing.
* Perform telephone testing.
* Perform complete end-to-end testing.
* Complete final error-handling verification.
* Complete final safety testing.
* Prepare final GitHub portfolio documentation.
* Record the final project demonstration.

---

# 41. Day 2 Final Summary

Day 2 transformed the initial QuickFix HVAC webhook into a structured service-request processing workflow.

The incoming Postman JSON was successfully received by n8n and processed through an **Edit Fields** node.

A JavaScript Code node was then used to normalize the incoming data and apply validation rules.

The validation system checks important information including:

```text
Phone
Service Area
Required Fields
Emergency Fee Agreement
```

The workflow produces an overall:

```text
isValid
```

result.

An IF node then separates valid and invalid requests.

The project also gained structured test scenarios and improved screenshot documentation.

The Day 1 and Day 2 screenshots were organized into separate folders and successfully pushed to the GitHub repository.

The project has therefore progressed from:

```text
Basic Webhook
      ↓
Received JSON
```

to:

```text
Webhook
   ↓
Data Preparation
   ↓
Normalization
   ↓
Validation
   ↓
Valid / Invalid Routing
```

The next development stage will continue with the remaining business automation, including Google Sheets, webhook responses, and eventually the AI voice-agent integration.

**Day 2 Status: DATA PREPARATION, VALIDATION, ROUTING, TESTING AND DOCUMENTATION COMPLETE**
