---
title: V2.17 Release Updates
author: Yachna
hidden: false
published_at: '2024-05-13T21:00:52.772Z'
type: added
---
## FillRequest Updates:

The endpoint enables client to send a request to update fill request (order) for shipping details (address and shipment code).Note: the Update will be applied as long as order has not been sent to our dispensing system.

## Patient Updates:

* Get patient: This endpoint requires patientKey and will retrieve/return patient information (active details) that exist in HD pharmacy system.
* Find Patient: This endpoint enables client to lookup patient in HealthDyne system using patient basic parameters (First Name + Last name+ DOB and Zipcode)  . If a match is found, HD returns the patient Key for client to retrieve patient details using Get Patient.

## Enhanced Prescription events:

The new event messages lets the client know about prescription/Rx status in HD system. Ingesting these events will allow clients to be able to better service the patients letting them know when prescription expires, ready for refill. This is configurable for client to opt in/out to receive these events while the default functionality is enabled to send the events.\*\*

* eRx Refill Reminder notifications: When a prescription is ready for refill.
* eRx Overdue notification: When a prescription is ready for refill and still have not received an order request.
* eRx Renewal notification: When a prescription has expired/exhausted all fills and is ready for prescriber to be renewed.

## Get Script API Update:

The endpoint response is updated  to include new elements:

* FillsRemaining
* Quantity remaining
* Next fill Date
* Clinic Code