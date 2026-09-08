---
title: Current HD Order API Endpoint Inventory
excerpt: Endpoint inventory for the current hd-order-api implementation.
deprecated: false
hidden: false
metadata:
  title: ''
  description: Current endpoint inventory pending OpenAPI regeneration.
  robots: index
---

# Current HD Order API Endpoint Inventory

This page records endpoints present in the current `hd-order-api` implementation that are not completely represented by the existing v2.17 OpenAPI reference. It is intended to prevent capability gaps while the generated reference is regenerated from the current source contract.

The existing v2.17 reference should not be assumed to include every endpoint listed here. Request and response schemas must be bound to a regenerated OpenAPI document before this page is treated as a replacement for operation-specific reference pages.

## Fill

| Method | Endpoint | Purpose |
|---|---|---|
| POST | `/v2/Fill` | Submit a standard fill request. |
| POST | `/v2/Fill/FillRequest` | Submit a fill request using the fill-request route. |
| GET | `/v2/Fill/FillRequest?fillRequestKey={key}` | Retrieve fill-request status. |
| GET | `/v2/Fill?partnerCode={code}` | Retrieve orders for a partner. |
| GET | `/v2/Fill/async?partnerCode={code}` | Retrieve orders asynchronously for a partner. |
| POST | `/v2/Fill/Cancel` | Cancel a fill request. |
| PUT | `/v2/Fill` | Submit a shipping/fill update. |
| POST | `/v2/Fill/RenewalRequest` | Submit a renewal request. |

See [Fill Request Data Objects](doc:fill-request-fields) for shared fill, shipping, insurance, and status objects.

## Mailbox

| Method | Endpoint | Purpose |
|---|---|---|
| GET | `/v2/Mailbox?messageCount={count}` | Fetch available mailbox events. |
| POST | `/v2/Mailbox?batchId={batchId}` | Mark mailbox events as delivered. |
| GET | `/v2/Mailbox/Status` | Retrieve mailbox status information. |
| GET | `/v2/Mailbox/Batch?batchId={batchId}` | Retrieve mailbox events for a batch. |
| GET | `/v2/Mailbox/Batch/List?batchId={batchId}` | Retrieve the event list for a batch. |

See [Mailbox Data Object Schemas](doc:mailbox-data-object-schemas) for event and response definitions.

## Patient

| Method | Endpoint | Purpose |
|---|---|---|
| POST | `/v2/Patient` | Create a patient. |
| PUT | `/v2/Patient` | Update a patient. |
| POST | `/v2/Patient/v2/Patient/Patient` | Create a patient through the legacy direct route. |
| PUT | `/v2/Patient/v2/Patient/Patient` | Update a patient through the legacy direct route. |
| GET | `/v2/Patient?patientKey={key}` | Retrieve a patient. |
| GET | `/v2/Patient/find?firstName=&lastName=&birthDate=&zipCode=` | Find a patient. |
| GET | `/v2/Patient/prescription?patientKey={key}` | Retrieve patient prescriptions. |
| GET | `/v2/Patient/Insurance?patientKey={key}` | Retrieve patient insurance. |
| POST | `/v2/Patient/insurance` | Add patient insurance. |
| PUT | `/v2/Patient/insurance` | Update patient insurance. |
| DELETE | `/v2/Patient/Insurance?patientKey=&planNumber=` | Delete patient insurance. |
| POST | `/v2/Patient/address` | Add a patient address. |
| DELETE | `/v2/Patient/address` | Delete a patient address. |
| POST | `/v2/Patient/Contact` | Add a patient contact. |
| DELETE | `/v2/Patient/Contact` | Delete a patient contact. |
| PUT | `/v2/Patient/Profile` | Update patient profile fields. |
| POST | `/v2/Patient/medications` | Add external medications. |
| DELETE | `/v2/Patient/medications` | Delete external medications. |
| POST | `/v2/Patient/allergies` | Add allergies. |
| DELETE | `/v2/Patient/allergies` | Delete allergies. |
| GET | `/v2/Patient/{patientKey}/paymentcard` | Retrieve payment cards. |
| POST | `/v2/Patient/paymentcard` | Add a payment card. |
| PUT | `/v2/Patient/paymentcard` | Update a payment card. |
| DELETE | `/v2/Patient/paymentcard` | Deactivate a payment card. |

See [Patient Request Data Objects](doc:patient-request-fields) for patient, address, contact, medication, allergy, identification, and payment-card objects.

## Prescriptions

| Method | Endpoint | Purpose |
|---|---|---|
| GET | `/v2/Prescriptions/List?fillRequestKey={key}` | Retrieve prescriptions associated with a fill request. |

The response contains a prescription list with request, Rx, status, shipping, plan, and ordered-drug information.

## Script

| Method | Endpoint | Purpose |
|---|---|---|
| POST | `/v2/Script` | Submit a script request. |
| GET | `/v2/Script?scriptKey={key}` | Retrieve script details. |
| POST | `/v2/Script/transfer` | Transfer a prescription. |
| POST | `/v2/Script/discontinue` | Discontinue a prescription. |

See [Script / RxTransfer Data Objects](doc:script-rxtransfer-fields) for pharmacy, prescription, prescriber, and transfer objects.

## Document/Triage

| Method | Endpoint | Purpose |
|---|---|---|
| POST | `/v2/Document/triage` | Submit a triage document and associated patient, pharmacy, prescriber, and attachment information. |

Triage attachments are validated as a single PDF attachment with a Base64 body. The current implementation also validates required metadata, patient demographics, destination pharmacy, prescriber, and program prescription type.

## Operational endpoint

| Method | Endpoint | Purpose |
|---|---|---|
| GET | `/v2/HealthCheck` | Check service health. |

## Publication requirement

Before publishing operation-specific pages for this inventory, regenerate the OpenAPI document from the current service and model definitions. Then bind each endpoint page to the regenerated document and remove any duplicate manual schema definitions that conflict with it.
