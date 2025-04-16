---
title: Central Fill APIs
deprecated: false
hidden: true
metadata:
  robots: noindex
next:
  pages:
    - slug: fill-request-copy
      title: Fill Request
      type: basic
---
The Central Fill API is a powerful and robust RESTful, JSON-based API designed to seamlessly integrate with your pharmacy or healthcare systems. It provides access to HealthDyne's national fulfillment infrastructure, enabling your organization to scale prescription fulfillment with speed, reliability, and compliance.

**Key Features:**

* Nationwide Delivery: Ship medications to all 50 U.S. states and US territories.
* Prescription Fill/Refill Management: Submit fill or refill requests through RxFill API.
* Real-Time Status Tracking: Retrieve current fill request statuses, including shipment  updates.
* Request Cancellations: Cancel a fill request when necessary, ensuring flexibility and control.

Get started by adding reviewing the [RxFill](doc:patient-request), [Cancel](doc:script-rxtransfer-request), and [Mailbox](doc:fill-request) request documentation.

# Fulfillment Workflows

## Submit a Rxfill Request (Fill/Refill) :

The RxFill Workflow is a critical process for submitting and tracking prescription fill or refill requests through HealthDyne’s Central Fill API. The steps below outline how your system should interact with the RxFill and Mailbox APIs for proper end-to-end order management.

1. Use the RxFill API to create a fill or refill order [RxFill API Guide](https://docs.healthdyne.com/v2.17/docs/patient-request)
2. Retrieve and Acknowledge Events [Mailbox API Guide](https://docs.healthdyne.com/v2.17/docs/mail-box)

* Use the GET method on the Mailbox API to retrieve current events.

  Important: After successfully retrieving and processing these events, you must call the DELETE method on the same mailbox event(s) to mark them as acknowledged. This step prevents duplicate processing and ensures accurate system state synchronization.

Note: Failure to acknowledge mailbox events with the DELETE method may result in repeated delivery of the same events.