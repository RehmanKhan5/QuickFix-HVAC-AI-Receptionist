# Day 3 — Routing Requests and Saving Data

## 1. Day 3 Goal

The main goal of Day 3 was to continue building the **QuickFix HVAC — Live Service Request** workflow.

On Day 2, the workflow was able to:

- Receive the customer request through the Webhook.
- Extract the customer information.
- Clean and normalize the data.
- Validate the customer request.
- Check the phone number.
- Check the service area.
- Check required information.
- Check the emergency fee agreement when required.
- Produce a final `isValid` value.
- Send valid and invalid requests to different branches.

On Day 3, the main focus was to take a **valid request** and determine whether it was:

- an **Emergency request**, or
- a **Routine request**.

The request was then sent to the appropriate branch and prepared for storage in Google Sheets.

---

# 2. Workflow Used on Day 3

The workflow structure was:

```text
Webhook
    ↓
Edit Fields
    ↓
Code
    ↓
IF
    ├── FALSE → Invalid Response
    │
    └── TRUE
          ↓
        Switch
        ├── Emergency
        │      ↓
        │   Google Sheets
        │
        └── Routine
               ↓
            Google Sheets
The workflow uses the validation result from the Code node before allowing the request to continue.

This prevents invalid customer requests from being stored as valid service requests.

3. The IF Node

The IF node checks the value:

{{ $json.isValid }}

The condition is:

is true

There are two possible results.

TRUE

If:

isValid = true

the request is considered valid and continues to the Switch node.

FALSE

If:

isValid = false

the request is invalid and does not continue to the normal service-request processing.

This is important because the system should not send incomplete or invalid requests to the technician/service database.

4. Switch Node

After a request passes validation, the Switch node determines whether the request is an emergency or routine request.

The Switch checks:

{{ $json.emergency }}

There are two possible values.

Emergency
true

The request goes to the Emergency branch.

Routine
false

The request goes to the Routine branch.

The same Switch node is used for both types of requests.

There is no need to create another Switch node.

5. Why the Switch Node Is Important

The Switch node makes the workflow behave differently depending on the customer's situation.

For example:

Routine request
{
  "customerName": "John Smith",
  "phone": "+15125550123",
  "address": "123 Austin Street, Austin, TX",
  "serviceType": "AC Repair",
  "issue": "AC is blowing warm air",
  "emergency": false,
  "preferredTime": "As soon as possible"
}

Because:

emergency = false

the request goes to the Routine branch.

Emergency request

For example:

{
  "customerName": "John Smith",
  "phone": "+15125550123",
  "address": "123 Austin Street, Austin, TX",
  "issue": "No cooling and water is leaking",
  "emergency": true,
  "feeAgreed": true
}

Because:

emergency = true

the request goes to the Emergency branch.

6. Emergency Branch

The Emergency branch is designed for urgent HVAC requests.

Examples can include:

No cooling during an emergency situation.
Serious heating failure.
Major water leakage.
Other situations that require urgent attention.

Emergency requests require additional validation.

For an emergency request, the workflow checks information such as:

customerName
phone
address
issue
emergency
feeAgreed

The emergency fee agreement is important.

If:

emergency = true

then:

feeAgreed = true

must be present for the request to be considered valid.

7. Routine Branch

Routine requests are normal HVAC service requests that do not require emergency handling.

For example:

AC Repair
Heating Repair
Maintenance
Inspection

A routine request requires information such as:

customerName
phone
serviceType
preferredTime

The request can then be routed to the Routine Google Sheets branch.

8. Google Sheets

Google Sheets was used as the storage/database layer for the portfolio project.

The purpose is to save valid customer service requests so that the HVAC company can review them later.

The workflow can store information such as:

Customer Name
Phone
Email
Address
Service Type
Issue
Emergency
Fee Agreement
Preferred Time
Service Area

This gives the project a simple database-like system without requiring a complicated CRM.

9. Emergency Google Sheets Test

An emergency request was tested and successfully routed through the emergency branch.

The test confirmed that:

emergency = true

caused the request to go to the Emergency route.

The request was then prepared for the Emergency Google Sheets node.

The successful routing was captured in screenshots for the portfolio.

10. Routine Google Sheets Test

A routine request was also tested.

For the routine test:

emergency = false

The Switch node correctly sent the request to the Routine branch.

The successful routine routing and Google Sheets result were captured in screenshots.

This confirmed that the same workflow can handle both:

Emergency → Emergency branch
Routine → Routine branch
11. Postman Testing

Postman was used to send test customer requests to the n8n Webhook.

This allowed the workflow to be tested without using a real telephone call.

The test process was:

Postman
    ↓
n8n Webhook
    ↓
Edit Fields
    ↓
Code Validation
    ↓
IF
    ↓
Switch
    ↓
Emergency / Routine
    ↓
Google Sheets

This makes testing easier before connecting the real phone system.

12. Important Validation Result

One successful routine test produced clean information similar to:

{
  "customerName": "John Smith",
  "phone": "+15125550123",
  "email": "john@example.com",
  "address": "123 Austin Street, Austin, TX",
  "serviceType": "AC Repair",
  "issue": "AC is blowing warm air",
  "emergency": false,
  "feeAgreed": false,
  "preferredTime": "As soon as possible",
  "phoneValid": true,
  "serviceAreaValid": true,
  "serviceArea": "austin",
  "emergencyFeeValid": true,
  "isValid": true,
  "missingFields": []
}

An important point is that:

feeAgreed = false

does not make a routine request invalid.

The emergency fee agreement is only required when:

emergency = true

Therefore, in a routine request:

emergencyFeeValid = true

means that no emergency fee agreement was required for this request.

13. One Code Node Handles the Validation

The project continues to use one main reusable Code node for validation.

The Code node handles multiple conditions, including:

Cleaning input.
Checking required fields.
Validating the phone number.
Checking emergency information.
Checking routine information.
Checking the service area.
Checking the emergency fee agreement.
Producing the final isValid result.

The test data changes from test to test.

The production validation logic remains in the same Code node.

This is better than creating a separate Code node for every possible customer situation.

14. Day 3 Screenshots

A total of 15 Day 3 screenshots were organized.

They were placed in:

screenshots/Day 3/

The screenshots were renamed in numerical order:

01-day-3-complete-workflow.png
02-day-3-switch-node.png
03-day-3-google-sheets-node.png
04-day-3-emergency-google-sheets-node.png
05-day-3-prepare-emergency-request-success.png
06-day-3-emergency-routing-success.png
07-day-3-emergency-response-success.png
08-day-3-successful-emergency-postman.png
09-day-3-emergency-google-sheets-success-left.png
10-day-3-emergency-google-sheets-success-right.png
11-day-3-routine-routing-success.png
12-day-3-routine-google-sheets-success-left.png
13-day-3-routine-google-sheets-success-right.png
14-day-3-emergency-google-sheets-record-left.png
15-day-3-emergency-google-sheets-record-right.png

The filenames were cleaned so that there were no accidental double extensions such as:

.png.PNG
15. GitHub Backup

After organizing the screenshots, the Day 3 screenshot folder was added to Git.

The files were staged with:

git add "screenshots/Day 3/"

The Day 3 screenshots were committed with:

git commit -m "Add Day 3 workflow screenshots"

The commit created was:

e33d8f7

with the message:

Add Day 3 workflow screenshots

The commit contained:

15 files changed

The changes were then pushed to GitHub using:

git push origin main

The push was successful:

4cc886a..e33d8f7  main -> main

Therefore, the 15 Day 3 screenshots are now backed up in the GitHub repository.

16. What Was Completed on Day 3

By the end of Day 3, the following work was completed:

Created/used the Switch routing logic.
Tested Emergency routing.
Tested Routine routing.
Connected the appropriate Google Sheets branches.
Tested emergency request processing.
Tested routine request processing.
Tested requests through Postman.
Verified successful routing.
Captured screenshots as portfolio evidence.
Renamed all 15 Day 3 screenshots.
Organized them inside screenshots/Day 3/.
Added the screenshots to Git.
Created a Day 3 Git commit.
Pushed the Day 3 screenshots to GitHub.
17. Day 3 Final Workflow Concept

The main concept learned on Day 3 is:

Receive Request
       ↓
Clean Data
       ↓
Validate Request
       ↓
Is Request Valid?
     /       \
   NO         YES
   ↓           ↓
Invalid      Switch
Response       ↓
          ┌────┴────┐
          ↓         ↓
      Emergency   Routine
          ↓         ↓
      Google      Google
      Sheets      Sheets

This creates a clear separation between:

Validation
Emergency handling
Routine handling
Data storage

This structure will make it easier to connect the workflow to the AI receptionist later.

18. Day 3 Result

Day 3 successfully moved the QuickFix HVAC project from basic validation toward a more complete service-request automation system.

The workflow can now determine:

Is the request valid?
        ↓
Is it an emergency?
        ↓
Which processing branch should be used?
        ↓
Where should the request be stored?