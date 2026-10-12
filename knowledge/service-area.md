
# QuickFix HVAC & Cooling — Service Area Policy

## 1. Purpose

This document defines the fictional service area for the QuickFix HVAC & Cooling AI receptionist portfolio project.

QuickFix HVAC & Cooling is a fictional demonstration business. The locations in this document are examples for testing and are not proof that a real company operates in these areas.

## 2. Primary Service Location

The demonstration business is based in Austin, Texas, USA.

Austin is the primary reference location for the example service area and business hours.

## 3. Supported Service Areas

For this portfolio demonstration, the configured service area includes:

- Austin, Texas
- Round Rock, Texas
- Pflugerville, Texas
- Cedar Park, Texas

The receptionist should use these locations as the approved example service area.

## 4. Collecting the Customer's Location

The receptionist should collect the service address and city when needed to determine whether the request falls within the configured service area.

If the customer has already provided the relevant location information, the receptionist should not ask for it again unnecessarily.

The receptionist must not assume that a location is supported merely because it is near Austin.

## 5. Customer Inside the Service Area

If the customer's location matches a supported area, the receptionist may continue collecting the information needed for the service request.

Example response:

"Thank you. That location is within our configured demonstration service area. I'll collect a few details about the HVAC problem."

The receptionist must still follow all other request requirements, including required customer details, safety screening, emergency-fee agreement where applicable, and tool availability.

Being inside the service area does not guarantee appointment availability or service confirmation.

## 6. Customer Outside the Service Area

If the customer's location is outside the supported areas, the receptionist must not promise that the business can provide service.

Example response:

"I'm sorry, but your location is outside our currently configured demonstration service area. I don't want to promise a service that I cannot verify."

The receptionist must follow the configured workflow for outside-area requests.

It must not submit an outside-area request as an eligible service request unless an authorized configuration explicitly permits it.

## 7. Unclear or Unrecognized Locations

If the customer gives an unclear location, the receptionist should ask one concise follow-up question.

Example response:

"Could you please tell me the city where the service is needed?"

If the location still cannot be verified, the receptionist must not guess or automatically approve the service area.

It should explain that the location could not be verified and follow the configured fallback procedure.

## 8. Emergency and Safety Situations

Service-area eligibility must not prevent the receptionist from providing appropriate basic safety guidance.

If a customer reports an immediate danger, such as a suspected gas leak, smoke, sparks, or another immediate threat, the receptionist must prioritize personal safety and direct the customer to the appropriate emergency service from a safe location.

The receptionist must not promise that QuickFix HVAC & Cooling will dispatch a technician outside the supported area.

An equipment failure alone does not automatically mean that there is an immediate life-threatening emergency.

## 9. Service Area and Appointment Availability

A customer being inside the service area does not mean an appointment is available.

The receptionist may collect a preferred service time, but it must not confirm a booking unless an actual booking system verifies it.

The receptionist must not promise a technician's arrival time without reliable confirmation.

## 10. Relationship to Other Knowledge Documents

Use `services.md` to understand supported service categories.

Use `pricing.md` to explain demonstration prices and emergency-fee rules.

Use `faq.md` for common customer questions and approved example answers.

Use `business-hours.md` for regular hours, after-hours handling, and holiday limitations.

Follow the configured workflow to determine whether the request satisfies the required conditions and whether submission succeeded.

## 11. Important Portfolio Disclaimer

The locations in this document are fictional demonstration settings for a portfolio project.

Before a real business uses this receptionist, its owner must verify and approve the actual service locations, boundaries, eligibility rules, and outside-area procedures.

# End of Service Area Document
