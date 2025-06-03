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

See [Fill](ref:put_v2-fill) API reference for request message fields.

This API lets client define when the order needs to be initiated in HealthDyne system and also defines the number of prescriptions/scripts that need to be consolidated in one order. A client can also use the GET method of Fill Request to retrieve current status.

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

`GET https://api.uat-healthdyne.com/v2/fill/fillRequest?fillRequestKey=FillPatientSample1404`

Click here to see [GET Fill Request Query Data](https://docs.healthdyne.com/docs/fill-request-fields#query-parameter)

#### GET Status Response Samples

> 📘 NOTE: Sample for a Single-line Rx.

```json
{
  "fillRequestKey": "ccdd5fd46a714cc09bc679f0365b2",
  "submitted": [
    {
      "eventId": "295955",
      "eventDateUtc": "2025-04-15T09:12:20.913021+00:00",
      "scriptKeys": [
        "SampleScriptKey007"
      ]
    }
  ],
  "rxVerified": [
    {
      "eventId": "295965",
      "eventDateUtc": "2025-04-15T09:16:48.804578+00:00",
      "scriptKey": "24388f1b53c04b0a89534056c311ece6326",
      "verifiedDate": null,
      "statusMessage": "The Rx has been verified by the pharmacist (PV1)"
    }
  ],
  "rxShipped": [
    {
      "eventId": "295985",
      "eventDateUtc": "2025-04-17T09:19:53.417176+00:00",
      "scriptKey": "24388f1b53c04b0a89534056c311ece6326",
      "shipmentDate": "2025-04-17T06:00:02Z",
      "trackingNumber": "7548253"
    }
  ],
  "rxIssue": [],
  "rxCanceled": [],
  "rejected": [],
  "renewed": [
    {
      "eventId": "191171",
      "eventDateUtc": "2025-06-02T11:23:23.248905Z",
      "scriptKeys": [
        "SampleScriptKey007"
      ]
    }
  ]
}
```

> 📘 NOTE: Sample for a Multiline Rx.

```json
{
  "fillRequestKey": "FillPatientSample1404",
  "submitted": [
    {
      "eventId": "295955",
      "eventDateUtc": "2025-04-15T09:12:20.913021+00:00",
      "scriptKeys": [
        "SampleScriptKey1",
        "SampleScriptKey2"
      ]
    }
  ],
  "rxVerified": [
    {
      "eventId": "288774",
      "eventDateUtc": "2025-04-11T18:43:07.995451Z",
      "scriptKey": "TestScriptKey1401",
      "verifiedDate": null,
      "statusMessage": "The Rx has been verified by the pharmacist (PV1)"
    },
    {
      "eventId": "2887749",
      "eventDateUtc": "2025-04-11T18:453:07.995451Z",
      "scriptKey": "TestScriptKey14091",
      "verifiedDate": null,
      "statusMessage": "The Rx has been verified by the pharmacist (PV1)"
    }
  ],
  "rxShipped": [],
  "rxIssue": [
    {
      "eventId": "289773",
      "eventDateUtc": "2025-04-15T09:30:57.585214+00:00",
      "scriptKey": "TestScriptKey1401",
      "issueMessage": "REJECTED 533 HEALTHDYNE RX REJECTED - "
    }
  ],
  "rxCanceled": [
    {
      "eventId": "288784",
      "eventDateUtc": "2025-04-11T18:50:00.418881Z",
      "scriptKey": "TestScriptKey1401",
      "statusMessage": "Cancelled"
    },
    {
      "eventId": "2887864",
      "eventDateUtc": "2025-04-11T18:50:00.418881Z",
      "scriptKey": "TestScriptKey14091",
      "statusMessage": "Cancelled"
    }
  ],
  "rejected": [
    {
      "eventId": "156270",
      "eventDateUtc": "2025-02-18T13:36:57.776842Z",
      "scriptKeys": [],
      "statusMessage": "RX: 10524420 found on OPEN order with External ID: NULL; "
    }
  ],
  "renewed": [
    {
      "eventId": "191171",
      "eventDateUtc": "2025-06-02T11:23:23.248905Z",
      "scriptKeys": [
        "SampleScriptKey007",
        "SampleScriptKey2"
      ]
    }
  ]
}
```

Click here to see [Get Fill Request Data Object](https://docs.healthdyne.com/docs/fill-request-fields#response-object)

The table below lists the potential response codes that can be received in response to a GET request.

| Code | Description                                              |
| :--- | :------------------------------------------------------- |
| 200  | Fill Request status details returned \| No records found |
| 400  | Bad Request – typically the header is missing key        |
| 401  | Unauthorized                                             |
| 500  | Internal Server Error                                    |

***

# Submit Fill Request

API field validation information in Appendix [Fill Request Fields](https://docs.healthdyne.com/docs/fill-request-fields#fill-request-data-object)

Client must send a Fill request with following details:

1. fillRequestKey: Unique key used to track each Fill Request.
2. scriptKeys: an array of scriptKey(s) sent in Script API and in a "Transferred" status.

![](https://files.readme.io/182e876-small-FillRequest.png)

#### Server

##### Only HTTPS connections are accepted.

| METHOD TYPE | ENDPOINT                       |
| :---------- | :----------------------------- |
| POST (Test) | api.uat-healthdyne.com/v2/fill |
| POST (Prod) | api.healthdyne.com/v2/fill     |

#### Header

| Key                         | Value                  |
| :-------------------------- | :--------------------- |
| Accept                      | application/json       |
| Content-Type                | application/json       |
| HealthDyne-Subscription-Key | Provided by HealthDyne |

#### Sample Submit Fill Request (single insurance per fill request)

`POST https://api.uat-healthdyne.com/v2/fill`

#### Sample Submit Fill Request Body

> 📘 NOTE: This request only allows to pass one insurance object per fill request

```json
{
  "fillRequestKey": "FillPatientSample1404",
  "scriptKeys": [
    "TestScriptKey1404"
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
  },
  "insurance": {
    "planNumber": "58189",
    "secondaryPlanNumber": "78654",
    "tertiaryPlanNumber": "58200",
    "coPay": "32.50",
    "transactionNumber": "pi_305qndABfMSbKdKQ0NA1r4L5",
    "personCode": "001",
    "relationshipCode": "02"
  }
}
```

Click here to see [Submit Fill Request Data Object](https://docs.healthdyne.com/docs/fill-request-fields#request-object)

#### Sample Submit Fill Response

```json
{
    "fillRequestKey": "FillPatientSample1404",
    "message": "The fill request was accepted"
}
```

Click here to see [Submit Fill Response Data Object](https://docs.healthdyne.com/docs/fill-request-fields#response-object-1)

<br />

#### Sample Submit Fill Request (multiple insurances per fill request)

`POST https://api.uat-healthdyne.com/v2/fill/fillrequest`

#### Sample Submit Fill Request Body

> 📘 NOTE: This request allows to pass one insurance object per script  in the fill request

```json
{
  "fillRequestKey": "Fill26",
  "scriptsKeys": [
    {
      "scriptsKey": "sc258",
      "patientInsurance": {
        "planNumber": "12349",
        "secondaryPlanNumber": "12348",
        "tertiaryPlanNumber": "12347",
        "clientItemCost": 123.11,
        "clientDispenseFee": 124.11,
        "clientOtherFee": 125.2,
        "clientCoPay": 126.66
      }
    },
    {
      "scriptsKey": "sc258testing",
      "patientInsurance": {
        "planNumber": "12369",
        "secondaryPlanNumber": "12389",
        "tertiaryPlanNumber": "12347",
        "clientItemCost": 123.11,
        "clientDispenseFee": 124.11,
        "clientOtherFee": 125.2,
        "clientCoPay": 126.66
      }
    }
  ],
  "shipping": {
    "address": {
      "line1": "16JUL20241206204211",
      "line2": "16JUL20241206204213",
      "line3": "16JUL20241206204213",
      "city": "LAKELAND",
      "state": "FL",
      "zipCode": "33810",
      "countryCode": "US"
    },
    "shippingCode": "POS 1M",
    "saturdayDelivery": false,
    "signatureRequired": false
  },
  "transactionNumber": "asvbbnh"
}
```

Click here to see [Submit Fill Request Data Object](https://docs.healthdyne.com/docs/fill-request-fields#request-object)

#### Sample Submit Fill Response

```json
{
    "fillRequestKey": "Fill26",
    "message": "The fill request was accepted"
}
```

Click here to see [Submit Fill Response Data Object](https://docs.healthdyne.com/docs/fill-request-fields#response-object-1)

***

# Update Fill Request

Once an order has been created in HealthDyne system (using a Fill request), the update API endpoint allows client to update shipping address or shipping code for a previously submitted fill request. NOTE: The update will be applied as long as order has not been sent to our dispensing system for fulfillment.

#### Server

##### Only HTTPS connections are accepted.

| METHOD TYPE | ENDPOINT                       |
| :---------- | :----------------------------- |
| PUT (Test)  | api.uat-healthdyne.com/v2/fill |
| PUT (Prod)  | api.healthdyne.com/v2/fill     |

#### Sample Update Fill Request

`PUT https://api.uat-healthdyne.com/v2/fill`

#### Sample Update Fill Request Body

```json
{
  "fillRequestKey": "FillPatientSample1404",
  "scriptKeys": [
    "TestScriptKey1404"
  ],
  "shipping": {
    "address": {
      "line1": "UpdateAgain1",
      "line2": null,
      "line3": null,
      "city": "LAKELAND",
      "state": "FL",
      "zipCode": "33810",
      "countryCode": "US"
    },
    "shippingCode": "POS 1C",
    "saturdayDelivery": false,
    "signatureRequired": false
  }
}
```

Click here to see [Update Fill Request Data Object](https://docs.healthdyne.com/docs/fill-request-fields#request-object-1)

#### Sample Update Fill Response

```json
{
    "fillRequestKey": "FillPatientSample1404",
    "message": "The fill update request was accepted"
}
```

Click here to see [Update Fill Response Data Object](https://docs.healthdyne.com/docs/fill-request-fields#response-object-2)

<br />

***

# Cancel Fill Request

Once an order has been created in the HealthDyne system (using a Fill request), the Cancel API endpoint allows the client to cancel a fill request or specific script(s) within a Fill Request. **NOTE: The cancelation will be applied if the order has not been sent to our dispensing system for fulfillment.**

#### Server

###### Only HTTPS connections are accepted.

| METHOD TYPE | ENDPOINT                              |
| :---------- | :------------------------------------ |
| POST (Test) | api.uat-healthdyne.com/v2/fill/cancel |
| POST (Prod) | api.healthdyne.com/v2/fill/cancel     |

#### Sample Cancel Fill Request

`POST https://api.uat-healthdyne.com/v2/fill/cancel`

#### Sample Cancel Fill Request Body

```json
{
  "fillRequestKey": "FillPatientSample1404",
  "scriptKeys": [
    "TestScriptKey1404"
  ],
  "cancelReason": "Cancelled"
}
```

Click here to see [Cancel Fill Request Data Object](https://docs.healthdyne.com/docs/fill-request-fields#request-object-2)

#### Sample Cancel Fill Request Response

```json
{
    "fillRequestKey": "FillPatientSample1404",
    "message": "Prescription fill for [TestScriptKey1404] under Fill request [FillPatientSample1404] has been canceled."
}
```

Click here to see [Cancel Response Data Object](https://docs.healthdyne.com/docs/fill-request-fields#response-object-3)

# Renewal Request:

See [Renewal](ref:put_v2-fill) API reference for request message fields.

This API lets the client initiate an outreach a request to the Physician for a new prescription on behalf of the patient. The API validates that the client has received a Proactive Renewal mail box event and requests that the client get approval from the patient for us to outreach to their physician.

# Submit Renewal Request

API field validation information in Appendix [Renewal Request Fields](https://docs.healthdyne.com/docs/fill-request-fields#renewal-request-data-object)

Client must send a Renewal request with following details:

1. fillRequestKey: Unique key used to track each Renewal Request.
2. scriptKeys: an array of scriptKey(s) sent in Script API and in a "Transferred" status.

#### Server

##### Only HTTPS connections are accepted.

| METHOD TYPE | ENDPOINT                                      |
| :---------- | :-------------------------------------------- |
| POST (Test) | api.uat-healthdyne.com/v2/fill/renewalrequest |
| POST (Prod) | api.healthdyne.com/v2/fill/renewalrequest     |

#### Header

| Key                         | Value                  |
| :-------------------------- | :--------------------- |
| Accept                      | application/json       |
| Content-Type                | application/json       |
| HealthDyne-Subscription-Key | Provided by HealthDyne |

#### Sample Submit Renewal Request

`POST https://api.uat-healthdyne.com/v2/fill/renewalrequest`

#### Sample Submit Renewal Request Body

```json
{
  "fillRequestKey": "RenewalRequest01",
  "scriptKeys": [
    {
      "scriptKey": "ScRenewalEnd12",
      "patientInsurance": {
        "planNumber": "59253",
        "secondaryPlanNumber": "59254",
        "tertiaryPlanNumber": "59255"
      }
    },
    {
      "scriptKey": "ScRenewalEnd13",
      "patientInsurance": {
        "planNumber": "59254",
        "secondaryPlanNumber": "59255",
        "tertiaryPlanNumber": "59253"
      }
    }
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
    }
  }
}
```

Click here to see [Submit Renewal Request Data Object](https://docs.healthdyne.com/docs/fill-request-fields#request-object)

#### Sample Submit Fill Response

```json
{
    "fillRequestKey": "RenewalRequest01",
    "message": "The renewal request was accepted"
}
```

Click here to see [Submit Renewal Response Data Object](https://docs.healthdyne.com/docs/fill-request-fields#renewal-response-object)

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

When a Rx or multiple Rx(s) in the order have been canceled pharmacy, HealthDyne will send an update at Rx level for each Rx in the order notifying of the canceled status. By default, unless order split has been configured for the client, the entire order will be canceled when there is an issue with any of the Rx in the same order. Cancelled Rx that have not also been rejected due to "RxIssue" are available to be assigned to a new Fill Request without additional action via the Script API. See [Fill Request RxCancel Status Event](doc:mail-box#rxcancel).

# Renewed Status

HealthDyne will create the order after receiving a Renewal Request by sending create order command in the downstream pharmacy management system. Once the order has been successfully created, HealthDyne will generate a ‘renewed’ order status message and queues the event up for the client to retrieve it. See [Renewal Request Submitted Status Event](doc:mail-box#renewed).