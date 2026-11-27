---
title: Getting Started
deprecated: false
hidden: true
metadata:
  robots: index
---
# Welcome to the HealthDyne API platform.

HealthDyne provides secure, API-driven pharmacy integration capabilities that enable healthcare organizations, digital health platforms, and pharmacy partners to manage patients, prescriptions, insurance coverage, and medication fulfillment through their existing applications.

This guide will help you understand the prerequisites for integrating with HealthDyne, establish API connectivity, execute your first API request, and prepare your application to support end-to-end pharmacy workflows.

## What You Will Learn

By completing this guide, you will understand how to:

- Identify the pharmacy workflows relevant to your business.
- Complete the prerequisites for API integration.
- Understand API responses and downstream pharmacy processing.
- Retrieve and process mailbox events.
- Test successful and unsuccessful business scenarios.
- Prepare your integration for production deployment.
- Access HealthDyne's testing environment.

## Understanding Your Integration with HealthDyne

HealthDyne provides a collection of APIs that allow clients to integrate pharmacy services without directly managing the underlying pharmacy operations.

Depending on the services enabled for your organization, HealthDyne APIs support the following capabilities.

- Patient Management: Create, search, retrieve, and update patient profiles
- Prescription Management: Retrieve prescriptions, Receive prescription transfers (transfer to HD), and perform supported prescription updates
- Insurance Management: Add, retrieve, and manage patient coverage information
- Fill Request Management: Initiate medication fulfillment, update, cancel, retrieve fill request information
- Mailbox Events : Receive updates about prescription and fulfillment activities

## How the Integration Works

A typical HealthDyne integration involves three primary participants.

### Client Application

Your application initiates API requests, maintains information relevant to your business, and processes responses and notifications received from HealthDyne.

### HealthDyne API Platform

HealthDyne receives and validates API requests, applies supported business rules, communicates with pharmacy systems, and provides API responses and supported event notifications.

### Pharmacy Operations

The pharmacy systems perform the applicable activities, which may include prescription intake, processing, verification, order creation, fulfillment, and shipping.

## Before You Begin: Integration Prerequisites

Before making API requests, your organization must complete the required onboarding and integration setup.

#### Client Onboarding

Work with your designated HealthDyne Client Account team to establish your organization's integration requirements.

The onboarding process should confirm:

- The HealthDyne services your organization will use.
- The business workflows to be supported.
- The APIs required for those workflows.
- The environments required for development and testing.
- The authentication credentials needed to access the APIs.
- Any client-specific pharmacy configuration or business rules.
- The technical and operational contacts responsible for the integration.

Some functionality may depend on your organization's configuration and may not be enabled by default.

### API Environments

HealthDyne provides separate testing and production environments to support safe integration development and deployment.

#### Environment URLs

The following are the documented base URLs for the Pharmacy APIs.

<Table>
  <thead>
    <tr>
      <th>
        Environment
      </th>

      <th>
        URL
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Test / UAT
      </td>

      <td>
        [https://api.uat-healthdyne.com/v2](https://api.uat-healthdyne.com/v2)
      </td>
    </tr>

    <tr>
      <td>
        Production
      </td>

      <td>
        [https://api.healthdyne.com/v2](https://api.healthdyne.com/v2)

        `HealthDyne-Subscription-Key`
      </td>
    </tr>
  </tbody>
</Table>

#### API Authentication and Authorization

HealthDyne uses subscription-key authentication for access to its documented Pharmacy APIs.

Your HealthDyne integration team provides the subscription key required to authenticate your application's API requests.

#### Required Request Headers

Include the following headers when calling the applicable JSON-based Pharmacy APIs.

<Table>
  <thead>
    <tr>
      <th style={{ width: "24.1%" }}>
        Header
      </th>

      <th style={{ width: "39.1%" }}>
        Value
      </th>

      <th style={{ width: "36.7%" }}>
        Purpose
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        `HealthDyne-Subscription-Key`
      </td>

      <td>
        Your assigned subscription key
      </td>

      <td>
        Authenticates and authorizes access
      </td>
    </tr>

    <tr>
      <td>
        Accept
      </td>

      <td>
        `application/json`
      </td>

      <td>
        Indicates the expected response format
      </td>
    </tr>

    <tr>
      <td>
        Content-Type
      </td>

      <td>
        `application/json`
      </td>

      <td>
        Indicates JSON request content, when applicable
      </td>
    </tr>
  </tbody>
</Table>

Header requirements may vary by endpoint and HTTP method. Refer to the endpoint-specific API reference.

#### Handling API Credentials

To maintain a secure integration:

- Store credentials securely.
- Do not embed subscription keys directly in application source code.
- Do not expose subscription keys in client-side applications, URLs, or public repositories.
- Restrict access to authorized services and personnel.
- Use secure transport for all API calls.
- Follow your organization's approved credential management practices.

#### Authentication Errors

If an API request cannot be authenticated or authorized, HealthDyne may return an HTTP error such as 401 Unauthorized.

When troubleshooting authentication, verify:

- The request is sent to the correct environment.
- The subscription key is valid for that environment.
- The required authentication header is present.
- The API capability is enabled for your organization.

If the issue persists, contact your HealthDyne Client Account team.

## Understanding API Errors and Business Validation

HealthDyne APIs validate incoming requests against the applicable request schema and business requirements.

Errors generally fall into three categories.

#### Request Validation Errors

These occur when the submitted request does not satisfy API requirements.

Examples include:

- Missing mandatory fields.
- Invalid field formats.
- Unsupported field values.
- Invalid data structures.
- Incomplete request information.

Recommended client action: Review the request schema and correct the submitted information before retrying.

### Business Rule Errors

These occur when the request is structurally valid but cannot be processed because of the current business state or a workflow restriction.

Examples may include:

- A fill request cannot proceed due to prescription status.
- Insurance information does not satisfy the applicable requirement.
- An order is no longer eligible for cancellation.

Recommended client action: Review the business reason, evaluate the current entity status, and follow the workflow-specific recovery steps.

### System or Processing Errors

These occur when the application or a downstream pharmacy integration cannot complete an operation.

Examples include temporary service failures, downstream processing problems, or other technical issues.

Recommended client action: Determine whether the request was accepted before retrying, to avoid unintentionally creating duplicate operations.

###### Common HTTP Response Categories

| Response                  | General Meaning                                                     |
| ------------------------- | ------------------------------------------------------------------- |
| 200  OK                   | Request was handled successfully according to the endpoint contract |
| 204 No content            | Request was handled successfully according to the endpoint contract |
| 400 Bad Request           | Invalid request or failed validation                                |
| 401 Unauthorized          | Authentication or authorization failure                             |
| Co409 Conflict            | Conflicting or duplicate request, where supported                   |
| 500 Internal Server Error | Server-side processing failure                                      |

<br />

### Understanding the Pharmacy Integration Lifecycle

Understanding the Pharmacy Integration Lifecycle

After establishing connectivity, determine the business workflows your application needs to support.

A typical pharmacy integration may involve the following activities.

##### Step 1: Patient Setup

Use the Patient APIs to identify an existing patient or register a new patient.

Patient information will be required for subsequent prescription, coverage, and fill request activities.

##### Step 2: Insurance and Coverage Management (If applicable)

Use the applicable Insurance APIs to manage patient coverage information.

Coverage information may include primary, secondary, or additional coverage, depending on the integration and supported business rules.

##### Step 3: Prescription Intake or Transfer

A prescription must be available in HealthDyne before applicable prescription management or fulfillment actions can be performed.

Depending on your integration, prescriptions may arrive through supported electronic prescription intake processes or prescription transfer workflows.

Use the Prescription APIs and related workflow guides to retrieve prescription details and understand processing requirements.

##### Step 4: Initiate a Fill Request

When a prescription is eligible for fulfillment, the client can use the applicable Fill Request API to initiate the fulfillment process which creates order in the pharmacy system

The Fill Request may contain prescription identifiers, insurance information, and other supported fulfillment instructions. HealthDyne validates the request and performs the applicable downstream processing.

##### Step 5: Monitor Pharmacy Processing

A successfully submitted fill request may progress through additional pharmacy activities, such as verification, order processing, fulfillment, and shipping.

The progression depends on business rules, client configuration, and the current state of the prescription or order.

##### Step 6: Receive Status Updates

Use supported mailbox events and GET APIs to remain informed about prescription and fill request activities.

Clients should process these updates to maintain the appropriate status information within their applications.

For detailed instructions, refer to the Business Workflow Guides.

## Understanding Mailbox Events

HealthDyne provides mailbox capabilities to communicate supported prescription and fulfillment-related activities.

Mailbox events allow your application to detect relevant state changes without assuming the initial API response represents the final outcome of a business process.

#### Why Mailbox Events Are Important

Consider a client that initiates a medication fill request. The request may be accepted initially, but additional pharmacy processing is still required.

Mailbox events allow the client to identify supported milestones or outcomes, such as a verification result, fulfillment issue, shipment, or cancellation.

#### Types of Events

Depending on your integration, mailbox events may communicate:

Prescription-related activities

- Prescription received.
- Prescription transferred.
- Prescription discontinued.
- Prescription clarification&#x20;
- Refill or renewal ready.
- Prescription update completed or failed.

Fill request-related activities

- Fill request submitted.
- Fill request rejected.
- Prescription verified.
- Order shipped.
- Order canceled.
