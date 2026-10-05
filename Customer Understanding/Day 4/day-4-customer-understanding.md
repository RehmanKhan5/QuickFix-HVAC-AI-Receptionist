# Day 4 — Post-Call Recording & Call History

## What We Want to Do

After an AI receptionist call is completed, the business should have a clear record of what happened during the call.

We want to create a separate process that stores important customer and call information for review, record keeping, and follow-up.

## What We Are Going to Do

* Create a separate post-call workflow.
* Receive completed call information through a dedicated webhook.
* Organize important customer and call details.
* Store the information in a Google Sheets Call History.
* Record different call outcomes.
* Test different types of completed calls.
* Verify that the call records are stored correctly.

## What We Have Performed

* Created the **QuickFix HVAC — Post Call Recording** workflow.

**Evidence:** [View the Day 4 post-call workflow](../../screenshots/Day%204/01-day-4-post-call-workflow.png)

* Created a dedicated POST webhook for receiving completed call information.

**Evidence:** [View the post-call webhook](../../screenshots/Day%204/02-day-4-post-call-webhook.png)

* Organized the call information into eight fields: Call ID, Date/Time, Customer Name, Phone, Call Summary, Call Outcome, Request Status, and Source.

**Evidence:** [View the Edit Fields configuration](../../screenshots/Day%204/03-day-4-edit-fields.png)

* Tested the post-call workflow and confirmed that the received information was processed correctly.

**Evidence:** [View the successful post-call test](../../screenshots/Day%204/04-day-4-post-call-test-success.png)

* Connected the workflow to a separate **Call History** sheet and mapped the call information to the appropriate columns.

**Evidence:** [View the Google Sheets mapping](../../screenshots/Day%204/05-day-4-google-sheets-mapping.png)

* Tested an incomplete customer call and confirmed that the incomplete outcome was recorded.

**Evidence:** [View the incomplete call record](../../screenshots/Day%204/06-day-4-incomplete-call-record.png)

* Tested a customer request to speak with a human representative and confirmed that the outcome was recorded.

**Evidence:** [View the human-requested record](../../screenshots/Day%204/07-day-4-human-requested-record.png)

* Tested a service-request tool failure and confirmed that the failed outcome was recorded.

**Evidence:** [View the tool-failure record](../../screenshots/Day%204/08-day-4-tool-failure-record.png)

* Tested an outside-service-area request and confirmed that the outcome was recorded correctly.

**Evidence:** [View the outside-service-area record](../../screenshots/Day%204/09-day-4-outside-service-area-record.png)

* Verified that all five test scenarios were successfully stored in the Call History.

**Evidence:** [View all Day 4 call-history test records](../../screenshots/Day%204/10-day-4-call-history-all-tests.png)

## Result

The QuickFix HVAC system now has a separate post-call process for maintaining an organized history of customer calls.

The system can record successful and different non-standard call outcomes, giving the business a clear record that can be used for **review, follow-up, and call management**.
