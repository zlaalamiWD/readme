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
Central Fill is a pharmacy fulfillment model that streamlines the dispensing and shipping of prescriptions by routing orders from healthcare providers or pharmacies to a centralized facility. This centralized approach enables faster, more accurate, and cost-effective prescription processing at scale allowing pharmacies to focus on patient care while leveraging advanced logistics and automation.

HealthDyne's Central Fill solution supports this model through a nationwide fulfillment infrastructure, ensuring timely delivery and regulatory compliance across all 50 states and U.S. territories.  To support seamless integration with your pharmacy or healthcare systems, HealthDyne offers a powerful and robust RESTful, JSON-based API. The Central Fill API provides direct access to our fulfillment platform, enabling your organization to automate and scale prescription processing with speed, reliability, and control.

**Key Features:**

* Prescription Fill/Refill Management: Submit new prescription fill or refill requests via the RxFill API
* Real-Time Status Tracking: Retrieve current fill request statuses, including acknowledgment, shipment updates.
* Flexible Cancellations: Cancel fill requests when needed to maintain control over order flow and minimize medication waste.

Get started by adding reviewing the [RxFill](), [Cancel](), and [Mailbox]() request documentation.

# Fulfillment Workflows

## Submit a Rxfill Request (Fill/Refill) :

The RxFill Workflow is a critical process for submitting and tracking prescription fill or refill requests through HealthDyne’s Central Fill API. The steps below outline how your system should interact with the RxFill and Mailbox APIs for proper end-to-end order management.

1. Use the RxFill API to create a fill or refill order [RxFill API Guide]()
2. Retrieve and Acknowledge Events [Mailbox API Guide]()
   1. Use the GET method on the Mailbox API to retrieve current events.

> 📘 Important: The status messages are not considered delivered and removed from the mailbox until the receipt of the message is acknowledged by using a POST method with the batchId as a query parameter. Hence, another status request should not be submitted until the previous status response is acknowledged.