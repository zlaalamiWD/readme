---
title: Current HD Order API Models
excerpt: Current request, response, and validation additions not fully represented in the legacy object pages.
---

# Current HD Order API Models

This page supplements the legacy object pages with model areas currently present in the HD Order API implementation. The endpoint reference and the project OpenAPI definition remain authoritative for exact operation-specific schemas.

## Current model areas

| Area | Current objects and fields | Used by |
|---|---|---|
| Patient profile | `patientLanguage`, `pregnancyIndicator`, identification fields, contact email and primary-phone fields | Patient create/update and subresources |
| Patient subresources | Address, contact, allergies, external medications, and payment-card request/response objects | Patient APIs |
| Insurance | Patient insurance, fill insurance, copay insurance, renewal insurance, secondary and tertiary plans | Patient, Fill, and Renewal APIs |
| Fill | `clientId`, `fillRequestId`, shipping updates, shipments, tracking, rejection, and error responses | Fill APIs |
| Renewal | Renewal request, renewal shipping, and script insurance information | Renewal request API |
| Prescriptions | Prescription-list item and response objects | Prescription list API |
| Mailbox | Fetch response, event message, event detail, batch, batch-list, and delivery response objects | Mailbox APIs |
| Script | Discontinue request, transfer-file fields, partner codes, and expanded prescription details | Script APIs |
| Triage | Triage request, attachment, pharmacy destination, prescriber, patient, and response objects | Document/Triage API |

## Contract rules to document

For every object used by a public endpoint, document the following:

- Exact JSON field name and casing.
- Data type and whether `null` is accepted.
- Required, optional, or conditionally required status.
- Maximum length and format restrictions.
- Allowed values and enum meanings.
- Date and time representation.
- Numeric and monetary representation.
- Request versus response usage.
- Validation and error behavior.

## Important distinctions

### Patient objects

The base patient payload is not interchangeable with address, contact, allergy, external-medication, identification, or payment-card payloads. These operations use separate request wrappers and should be documented separately.

### Insurance objects

Patient insurance, fill insurance, copay insurance, and renewal insurance are related but operation-specific objects. Their similarly named fields should not be assumed to have identical requirements or types.

### Fill status objects

Fill status responses contain separate event collections, including `Submitted`, `RxVerified`, `RxShipped`, `RxIssue`, `RxCanceled`, `Rejected`, and `Renewed`. Each event type should have its own field table and example.

### Mailbox objects

Mailbox fetch responses, individual event messages, event details, batch responses, batch-list responses, and mark-delivered responses are distinct structures. They should not be documented as one generic mailbox object.

## Current object backlog

The following pages or sections should be added to the appropriate detailed Appendix pages:

- Payment-card request and response schemas.
- Prescription-list request, item, and response schemas.
- Renewal request and renewal-shipping schemas.
- Fill shipping-update, shipment, rejection, and error-response schemas.
- Mailbox batch, batch-list, and delivery-response schemas.
- Script discontinue request schema.
- Document/Triage request, attachment, and response schemas.

## Version and maintenance note

This page was added as part of the v2.30 documentation alignment work. It must be reviewed against the current `hd-order-api` model, validator, and OpenAPI sources whenever the API contract changes. It is not a replacement for operation-specific API reference pages.
