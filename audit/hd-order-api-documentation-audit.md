---
title: HD Order API Documentation Audit
excerpt: Comparison of the HealthDyne documentation repository with the hd-order-api project.
hidden: true
---

# HD Order API Documentation Audit

## Executive summary

The current documentation provides a useful conceptual introduction to the HealthDyne Pharmacy APIs and their primary workflows. It does not, however, provide a complete or fully current representation of the `hd-order-api` project.

The documentation is strongest for the original Patient, Script, Fill, Insurance, and Mailbox workflows. The largest gaps are newer patient subresources, payment cards, prescription lists, renewals, triage, expanded mailbox operations, and detailed response models.

The Appendix is valuable as business-facing guidance, but it should not currently be treated as the authoritative definition of the API contract. Several field names, types, required/optional indicators, constraints, and response structures need to be reconciled with the project models and validators.

## Scope and method

This review compared:

- The Pharmacy APIs documentation under `docs/Documentation/workflows`.
- The non-Central Fill Appendix pages under `docs/Appendix`.
- The generated API reference under `reference/HealthDyne Order API v2.17`.
- The current endpoint inventory and QA reports in the `hd-order-api` project.
- The C# request, response, model, and validator definitions under `hd-order-api/Model/v2`.

Central Fill API documentation was excluded from the Appendix review as requested.

The comparison was a static documentation-to-source review. It did not validate deployed environments or production behavior.

## Pharmacy API coverage

The `hd-order-api` project endpoint inventory contains 44 endpoint scenarios. The current API reference contains 18 endpoint pages.

| API area | Project endpoints | Reference pages | Assessment |
|---|---:|---:|---|
| Fill | 8 | 4 | Partial |
| Mailbox | 5 | 3 | Partial |
| Patient | 24 | 8 | Significant gaps |
| Prescriptions | 1 | 0 | Missing |
| Script | 4 | 3 | Partial |
| Document/Triage | 1 | 0 | Missing |
| HealthCheck | 1 | 0 | Operational endpoint not represented |
| **Total** | **44** | **18** | **Incomplete** |

### Missing or incomplete Pharmacy API areas

The following project capabilities are not fully represented in the reference documentation:

- Fill order retrieval, asynchronous retrieval, general fill submission, and renewal requests.
- Mailbox status, batch, and batch-list operations.
- Patient address, contact, medication, allergy, and payment-card operations.
- Prescription list retrieval.
- Script discontinuation.
- Document/Triage submission.
- Current response and error models across the API.

The Pharmacy APIs landing page correctly explains the main eRx/Surescripts and Rx Transfer workflows, but it should either link to the complete API surface or clearly state that it is a workflow overview rather than a complete endpoint catalog.

## Appendix coverage

| Appendix section | Coverage | Assessment |
|---|---|---|
| Patient request fields | Mostly represented | Good baseline, incomplete current model |
| Insurance request fields | Partially represented | Core fields present; current variants incomplete |
| Script/Rx transfer fields | Mostly represented | Strong structure; current fields and rules incomplete |
| Fill request fields | Partially represented | Core payload covered; renewal, shipping update, and response models incomplete |
| Mailbox data object schemas | Partially represented | Good event catalog; exact current response shapes incomplete |
| Top reject reasons | Supplemental | Useful reference, not an object definition |
| `*-copy` pages | Duplicate content | Authority and maintenance risk |

## Detailed findings by Appendix section

### Patient request fields

The page covers the primary patient fields, address, contact, allergies, external medications, identification, prescriptions, and payment cards at a conceptual level.

Current project fields that are missing or insufficiently described include:

- `patientLanguage`
- `pregnancyIndicator`
- Patient identification code, identifier, and expiration date.
- Contact `primaryPhone` and `emailAddress`.
- Current payment-card request, response, and validation fields.
- Wrapper metadata such as `memberId` and ePost patient identifiers.

The documentation should distinguish the base patient payload from the separate address, contact, medication, allergy, and payment-card payloads. The project defines these as separate contracts.

### Insurance request fields

The page documents the primary insurance operations and common PBM fields such as BIN, PCN, group ID, policy/member information, and relationship codes.

Current definitions introduce additional or operation-specific fields, including:

- `insuranceMemberID`
- `personCode`
- `relationshipCode`
- `policyHolderId`
- Secondary and tertiary plan numbers.
- Fill copay fields: `clientItemCost`, `clientDispenseFee`, `clientOtherFee`, and `clientCoPay`.
- `transactionNumber` and fill-specific copay information.

Terminology is inconsistent across the documentation and code, including `groupId`/`groupNumber`, `policyHolderId`/`policyHolderID`, and `relationship`/`relationshipCode`. These should be resolved or explicitly documented as different contracts.

### Script/Rx transfer fields

This is one of the better-covered sections. It documents sending and receiving pharmacies, pharmacists, pharmacy contacts and addresses, prescriptions, prescribers, and transfer information.

The current project additionally includes:

- `transferFileType`
- `transferFileUrl`
- `orTransfer`
- `partnerCodes`
- Expanded prescription quantity, fill, refill, and inactive-status fields.

The documentation should clearly separate the transfer request, GET Script response, and fulfilling-pharmacy payload. These are related but distinct models in the project.

### Fill request fields

The page provides useful coverage of fill request keys, script keys, shipping, shipping codes, addresses, insurance, cancellation, updates, and status events.

Current project models add or expand:

- `clientId`
- `fillRequestId`
- Payment-card sequence number.
- Copay-specific script insurance details.
- Renewal request and renewal shipping objects.
- Shipping update objects.
- Shipment, tracking, order number, fill number, refill-by date, and remaining-refill details.
- Detailed rejected and error response fields.

The status documentation should be reconciled with the current event collections: `Submitted`, `RxVerified`, `RxShipped`, `RxIssue`, `RxCanceled`, `Rejected`, and `Renewed`.

### Mailbox data object schemas

The Mailbox page is strong as a business-level event catalog. It explains Rx transfer, Rx status, fill request, shipment, issue, cancellation, received, clarified, and payment events.

It is less complete as an exact object reference. Current models include distinct fetch, event-detail, batch, batch-list, and mark-delivered structures with fields such as:

- `batchId`
- `partnerCode`
- `count`
- `approximateRemainingCount`
- `messageList`
- `eventId`
- `messageId`
- `eventType`
- `eventDateUtc`
- `status`
- `statusMessage`

These structures should be documented separately with exact JSON examples.

## Description quality

The existing descriptions are generally understandable and useful for business users. They explain domain concepts such as shipping codes, relationship codes, prescription transfers, and mailbox statuses.

The following issues reduce contract confidence:

- Descriptions appear to reflect older model versions in places.
- Required versus optional status is not consistently aligned with validators.
- Types, nullability, length limits, date formats, and numeric formats are incomplete.
- Field casing and naming vary between pages.
- Request objects are described more consistently than response and error objects.
- The same object is described differently across multiple Appendix pages.
- The `*-copy.md` files create uncertainty about which page is authoritative.
- Validator behavior, including conditional requirements and allowed values, is generally not documented.

## Product-owner impact

A partner using the current documentation may be able to understand the main integration journey, but may not be able to implement all currently supported operations without consulting the source project or obtaining additional guidance.

The practical risks are:

- Partners miss supported capabilities such as payment cards, renewals, prescription lists, or triage.
- Integrations send incorrect field names or data types.
- Partners misunderstand required fields or conditional validation.
- Response and mailbox event processing is implemented against incomplete shapes.
- Documentation and implementation drift further as new endpoints are added.

## Recommended priorities

### Priority 1: Establish a source of truth

Confirm that the current `hd-order-api` models, validators, and generated OpenAPI definition are the authoritative contract. Confirm whether the ReadMe reference should represent the current project version rather than the existing v2.17 snapshot.

### Priority 2: Close endpoint and object gaps

Add documentation for:

- Patient subresources and payment cards.
- Prescription lists.
- Fill retrieval, asynchronous retrieval, renewals, and shipping updates.
- Mailbox status, batch, and batch-list operations.
- Script discontinuation.
- Document/Triage.
- Current error and response objects.

### Priority 3: Reconcile every Appendix contract

For each object, document the exact:

- JSON field name.
- Data type and nullability.
- Required/optional status.
- Length and format constraints.
- Allowed values and enums.
- Conditional validation rules.
- Request versus response usage.

### Priority 4: Improve maintainability

- Select one authoritative page for each object.
- Retire or clearly label the `*-copy.md` pages.
- Add representative request and response JSON examples.
- Add a version or last-reviewed indicator.
- Add a repeatable documentation validation step against the OpenAPI/model source.

## Recommended work plan

The following actions convert the findings into an implementation backlog.

| Priority | Action | Outcome |
|---|---|---|
| P0 | Confirm the supported API version and contract owner with the PO and engineering team. | Prevents documentation work from targeting an obsolete model or endpoint set. |
| P0 | Identify the authoritative OpenAPI/model source and compare it with the v2.17 reference currently in ReadMe. | Establishes whether the generated reference must be regenerated or only supplemented. |
| P0 | Reconcile required fields and conditional validation against the C# validators. | Prevents partners from receiving misleading implementation guidance. |
| P1 | Create a complete endpoint-to-documentation matrix for all current endpoints. | Makes coverage measurable and prevents missed endpoints. |
| P1 | Add missing reference pages for patient subresources, payment cards, prescription lists, renewals, mailbox operations, Script discontinue, and Document/Triage. | Brings the published API surface closer to the current project. |
| P1 | Update Appendix object tables to include every request and response field. | Provides complete implementation-level object coverage. |
| P1 | Document error, validation, status, shipment, and mailbox response objects. | Improves integration troubleshooting and event processing. |
| P2 | Standardize field names, casing, terminology, types, dates, and identifier names. | Reduces ambiguity and inconsistent payload implementations. |
| P2 | Add valid and invalid examples for each major request and response object. | Makes the documentation practical for partner developers. |
| P2 | Remove, merge, or clearly label the `*-copy.md` pages. | Eliminates duplicate-content and conflicting-definition risk. |
| P3 | Add a documented review/version marker to each contract page. | Makes stale documentation easier to identify. |
| P3 | Add a lightweight validation process that checks links, frontmatter, navigation, and model/reference coverage. | Creates an ongoing drift-detection mechanism. |

## Specific fixes and cleanup recommendations

### Fix contract accuracy

- Replace descriptions that do not match the current model or validator behavior.
- Mark nullability explicitly instead of inferring it from “optional.”
- Distinguish a field being optional from a field being conditionally required.
- Document exact JSON casing, especially where the code uses inconsistent casing such as `insuranceMemberID`, `EPostPatientNumber`, or legacy lower-case response properties.
- State whether dates are sent as `YYYY-MM-DD`, ISO date-time strings, or another format.
- State whether monetary values are strings, `double`, or decimal values for each operation.
- Document maximum lengths and format restrictions for identifiers, phone numbers, ZIP codes, NDCs, and pharmacy identifiers.
- Document enums and allowed values, including gender, address type, relationship code, shipping code, transfer file type, and program prescription type.

### Add missing object documentation

- Add dedicated patient subresource object sections for address, contact, allergies, external medications, identification, and payment cards.
- Add separate add, update, get, and delete payment-card request/response definitions.
- Add insurance definitions for patient insurance, fill insurance, copay insurance, and renewal insurance instead of presenting them as one interchangeable object.
- Add renewal request and renewal shipping definitions.
- Add prescription-list request, item, and response definitions.
- Add fill shipping-update, shipment, status, rejection, and error-response definitions.
- Add mailbox fetch, event message, event detail, batch, batch-list, and delivery-response definitions.
- Add Script discontinue and Document/Triage payload definitions if those endpoints are intended for external partners.

### Clean up organization and navigation

- Keep business workflow explanations in `docs/Documentation/workflows`.
- Keep exact field and payload definitions in `docs/Appendix`.
- Keep endpoint-specific request/response details in the API reference.
- Add links between each workflow, its endpoint reference pages, and its Appendix object definitions.
- Remove duplicate `patient-request-fields-copy.md`, `script-rxtransfer-fields-copy.md`, and `fill-request-fields-copy.md`, or label them as deprecated historical pages.
- Review `docs/Appendix/_order.yaml` after every page addition, rename, or removal.
- Decide whether `top-reject-reasons.md` belongs in the Appendix or under a troubleshooting/error documentation area.

### Define “done” for each object page

An Appendix object page should not be considered complete until it contains:

1. The object name and purpose.
2. Request or response direction.
3. Exact JSON field names.
4. Data type and nullability.
5. Required, optional, or conditionally required status.
6. Length, format, and allowed-value rules.
7. A valid JSON example.
8. Relevant error or validation behavior.
9. Links to the endpoints and workflows that use the object.
10. The API/model version and last-reviewed date.

## Suggested delivery sequence

1. Confirm the target contract/version and identify the source of truth.
2. Build the endpoint and object coverage matrix.
3. Update the Patient and Insurance sections first because they are shared by multiple workflows.
4. Update Script, Fill, and Mailbox request/response objects.
5. Add missing Prescription, Renewal, Payment Card, and Triage definitions.
6. Consolidate duplicate pages and repair navigation links.
7. Review all descriptions and validation rules with engineering and the PO.
8. Run documentation validation and perform a ReadMe review using partner-oriented examples.

This sequence reduces rework by resolving shared object definitions before updating the workflow and endpoint pages that depend on them.

## Final assessment

The documentation is suitable as a high-level introduction to the core HealthDyne Pharmacy workflows. It is not yet sufficient as a complete implementation reference for the current `hd-order-api` project.

The recommended product decision is to treat this as a documentation alignment effort, not simply a content polish effort. The work should include contract reconciliation, missing endpoint coverage, response-model documentation, and a maintenance process that prevents future drift.

## v2.30 implementation status

The following alignment work has been implemented in this branch:

- Added a current-model supplement in the Appendix.
- Added a current endpoint inventory to the API reference navigation.
- Recorded the missing Fill, Mailbox, Patient, Prescription, Script, Document/Triage, and HealthCheck endpoints.
- Removed duplicate copy pages from Appendix navigation while preserving the hidden files.
- Added cross-links from the primary Appendix pages to the current-model supplement.
- Clarified that the Pharmacy APIs landing page is a workflow overview.

The following work remains before the documentation can be considered fully contract-aligned:

- Regenerate the OpenAPI source from the current service implementation.
- Bind the inventory endpoints to operation-specific generated reference pages.
- Complete field-by-field reconciliation against every model and validator.
- Add exact request/response examples and validation behavior for the newly documented objects.
- Obtain engineering and PO confirmation of the supported public contract and version.

## Evidence locations

- Pharmacy API navigation: `docs/Documentation/workflows/index.md`
- Appendix navigation: `docs/Appendix/_order.yaml`
- Patient Appendix: `docs/Appendix/patient-request-fields.md`
- Insurance Appendix: `docs/Appendix/insurance-request-fields.md`
- Script Appendix: `docs/Appendix/script-rxtransfer-fields.md`
- Fill Appendix: `docs/Appendix/fill-request-fields.md`
- Mailbox Appendix: `docs/Appendix/mailbox-data-object-schemas.md`
- Project endpoint inventory: `hd-order-api/docs/qa/endpoints/README.md`
- Project consolidated QA inventory: `hd-order-api/docs/qa/all-endpoints-scenario-report.md`
