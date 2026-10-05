# Day 1 — Project Setup & Webhook Foundation

## What We Want to Do

We want to build a reliable AI receptionist system for QuickFix HVAC that can receive customer service requests and connect the AI receptionist with an automation workflow.

The first step is to create the foundation of the system so that customer information can be received by the automation workflow.

## What We Are Going to Do

* Set up the QuickFix HVAC automation project.
* Create the initial n8n workflow.
* Create a webhook that can receive customer service request information.
* Test that the webhook can successfully receive customer data.
* Establish the foundation for connecting the AI receptionist with the automation workflow.

## What We Have Performed

* Created the **QuickFix HVAC — Live Service Request** workflow in n8n.

* Created a **POST webhook** to receive service request information from the AI receptionist.

* Configured the webhook so that it can receive customer information through a structured request.

* Tested the webhook with sample customer information and confirmed that the request was successfully received by the n8n workflow.

* Confirmed that the received information is available inside the workflow and can be processed by the next automation steps.

**Evidence:** [View the successful webhook test](../../screenshots/Day%201/n8n-test-webhook.png)

## Result

The basic communication foundation for the QuickFix HVAC system is now working.

The n8n workflow can receive a customer service request through its webhook, providing the starting point for processing, validating, routing, and storing customer requests in the following stages of the project.
