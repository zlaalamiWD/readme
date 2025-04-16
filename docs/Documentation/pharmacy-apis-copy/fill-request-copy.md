---
title: Fill Request
deprecated: false
hidden: true
metadata:
  robots: index
---
# RxFill:

See [Fill](ref:post_v2-fill) API reference for request message fields.

The Rx Fill API provides the ability to submit new prescription fill requests and to retrieve status messages for previously sent prescription fill requests.

### Server

##### Only https connections are accepted.

| REQUEST TYPE | ENDPOINT                              |
| :----------- | :------------------------------------ |
| POST (Test)  | api.uat-healthdyne.com/v1/fillrequest |
| POST (Prod)  | api.healthdyne.com/v1/fillrequest     |

### Header

| Key                         | Value                  |
| :-------------------------- | :--------------------- |
| Accept                      | application/json       |
| Content-Type                | application/json       |
| HealthDyne-Subscription-Key | Provided by HealthDyne |

### RxFill Response codes

The below table lists the potential response codes that can be received in response to a POST request.

| Code | Description                                 |
| :--- | :------------------------------------------ |
| 200  | Message Received                            |
| 400  | Bad Request                                 |
| 409  | Message already exists (based on MessageId) |
| 500  | Internal Server Error                       |

### Sample RxFill

```json
{
  
  
  
  
}
```

# Cancel a Fill Request:

The Cancel Request API enables client systems to submit a cancellation request for an existing order. This API supports order-level cancellation when an order is no longer needed or was submitted in error.An order can only be canceled if it is in a cancelable state. If the order does not meet the criteria for cancelation (e.g., already processed or dispensed), the API will return an appropriate response indicating that the cancelation cannot be performed.

### Server

##### Only https connections are accepted.

| REQUEST TYPE | ENDPOINT                                  |
| :----------- | :---------------------------------------- |
| POST (Test)  | partner.uat-welldyne.com/v2/cancelrequest |
| POST (Prod)  | partner.welldyne.com/v2/cancelrequest     |

### Sample Cancel Fill Request

```json
{
  
  
}
```

<br />

```json
{
    "fillRequestKey": "NewNSCP24FILLREQUEST987660102",
    "submitted": [
        {
            "eventId": "116957",
            "eventDateUtc": "2024-03-27T16:22:17.760822Z",
            "scriptKeys": []
        }
    ],
    "rxVerified": [],
    "rxShipped": [],
    "rxIssue": [
        {
            "eventId": "116959",
            "eventDateUtc": "2024-03-27T16:25:35.333628Z",
            "scriptKey": "3081ccf283ed41b2977a7e67649f8374",
            "issueMessage": "REJECTED 533 HEALTHDYNE RX REJECTED - TEST FOR ORDER DETAIL"
        }
    ],
    "rxCanceled": [
        {
            "eventId": "116960",
            "eventDateUtc": "2024-03-27T16:30:56.077151Z",
            "scriptKey": "3081ccf283ed41b2977a7e67649f8374",
            "statusMessage": "ORDER CANCELED"
        }
    ],
    "rejected": []
}
```

# Fill Request Status Mailbox Events

Please see the [Fill Request](doc:mail-box#fill-request-status-events) status events under the [Mailbox](doc:mail-box) API guide for a detailed list of status events.

# Submitted Status

HealthDyne will create the order after receiving a Fill Request by sending create order command in the downstream pharmacy management system. Once the order has been successfully created, HealthDyne will generate a ‘submitted’ order status message and queues the event up for the client to retrieve it. See [Fill Request Submitted Status Event](doc:mail-box#submitted).

# Rejected Status

If order creation errors/rejects; then Rejected event will be created. Possible reasons for system to reject order request include existing open orders for an Rx. See [Fill Request Rejected Status Event](doc:mail-box#rejected-1)

# RxVerified

A "RxVerified" event will be generated once a Pharmacist has completed PV1 and released the prescription for fulfillment. See [Fill Request RxVerified Status Event](doc:mail-box#rxverified).

# RxShipped

Once the Rx has been shipped successfully by pharmacy, then send update for each Rx within the order will be sent to client. This event will be ‘Shipped’ event sent for each Rx. See [Fill Request Shipped Status Event](doc:mail-box#shipped)

# RxIssue

When an Order is successfully created, and then one of the Rx is subsequently rejected by pharmacy because there is an issue with the prescription (reason such as: Insurance reason/DUR/Pharmacy unable to read the prescription)- then RxIssue event will be pushed only for the prescription having an issue. See [Fill Request RxIssue Event Status](doc:mail-box#rxissue)

# RxCancel

When a Rx or multiple Rx(s) in the order have been canceled pharmacy, HealthDyne will send an update at Rx level for each Rx in the order notifying of the canceled status. By default, unless order split has been configured for the client, the entire order will be cancelled when there is an issue with any of the Rx in the same order. Cancelled Rx that have not also been rejected due to "RxIssue" are available to be assigned to a new Fill Request without additional action via the Script API. See [Fill Request RxCancel Status Event](doc:mail-box#rxcancel).