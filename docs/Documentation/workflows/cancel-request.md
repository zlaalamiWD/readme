---
title: Cancel Order
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
# Cancel Request

View the [Cancel Request](ref:post_v1-prescriptionrequest-cancel) API Reference for detailed request body information.

This endpoint should be used to submit a cancel request when a new prescription needs to be canceled. The prescription can be canceled before the dispensing process begins in the pharmacy. The description below provides a high-level overview of the request message. Detailed descriptions of the entities contained within the request can be found in the Appendix as well as the API Reference.\
The Cancel Request API is a client configurable API that accepts:

1. RequestID
2. Cancel reason

### Server

| REQUEST TYPE | ENDPOINT                                                                                                                         |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------- |
| Post (Test)  | [https://partner.UAT-WellDyne.com/v1/prescriptionrequest/cancel](https://partner.UAT-WellDyne.com/v1/prescriptionrequest/cancel) |
| Post (Prod)  | [https://partner.WellDyne.com/v1/prescriptionrequest/cancel](https://partner.WellDyne.com/v1/prescriptionrequest/cancel)         |

### Header

| Key                         | Value                  |
| :-------------------------- | :--------------------- |
| Accept                      | application/json       |
| Content-Type                | application/json       |
| HealthDyne-Subscription-Key | Provided by HealthDyne |

### Body

| Key          | Value                                                                   |
| :----------- | :---------------------------------------------------------------------- |
| RequestId    | The unique request ID from the client sent for new prescription request |
| CancelReason | Client defined reason for cancelation                                   |

#### Sample Cancel Request

```json
{
  "RequestId": "30MAR2023054843664"
  "CancelReason": "Cancel"
}
```

# Cancel Response

The description below provides a management overview of the response message returned after transmission of a cancel request message. Detailed descriptions of the entities contained within the response can be found in the Appendix section of this document as well as the API Reference.

| Code | Description                                                              |
| :--- | :----------------------------------------------------------------------- |
| 200  | Request accepted                                                         |
| 400  | Bad Request – typically incorrect message formatting                     |
| 401  | Unauthorized                                                             |
| 409  | Conflict – typically duplicate RequestId                                 |
| 422  | Unprocessable Entity – correctly formatted but unable to process request |
| 500  | Internal server error                                                    |

### Body

| Key             | Description                          |
| :-------------- | :----------------------------------- |
| RequestId       | ID used to uniquely identify message |
| RequestReceived | Echo of Request Received             |

#### Sample Cancel Response

```json
{
  "cancelRequest": {
    "requestId": "30MAR2023054843664",
    "cancelReason": "Cancel"
  },
  "receivedUtc": "2023-03-30T13:07:10.6198045Z",
  "Success": true,
  "errors": null
}
```
