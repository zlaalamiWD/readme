---
title: Mailbox
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
# Status Request

View the [MailBox](ref:post_v2-mailbox) API Reference for detailed request body information.

This endpoint should be used to obtain the status of Script and/or Fill requests previously submitted. No request body is required.\
HealthDyne employs a mailbox style order status reporting methodology. Therefore, when an order has a status update, the status message is delivered to the partner’s mailbox. This status message remains in the mailbox until the status message is retrieved by the partner and receipt of the message is acknowledged.
A maximum of 100 status messages will be returned with a single request. Each request will have the same batch id and messages until marked as delivered. To receive the next set of messages, the current batch id need to be confirmed as delivered through the POST call. Multiple requests may be necessary to receive all outstanding status messages. Please refer to the Status Codes returned to determine if all messages have been retrieved.
Note, the status messages are not considered delivered and removed from the mailbox until the receipt of the message is acknowledged by using a POST method with the batchId as a query parameter. Hence, another status request should not be submitted until the previous status response is acknowledged.

### Server

##### Only https connections are accepted.

| REQUEST TYPE       | ENDPOINT                              |
| :----------------- | :------------------------------------ |
| GET or Post (Test) | partner.uat-healthdyne.com/v2/mailbox |
| GET or Post (Prod) | partner.healthdyne.com/v2/mailbox     |

### Header

| Key                         | Value                  |
| :-------------------------- | :--------------------- |
| Accept                      | application/json       |
| Content-Type                | application/json       |
| HealthDyne-Subscription-Key | Provided by HealthDyne |

# GET Request

#### Sample GET Request

partner.uat-healthdyne.com/v2/mailbox?messageCount=10

This tells the API to only respond with 10 messages. The default message count is 100 messages. The Mailbox only allows 100 messages to be pulled at a time.

# GET Status Response

The below table lists the potential response codes that can be received in response to a GET request.

| Code | Description                                                                    |
| :--- | :----------------------------------------------------------------------------- |
| 200  | All messages delivered                                                         |
| 204  | No messages                                                                    |
| 206  | Max allowed messages delivered - submit another request for remaining messages |
| 400  | Bad Request – typically header is missing key                                  |
| 401  | Unauthorized                                                                   |
| 500  | Internal Server Error                                                          |

#### Sample Status Response

```json
{
    "batchId": "6be689c3-3306-4a75-b0d3-a769be788c99",
    "count": 2,
    "approximateRemainingCount": 0,
    "messageList": [
        {
            "eventId": "1000003",
            "eventDateUtc": "2023-05-08T19:14:55.22818Z",
            "eventType": "RXTRANSFER",
            "scriptKey": "1000001",
            "status": "Transferred",
            "statusMessage": "The Rx has been transferred successfully",
            "detail": {
                "patientKey": "1000002",
                "rxNumber": "RX12345"
            }
        },
        {
            "eventId": "1000005",
            "eventDateUtc": "2023-05-08T19:15:55.22818Z",
            "eventType": "RXTRANSFER",
            "scriptKey": "1000004",
            "status": "Rejected",
            "statusMessage": "The file [http://somedomain.com/files/12548.png] could not be retrieved.",
            "detail": {
                "patientKey": "1000002",
                "rxNumber": null
            }
        }
    ]
}
```

# POST Request

#### Sample POST Request

> `<https://partner.uat-healthdyne.com/v2/mailbox?batchId=6be689c3-3306-4a75-b0d3-a769be788c99>`

#### Sample POST Response

```json
{ 
    "batchId": "6be689c3-3306-4a75-b0d3-a769be788c99", 
    "status": "MARKED DELIVERED", 
    "eventId": [ 
        "1000003", 
        "1000005"
    ] 
}
```

# Status Event Types:

# Rx Status Events

## RxReceived *(eRx, fax, phone intake only)*

A RxReceived event will be produced when HealthDyne successfully receives an eRx from Surescripts for a registered patient.

```json
{
  "eventId": "1000003",
  "eventDateUtc": "2023-05-08T19:14:55.22818Z",
  "eventType": "RXSTATUS",
  "patientKey": "1000002",
  "scriptKey": "1000001",
  "status": "Received", 
  "statusMessage": "A new prescription has been received",   
  "detail": {
    "reason":null
  }
}
```

## RxDiscontinued

RxDiscontinued events will be generated anytime an Rx has been discontinued by the pharmacy. The discontinued status means the Rx is no longer valid and cannot be used for any future Fill requests.

```json
{
  "eventId": "1000003",
  "eventDateUtc": "2023-05-08T19:14:55.22818Z",
  "eventType": "RXSTATUS",
  "scriptKey": "1000001",
  "status": "Discontinued",
  "statusMessage": "The prescription has been discontinued by pharmacy",
  "detail": {
    "reason":"Rx Transferred out of pharmacy"
  }
}
```

## RxRefillReady

RxRefillReady event will be generated anytime an Rx is ready for refill. NOTE: The event is configurable to be turned on/off to be received by client.

```json
{
    "eventId": "118081",
    "eventDateUtc": "2024-05-01T06:01:25.527727Z",
    "eventType": "RXSTATUS",
    "status": "RefillReady",
    "statusMessage": "The prescription is ready for refill.",
    "scriptKey": "f324f6d0894f4abdba6b252158a2313d",
    "patientKey": "AB1890001",
    "detail": {
        "reason": null
    }
}
```

## RxOverdue

RxOverdue event will be generated anytime an Rx is overdue for a refill. NOTE: The event is configurable to be turned on/off to be received by client.

```json
{
    "eventId": "118087",
    "eventDateUtc": "2024-05-05T06:02:19.771002Z",
    "eventType": "RXSTATUS",
    "status": "Overdue",
    "statusMessage": "The prescription is overdue for refill",
    "scriptKey": "f324f6d0894f4abdba6b252158a2313d",
    "patientKey": "AB1890001",
    "detail": {
        "reason": null
    }
}
```

## RxRenewalReady

RxRenewalReady event will be generated anytime an Rx is ready for prescriber to renew (Rx has exhausted all fills or when Rx has expired). The event is configurable to be turned on/off to be received by client.

```json
{
    "eventId": "118079",
    "eventDateUtc": "2024-04-30T15:01:50.250195Z",
    "eventType": "RXSTATUS",
    "status": "RenewalReady",
    "statusMessage": "The prescription needs to be renewed.",
    "scriptKey": "2fbb38d736b74d83bccf13c2e98ad3a4",
    "patientKey": "AB1890001",
    "detail": {
        "reason": null
    }
}
```

## Transferred *(Rx Transfer only)*

Once the PNG or XML has been successfully downloaded, HealthDyne will store the file and create the prescription record in HealthDyne's pharmacy management system. Once the Rx has been created, HealthDyne will generate a ‘Transferred’ event.

#### Sample "Transferred" event

```json
{
    "eventId": "1000003",
    "eventDateUtc": "2023-05-08T19:14:55.22818Z",
    "eventType": "RXTRANSFER",
    "scriptKey": "1000001",
    "status": "Transferred",
    "statusMessage": "The Rx has been transferred successfully",
    "detail": {
        "patientKey": "1000002",
        "rxNumber": "RX12345"
    }
}
```

## Rejected *(During Rx Transfer)*

When a RxTransfer request can't be validated, HealthDyne generates a rejection event with status "Rejected". RxTransfers will be rejected if the PNG or XML download was unsuccessful after two (2) failed attempts.

#### Sample "Rejected" event

```json
{
    "eventId": "1000005",
    "eventDateUtc": "2023-05-08T19:15:55.22818Z",
    "eventType": "RXTRANSFER",
    "scriptKey": "1000004",
    "status": "Rejected",
    "statusMessage": "The file [http://somedomain.com/files/12548.png] could not be retrieved."
}
```

# Fill Request Status Events

## Submitted

HealthDyne will create the order after receiving a Fill Request by sending create order command in the downstream pharmacy management system. Once the order has been successfully created, HealthDyne will generate a ‘submitted’ order status message and queues the event up for the client to retrieve it.

#### sample "Submitted" event

```json
{
    "eventId": "1000007",
    "eventDateUtc": "2023-05-08T19:16:55.22818Z",
    "eventType": "FILLREQUEST",
    "fillRequestKey": "1000006",
    "status": "Submitted",
    "statusMessage": "The order is being processed",
    "detail": {
        "orderNumber": "12345",
        "fillNumber": 0
    }
}
```

## RxVerified

A "RxVerified" event will be generated once a Pharmacist has completed PV1 and released the prescription for fulfillment.

> 📃 NOTE: This is at Rx level (i.e. for each Rx)

#### sample "RxVerified" event

```json
{
    "eventId": "1000008",
    "eventDateUtc": "2023-05-08T19:17:55.22818Z",
    "eventType": "FILLREQUEST",
    "fillRequestKey": "1000006",
    "status": "RxVerified",
    "statusMessage": "The Rx has been verified by the pharmacist (PV1)",
    "detail": {
        "orderNumber": "12345",
        "scriptKey": "1000004",
        "fillNumber": 0,
        "dispenseDrug": {
            "dispenseNDC": "780000001290",
            "dispenseDrugName": "Tylenol",
            "daySupply": 30,
            "prescribedQuantity": 60,
            "labelDirections": "TAKE 1 TABLET DAILY",
            "dosageForm": "TABLET",
            "drugStrength": "200",
            "drugStrengthUOM": "Mg"
        }
    }
}
```

## Rejected

If order creation errors/rejects; then Rejected event will be created. Possible reasons for system to reject order request include existing open orders for an Rx or when one of the Rx is discontinued.

#### Sample "Rejected" event

```json
{
    "eventId": "1000012",
    "eventDateUtc": "2023-05-08T19:19:55.22818Z",
    "eventType": "FILLREQUEST",
    "fillRequestKey": "1000010",
    "status": "Rejected",
    "statusMessage": "An open order exists for one or more RXs"
}
```

## RxIssue

When an Order is successfully created, and then one of the Rx is subsequently rejected by pharmacy because it has issue (reason such as: Insurance reason/DUR/Pharmacy unable to read the prescription)- then RxIssue event will be pushed only for Rx that has an issue.

> 📃 NOTE: This is at Rx level (i.e. for each Rx)

#### Sample "RxIssue" event

```json
{
    "eventId": "1000016",
    "eventDateUtc": "2023-05-08T19:20:55.22818Z",
    "eventType": "FILLREQUEST",
    "fillRequestKey": "1000013",
    "status": "RxIssue",
    "statusMessage": "HEALTHDYNE RX REJECTED",
    "detail": {
        "orderNumber": "56789",
        "scriptKey": "1000003",
        "fillNumber": 0,
        "issueMessage": "REJECTED 533 HEALTHDYNE RX REJECTED",
        "ClaimRejectCode": "388",
        "ClaimRejectDescription": "PRIOR AUTHORIZATION SUPPORTING DOCUMENT IS NOT USED FOR THIS TRANSACTION CODE"
    }
}
```

The 'statusMessage' field will show the pharmacy defined reason for the RxIssue status. Please see the Status Message table for a list of issues.

|                                                                |                                               |
| :------------------------------------------------------------- | :-------------------------------------------- |
| PATIENT PROFILE                                                | CREDIT CARD                                   |
| NDC NOT COVERED                                                | DOCTOR DENIED/NON-RESPONSE                    |
| ORDER ISSUE                                                    | PRIOR AUTHORIZATION REQUIRED                  |
| HIGH COPAY                                                     | ALLERGY/MEDICAL CONDITION INFO                |
| PAYMENT REQUIRED                                               | COPAY ASSISTANCE ENROLLMENT MANDATORY         |
| RPH NEEDS MEMBER CONSULTATION                                  | SHORT-TERM ANTIBIOTICS MUST BE FILLED LOCALLY |
| SPECIALTY MEDICATION MUST BE FILLED THROUGH SPECIALTY PHARMACY | HEALTHDYNE RX REJECTED                        |
| INSURANCE ISSUE                                                |                                               |

Additional details will be provided via free form text notes from the pharmacy in the 'issueMessage' field. For example, "Clarification required from prescriber"

> 📃 The 'issueMessage' field is a free form text field and can vary in response.

## RxCancel

When a Rx or multiple Rx(s) in the order have been canceled pharmacy, HealthDyne will send an update at Rx level for each Rx in the order notifying of the canceled status. By default, unless order split has been configured for the client, the entire order will be cancelled when there is an issue with any of the Rx in the same order. Cancelled Rx that have not also been rejected due to "RxIssue" are available to be assigned to a new Fill Request without additional action via the Script API.

> 📃 NOTE: This is at Rx level (i.e. for each Rx)

#### Sample "RxCancel" event

```json
{
  "eventId": "1000017",
  "eventDateUtc": "2023-05-08T19:20:55.22818Z",
  "eventType": "FILLREQUEST",
  "fillRequestKey": "1000013",
  "status": "RxCanceled",
  "statusMessage": "Order canceled",
  "detail": {
    "orderNumber": "56789",
    "scriptKey": "1000003"
  }
}
```

## Shipped

Once the Rx has been shipped successfully by pharmacy, then send update for each Rx within the order will be sent to client. This event will be ‘Shipped’ event sent for each Rx.

> 📃 NOTE: This is at Rx level (i.e. for each Rx)

#### Sample "Shipped" event

```json
{
  "eventId": "1000009",
  "eventDateUtc": "2023-05-08T19:18:55.22818Z",
  "eventType": "FILLREQUEST",
  "fillRequestKey": "1000006",
  "status": "RxShipped",
  "statusMessage": "The Rx has been shipped",
  "detail": {
    "orderNumber": "12345",
    "scriptKey": "1000004",
    "shipments": [{
        "Cost": 4.88,
        "Weight": 0.6,
        "DaysSupply": "45",
        "TrackingUrl": "https://tools.usps.com/go/TrackConfirmAction?tLabels=?92001122222222222",
        "DispensedQty": "90",
        "ShipmentCode": "POS 1C",
        "ShipmentDate": "2024-04-04T19:30:36Z",
        "TrackingNumber": "122222222222"
      }],
    "fillNumber": 2,
    "RemainingRefills": "2",
    "RefillByDate": "2024-04-29T06:00:00Z"
  }
}

```

##