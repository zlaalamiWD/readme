---
title: Fill Request
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Fill Request:

See [Fill](ref:post_v2-fill) API reference for request message fields.

This API lets client define when the order needs to be initiated in HD system and also defines the number of prescription/scripts that needs to be consolidated in one order. A client can also use the GET method of Fill Request to retrieve current status.

<br />

# Submit Fill Request

API field validation information in Appendix [Fill Request Fields](doc:fill-request-fields)

Client must send a Fill request with following details:

1. fillRequestKey: Unique key used to track each Fill Request.
2. scriptKeys: an array of scriptKey(s) sent in Script API and in a "Transferred" status.

![](https://files.readme.io/182e876-small-FillRequest.png)

<br />

#### Server

##### Only HTTPS connections are accepted.

| REQUEST TYPE | ENDPOINT                       |
| :----------- | :----------------------------- |
| POST (Test)  | api.uat-healthdyne.com/v2/fill |
| POST (Prod)  | api.healthdyne.com/v2/fill     |

#### Header

| Key                         | Value                  |
| :-------------------------- | :--------------------- |
| Accept                      | application/json       |
| Content-Type                | application/json       |
| HealthDyne-Subscription-Key | Provided by HealthDyne |

<br />

#### Sample Submit Fill Request

> [POST https://(ENDPOINT)/v2/fill](https://\(ENDPOINT\)/v2/fill)

#### Sample Submit Fill Request Body

```json
TBD
```

#### Sample Submit Fill Response

```json
TBD
```

# Get Fill Request Status

The GET Fill Request Status API lets clients retrieve the status and event summary for previously submitted Fill Requests.

#### Server

##### Only HTTPS connections are accepted.

| METHOD TYPE | ENDPOINT                                                                    |
| :---------- | :-------------------------------------------------------------------------- |
| GET (Test)  | api.uat-healthdyne.com/v2/FILL/fillRequest?fillRequestKey=\<fillRequestKey> |
| GET (Prod)  | api.healthdyne.com/v2/FILL/fillRequest?fillRequestKey=\<fillRequestKey>     |

#### Header

| Key                         | Value                  |
| :-------------------------- | :--------------------- |
| Accept                      | application/json       |
| Content-Type                | application/json       |
| HealthDyne-Subscription-Key | Provided by HealthDyne |

#### Sample GET Status Request

> [GET https://(ENDPOINT)/v2/fill/fillRequest?fillRequestKey=NewNSCP24FILLREQUEST987660102](https://\(ENDPOINT\)/v2/fill/fillRequest?fillRequestKey=NewNSCP24FILLREQUEST987660102)

This tells the API to query for fillRequestKey NewNSCP24FILLREQUEST987660102 and return relevant details.

#### Sample GET Status Response

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

The table below lists the potential response codes that can be received in response to a GET request.

| Code | Description                                              |
| :--- | :------------------------------------------------------- |
| 200  | Fill Request status details returned \| No records found |
| 400  | Bad Request – typically header is missing key            |
| 401  | Unauthorized                                             |
| 500  | Internal Server Error                                    |

# Cancel Fill Request

Once an order has been created in the HealthDyne system (using a Fill request), the Cancel API endpoint allows the client to cancel a fill request or specific script(s) within a Fill Request. **NOTE: The cancelation will be applied if the order has not been sent to our dispensing system for fulfillment.**

#### Server

##### Only HTTPS connections are accepted.

| REQUEST TYPE | ENDPOINT                                |
| :----------- | :-------------------------------------- |
| POST (Test)  | partner.uat-welldyne.com/v2/fill/cancel |
| POST (Prod)  | partner.welldyne.com/v2/fill/cancel     |

#### Sample Cancel Fill Request

> [POST https://(ENDPOINT)/v2/fill/cancel](https://\(ENDPOINT\)/v2/fill/cancel)

#### Sample Cancel Fill Request Body

```json
{
  "FillRequestKey": "FR178899",
  "ScriptKeys": [
    " 77351bb76d194f338c567b11ab8a789c"
  ],
  "CancelReason": "TEST"
}
```

#### Sample Cancel Fill Request Response

```json
{
    "fillRequestKey": "FR178899",
    "message": "Order for Fill request Key [FR178899] has been canceled"
}

```

# Update Fill Request

Once an order has been created in HD system (using a Fill request), the update API endpoint allows client to update shipping address or shipping code for previously submitted fill request. NOTE: The update will be applied as long as order has not been sent to our dispensing system for fulfillment.

#### Server

##### Only HTTPS connections are accepted.

| REQUEST TYPE | ENDPOINT                         |
| :----------- | :------------------------------- |
| PUT (Test)   | partner.uat-welldyne.com/v2/fill |
| PUT (Prod)   | partner.welldyne.com/v2/fill     |

<br />

#### Sample Update Fill Request

> [PUT https://(ENDPOINT)/v2/fill](https://\(ENDPOINT\)/v2/fill)

#### Sample Update Fill Request Body

```json
{
    "FillRequestKey": "NewNSCP24FILLREQUEST987660117",
    "Shipping": {
        "Address": {
            "Line1": "UpdateAgain1",
            "Line2": null,
            "Line3": null,
            "City": "LAKELAND",
            "State": "FL",
            "ZipCode": "33810",
            "CountryCode": "US",
            "ZipCodeFour": null
        },
        "ShippingCode": "UPS 2D",
       "SaturdayDelivery": false,
       "SignatureRequired": false
    }
}
```

#### Sample Update Fill Response

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

<br />

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