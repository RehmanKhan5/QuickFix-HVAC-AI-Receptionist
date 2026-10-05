# Day 2 — Customer Information Processing & Validation

## What We Want to Do

We want the QuickFix HVAC system to take the customer information received from the webhook, organize it into a consistent format, and check whether the information is suitable for processing.

This helps prevent incomplete or invalid service requests from continuing through the automation.

## What We Are Going to Do

* Organize the customer information received from the webhook.
* Create a consistent structure for the service request data.
* Validate important customer information.
* Check whether the customer's address is within the QuickFix HVAC service area.
* Check emergency-service requirements.
* Create a clear valid or invalid result.
* Identify any required information that is missing.

## What We Have Performed

* Created the initial workflow structure for processing incoming customer service requests.

**Evidence:** [View the Day 2 workflow overview](../../screenshots/Day%202/00-workflow-overview.png)

* Added an **Edit Fields** step to organize the information received from the webhook into clearly defined customer and service-request fields.

**Evidence:** [View the Edit Fields configuration](../../screenshots/Day%202/01-edit-fields.png)

* Added a validation step that checks important information such as the customer's phone number, service area, and emergency-service requirements.

**Evidence:** [View the validation configuration](../../screenshots/Day%202/02-code-validation.png)

* Added an **IF** step to separate valid service requests from requests that require correction or additional information.

**Evidence:** [View the IF validation step](../../screenshots/Day%202/03-if-node.png)

* Tested a complete and valid customer service request and confirmed that it passed the validation process successfully.

**Evidence:** [View the successful validation test](../../screenshots/Day%202/04-valid-execution.png)

* Tested an invalid service request and confirmed that the system correctly identified the request as invalid instead of allowing it to continue as a valid request.

**Evidence:** [View the invalid validation test](../../screenshots/Day%202/05-invalid-execution.png)

## Result

The QuickFix HVAC workflow can now organize incoming customer information and validate service requests before they continue through the automation.

The system can distinguish between valid and invalid requests, helping ensure that incomplete or unsuitable information is identified before the request is processed further.
