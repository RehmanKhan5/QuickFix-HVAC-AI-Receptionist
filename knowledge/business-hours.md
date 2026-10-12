# QuickFix HVAC & Cooling — Business Hours

## 1. Purpose

This document defines the fictional business hours and availability rules used in the QuickFix HVAC & Cooling AI receptionist portfolio project.

QuickFix HVAC & Cooling is a fictional demonstration business. These hours are examples for testing and must not be presented as verified hours for a real company.

## 2. Time Zone

The demonstration business is located in Austin, Texas, USA.

Use the local time in Austin, Texas, when interpreting the business's opening hours and customer-preferred service times.

The receptionist must not assume that the customer's local time is the same as the business's local time.

## 3. Regular Business Hours

For this portfolio demonstration, use the following example weekday schedule:

- Monday: 8:00 AM to 5:00 PM
- Tuesday: 8:00 AM to 5:00 PM
- Wednesday: 8:00 AM to 5:00 PM
- Thursday: 8:00 AM to 5:00 PM
- Friday: 8:00 AM to 5:00 PM

These are fictional example hours. They have not been verified for a real business.

Saturday and Sunday hours have not been established for this demonstration. The receptionist must not assume that the business is open or closed on those days.

## 4. After-Hours Requests

The AI receptionist may collect a service request outside regular business hours if the configured workflow permits it.

The receptionist must explain that submitting a request does not guarantee immediate service or technician availability.

Example response:

"Our regular office hours have ended, but I can collect your information if the request system is available. I cannot guarantee when a technician will respond."

The receptionist must not promise a callback time unless an authorized system confirms it.

## 5. Emergency Requests Outside Business Hours

A customer may report an urgent HVAC problem outside regular business hours.

The receptionist should:

- Ask appropriate questions to understand the reported issue.
- Screen for immediate safety risks.
- Follow the emergency and safety instructions in the approved knowledge documents.
- Explain the demonstration emergency fee of $180 when the applicable workflow requires it.
- Record the customer's fee decision accurately.
- Submit the request only when the required information and conditions are satisfied and the configured tool is available.

The receptionist must not claim that an emergency technician is available or has been dispatched unless a reliable system confirms it.

The emergency fee is a fictional demonstration amount, not a verified real-world charge.

## 6. Holidays

Holiday hours have not been defined for this demonstration.

If a customer asks whether the business is open on a holiday, the receptionist must not invent a holiday schedule.

Example response:

"I don't have verified holiday hours available. I can record your request if the system allows it, but I cannot confirm holiday service availability."

A real business must provide its approved holiday schedule before this feature is used in production.

## 7. Appointment Availability

Business hours do not automatically indicate that an appointment slot is available.

The receptionist may collect a customer's preferred date and time.

The receptionist must not:

- Guarantee an appointment based only on business hours.
- Claim that a technician is free at a particular time without confirmation.
- Promise a same-day visit without verified availability.
- Say that a booking is confirmed unless an actual booking system confirms it.

If no booking system is connected, the receptionist must explain that the preferred time is a request, not a confirmed appointment.

## 8. Human Assistance

If a customer asks to speak with a person, the receptionist should follow the configured human-handoff process if one exists.

If no working transfer or callback system is available, the receptionist must not claim that a transfer or callback has been arranged.

The receptionist may record a request for human assistance if the configured workflow supports it.

## 9. When Business Hours Cannot Be Verified

If the hours or availability information is missing, unclear, or inconsistent, the receptionist must not guess.

It should explain the limitation politely and follow the configured procedure for collecting or escalating the request.

## 10. Relationship to Other Knowledge Documents

Use `services.md` for supported service categories and safety limitations.

Use `pricing.md` for demonstration prices and emergency-fee rules.

Use `faq.md` for common customer questions and approved example responses.

Use `service-area.md` for service-area eligibility.

Use the configured workflow or booking system to verify whether a request was submitted or an appointment was confirmed.

## 11. Important Portfolio Disclaimer

The business hours in this document are fictional examples for an AI receptionist portfolio project.

Before use by a real business, the owner must review and approve all opening hours, holiday schedules, after-hours procedures, and emergency availability rules.

# End of Business Hours Document