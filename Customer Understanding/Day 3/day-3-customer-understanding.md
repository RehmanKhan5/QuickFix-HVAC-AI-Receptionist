# Day 3 — Request Routing & Service Record Creation

## What We Want to Do

We want the QuickFix HVAC system to take validated customer service requests and route them correctly based on whether the request is an emergency or a routine service request.

The system should then create an organized service record so the business can keep track of incoming requests.

## What We Are Going to Do

* Add emergency and routine request routing.
* Separate emergency requests from routine service requests.
* Connect the appropriate workflow paths to Google Sheets.
* Create service request records.
* Test both emergency and routine requests.
* Confirm that the correct information is recorded successfully.

## What We Have Performed

* Configured the workflow to route validated requests according to their emergency status.

**Evidence:** [View the Day 3 workflow overview](../../screenshots/Day%203/01-day-3-complete-workflow.png)

* Configured the **Switch** step to separate emergency requests from routine requests.

**Evidence:** [View the Switch configuration](../../screenshots/Day%203/02-day-3-switch-node.png)

* Connected the request-processing workflow to Google Sheets for storing service request records.

**Evidence:** [View the Google Sheets configuration](../../screenshots/Day%203/03-day-3-google-sheets-node.png)

* Configured the emergency-service path to store emergency requests correctly.

**Evidence:** [View the emergency Google Sheets configuration](../../screenshots/Day%203/04-day-3-emergency-google-sheets-node.png)

* Tested an emergency service request and confirmed that it was successfully prepared and routed through the emergency path.

**Evidence:** [View the emergency request test](../../screenshots/Day%203/05-day-3-prepare-emergency-request-success.png)

* Confirmed that the emergency request reached the correct routing path.

**Evidence:** [View the emergency routing result](../../screenshots/Day%203/06-day-3-emergency-routing-success.png)

* Confirmed that the emergency request received the expected workflow response.

**Evidence:** [View the emergency response result](../../screenshots/Day%203/07-day-3-emergency-response-success.png)

* Tested the emergency request through Postman and confirmed successful processing.

**Evidence:** [View the successful emergency Postman test](../../screenshots/Day%203/08-day-3-successful-emergency-postman.png)

* Verified that the emergency service request was successfully recorded in Google Sheets.

**Evidence:** [View the emergency service record — left](../../screenshots/Day%203/09-day-3-emergency-google-sheets-success-left.png) · [right](../../screenshots/Day%203/10-day-3-emergency-google-sheets-success-right.png)

* Tested a routine service request and confirmed that it was routed through the routine path instead of the emergency path.

**Evidence:** [View the routine routing result](../../screenshots/Day%203/11-day-3-routine-routing-success.png)

* Verified that the routine service request was successfully recorded in Google Sheets.

**Evidence:** [View the routine service record — left](../../screenshots/Day%203/12-day-3-routine-google-sheets-success-left.png) · [right](../../screenshots/Day%203/13-day-3-routine-google-sheets-success-right.png)

* Further verified the emergency service record in Google Sheets.

**Evidence:** [View the emergency record — left](../../screenshots/Day%203/14-day-3-emergency-google-sheets-record-left.png) · [right](../../screenshots/Day%203/15-day-3-emergency-google-sheets-record-right.png)

## Result

The QuickFix HVAC system can now take validated service requests and route them correctly as either **emergency** or **routine** requests.

The requests are then recorded in Google Sheets, giving the business an organized service-request record and ensuring that different types of customer requests follow the appropriate workflow path.
