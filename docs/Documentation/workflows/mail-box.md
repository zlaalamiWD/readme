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
A maximum of 100 status messages will be returned with a single request. Multiple requests may be necessary to receive all outstanding status messages. Please refer to the Status Codes returned to determine if all messages have been retrieved.
Note, the status messages are not considered delivered and removed from the mailbox until the receipt of the message is acknowledged by using a POST method with the batchId as a query parameter. Hence, another status request should not be submitted until the previous status response is acknowledged.

### Server

##### Only https connections are accepted.

| REQUEST TYPE       | ENDPOINT                          |
| :----------------- | :-------------------------------- |
| GET or Post (Test) | api.uat-healthdyne.com/v2/mailbox |
| GET or Post (Prod) | api.healthdyne.com/v2/mailbox     |

### Header

| Key                         | Value                  |
| :-------------------------- | :--------------------- |
| Accept                      | application/json       |
| Content-Type                | application/json       |
| HealthDyne-Subscription-Key | Provided by HealthDyne |

# GET Request

#### Sample GET Request

> `<https://api.uat-healthdyne.com/v2/mailbox?messageCount=10>`

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

#### Sample Status Response *(RxTransfer)*

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

#### Sample Status Response *(RxClarified)*

```json
{
  "batchId": "ba205118-d0b2-403b-912a-acace449baea",
  "count": 1,
  "approximateRemainingCount": 1,
  "messageList": [
    {
      "eventId": "306794",
      "eventDateUtc": "2025-05-13T20:31:22.300632+00:00",
      "eventType": "RXSTATUS",
      "status": "Clarified",
      "statusMessage": "TEST TEST",
      "scriptKey": "fbbf557039844ba681e197d3831ebcfe",
      "patientKey": "TPNS0025UAT237test3",
      "detail": {
        "reason": null
      }
    }
  ]
}
```

# POST Request

#### Sample POST Request

> `<https://api.uat-healthdyne.com/v2/mailbox?batchId=6be689c3-3306-4a75-b0d3-a769be788c99>`

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
        "reason": null
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
        "reason": "Rx Transferred out of pharmacy"
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

## RxClarified

RxClarifiied events are generated when an Rx has a clarified prescription note. The event candidate is identified when an Rx has a clarified prescription note and no previous event generation.

#### Sample "Clarified" event

```json
{
  "eventId": "306794",
  "eventDateUtc": "2025-05-13T20:31:22.300632+00:00",
  "eventType": "RXSTATUS",
  "status": "Clarified",
  "statusMessage": "TEST TEST",
  "scriptKey": "fbbf557039844ba681e197d3831ebcfe",
  "patientKey": "TPNS0025UAT237test3",
  "detail": {
    "reason": null
  }
}
```

## Routed

When fax is successfully transferred to pharmacy, We send mailbox event and update the Routed status in HealthDyne System.

#### Sample "Routed" event

```json
{
	"eventId": "213258",
	"eventDateUtc": "2025-07-28T12:11:29.594001Z",
	"eventType": "RXTRANSFER",
	"status": "Routed",
	"statusMessage": "The script has been routed successfully.",
	"scriptKey": "RX-2024-001",
	"detail": {
		"patientKey": "PAT-2024-001",
		"rxNumber": "10552281",
		"receivingPharmacy": "HealthCare Plus Pharmacy"
	}
}
```

## Failed Routing

When fax is not transferred to pharmacy even after trying 3 attempts, We send mailbox event and update the FailedRouting status in HealthDyne System.

#### Sample "Failed Routing" event

```json
{
	"eventId": "213258",
	"eventDateUtc": "2025-07-28T12:11:29.594001Z",
	"eventType": "RXTRANSFER",
	"status": "Failed Routing",
	"statusMessage": "The Script routing has failed.",
	"scriptKey": "RX-2024-001",
	"detail": {
		"patientKey": "PAT-2024-001",
		"rxNumber": "10552281",
		"receivingPharmacy": "HealthCare Plus Pharmacy",
		"issueMessage": "An unexpected error seems to have occurred. Please contact our support team if the problem persists"
	}
}
```

<br />

# Fill Request Status Events

## Submitted

HealthDyne will create the order after receiving a Fill Request by sending create order command in the downstream pharmacy management system. Once the order has been successfully created, HealthDyne will generate a ‘submitted’ order status message and queues the event up for the client to retrieve it.\
**Note:** scriptKey can contain multiple scriptKey separated by comma.

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
       "scriptKey": "SampleScriptKey1,SampleScriptKey2",
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
        "claimRejectCode": "388",
        "claimRejectDescription": "PRIOR AUTHORIZATION SUPPORTING DOCUMENT IS NOT USED FOR THIS TRANSACTION CODE"
    }
}
```

The 'statusMessage' field will show the pharmacy defined reason for the RxIssue status. Please see the Status Message table for a list of issues.

| Issue Message Examples List 1                                  | Issue Message Examples List 2                 |
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
    "scriptKey": "1000003",
    "fillNumber": 0,
    "orderCanceledReasonCode": "19",
    "orderCanceledReasonDesc": "There is an issue with your address or your medication is cold chain and requires a non-PO Box address. Please review and confirm your address details."
  }
}
```

<br />

> 📃 NOTE: below is the list of expected order canceled reason codes with their description
>
> | Code | Description                                        |
> | :--- | :------------------------------------------------- |
> | 1    | Short Term Out of Stock                            |
> | 2    | Long Term Out of Stock                             |
> | 3    | Non-Formulary Items                                |
> | 4    | Invalid Insurance Information/Cannot Process Claim |
> | 5    | Non-Contracted Pharmacy                            |
> | 6    | Prior Authorization                                |
> | 7    | Quantity/Day Supply Limit                          |
> | 8    | Refill Too Soon                                    |
> | 9    | Product Not Covered                                |
> | 10   | DUR Clarification/Rx Clarification                 |
> | 11   | Allergy Issue                                      |
> | 12   | Duplicate or Newer Rx for Same Med/GPI             |
> | 13   | Non-Matching Patient Information                   |
> | 14   | Item Entry Error                                   |
> | 15   | Patient Copay exceeds their Codal Threshold        |
> | 16   | Rx Discontinued                                    |
> | 17   | Patient Request                                    |
> | 18   | Medication Needs Secondary Insurance               |
> | 19   | Address Issue                                      |

Once the Rx has been shipped successfully by pharmacy, an update is sent for each Rx within the order. This event will be a ‘Shipped’ event sent for each Rx. For example, if an order has 2 RXs, you will receive 2 shipped messages.

## Shipped

Once the Rx has been shipped successfully by pharmacy, an update is sent for each Rx within the order. This event will be  a ‘Shipped’ event sent for each Rx. For example, if an order has 2 RXs, you will receive 2 shipped messages.

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
        "shipments": [
            {
                "Cost": 4.88,
                "Weight": 0.6,
                "DaysSupply": "45",
                "TrackingUrl": "https://tools.usps.com/go/TrackConfirmAction?tLabels=?92001122222222222",
                "DispensedQty": "90",
                "ShipmentCode": "POS 1C",
                "ShipmentDate": "2024-04-04T19:30:36Z",
                "TrackingNumber": "122222222222"
            }
        ],
        "fillNumber": 2,
        "RemainingRefills": "2",
        "RefillByDate": "2024-04-29T06:00:00Z"
    }
}
```

> ❗️ NOTE: the address attribute only return null for now

## RxCopay

Once the Rx has been adjudicated successfully by pharmacy, an update is sent for each RX with adjudication summary and insurance used to adjudicate the order. This event will be  a ‘RxCopay’ event sent for each Rx. For example, if an order has 2 RXs, you will receive 2 RxCopay messages.

#### Sample "RxCopay" event

```json
{
    "eventId": "176357",
    "eventDateUtc": "2025-04-15T12:26:20.613448Z",
    "eventType": "FILLREQUEST",
    "status": "RxCopay",
    "statusMessage": "The prescription has been adjudicated.",
    "fillRequestKey": "FILL85ea1e519bd146ed89b96f3f0066ff",
    "detail": {
        "orderNumber": "7546472",
        "scriptKey": "993c869261204aecbea1a4a84a58329408ff6129da5243a79b",
        "fillNumber": 0,
        "adjudicationSummary": {
            "claimStatus": "PAID",
            "claimType": "B1",
            "claimAdjRunDate": "2025-04-15T12:21:10.367Z",
            "copayAmount": 14.77,
            "clientCoPay": 126.36
        },
        "insurance": {
            "bin": "4341",
            "pcn": "341",
            "payorPlanNumber": "58146",
            "memberId": "341",
            "policyHolderId": "341",
            "personCode": "341",
            "relationshipCode": "1"
        }
    }
}
```