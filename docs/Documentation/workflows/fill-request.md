---
title: Fill Request
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
# Fill Request:

See [Fill](ref:post_v2-fill) API reference for request message fields.

This API lets client define when the order needs to be initiated in HD system and also defines the number of prescription/scripts that needs to be consolidated in one order.

API field validation information in Appendix [Fill Request Fields](doc:fill-request-fields)

Client must send a Fill request with following details:

1. fillRequestKey: Unique key used to track each Fill Request.
2. scriptKeys: an array of scriptKey(s) sent in Script API and in a "Transferred" status.

![](https://files.readme.io/182e876-small-FillRequest.png)

### Server

##### Only https connections are accepted.

| REQUEST TYPE | ENDPOINT                       |
| :----------- | :----------------------------- |
| POST (Test)  | api.uat-healthdyne.com/v2/fill |
| POST (Prod)  | api.healthdyne.com/v2/fill     |

### Header

| Key                         | Value                  |
| :-------------------------- | :--------------------- |
| Accept                      | application/json       |
| Content-Type                | application/json       |
| HealthDyne-Subscription-Key | Provided by HealthDyne |

### Sample Fill Request

```json
{
	"fillRequestKey": "8a97815e-ef31-43ee-af87",
	"scriptKeys": [
		"e156daa5-1905-42c5-9e2e"
	],
	"shipping": {
		"address": {
			"line1": "500 Eagles Landin Dr",
			"line2": null,
			"line3": null,
			"city": "Lakeland",
			"state": "FL",
			"zipCode": "33810",
			"countryCode": "US"
		},
    "shippingCode": "UPS 1D",
    "saturdayDelivery": true,
    "signatureRequired": true
  }
}
```

# Status Events

Please see the [Fill Request](doc:mail-box#fill-request-status-events) status events under the [Mailbox](doc:mail-box) API guide for a detailed list of status events.

# Submitted Status

HealthDyne will create the order after receiving a Fill Request by sending create order command in the downstream pharmacy management system. Once the order has been successfully created, HealthDyne will generate a ‘submitted’ order status message and queues the event up for the client to retrieve it. See [Fill Request Submitted Status Event](doc:mail-box#submitted).

# RxVerified

A "RxVerified" event will be generated once a Pharmacist has completed PV1 and released the prescription for fulfillment. See [Fill Request RxVerified Status Event](doc:mail-box#rxverified).

# Rejected Status

If order creation errors/rejects; then Rejected event will be created. Possible reasons for system to reject order request include existing open orders for an Rx. See [Fill Request Rejected Status Event](doc:mail-box#rejected-1)

# RxIssue Status

When an Order is successfully created, and then one of the Rx is subsequently rejected by pharmacy (reason such as: Insurance reason/DUR/Pharmacy unable to read/understand the prescription)- then RxIssue event will be pushed. See [Fill Request RxIssue Event Status](doc:mail-box#rxissue)

# RxCancel Status

When a Rx or multiple Rx(s) in the order have been canceled pharmacy, HealthDyne will send an update at Rx level for each Rx in the order notifying of the canceled status. By default, unless order split has been configured for the client, the entire order will be cancelled when there is an issue with any of the Rx in the same order. Cancelled Rx that have not also been rejected due to "RxIssue" are available to be assigned to a new Fill Request without additional action via the Script API. See [Fill Request RxCancel Status Event](doc:mail-box#rxcancel)

# Shipped Status

Once the Rx has been shipped successfully by pharmacy, then send update for each Rx within the order will be sent to client. This event will be ‘Shipped’ event sent for each Rx. See [Fill Request Shipped Status Event](doc:mail-box#shipped)
