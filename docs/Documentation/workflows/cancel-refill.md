---
title: Cancel Refill
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
# Cancel Refill Request

View the [Cancel Refill](ref:post_v1-refill-cancelrefill) API Reference for detailed request body information.

This endpoint should be used to submit a cancel request when a refill prescription needs to be canceled. The description below provides a management overview of the request message. Detailed descriptions of the entities contained within the request can be found in the Appendix section of this document as well as the API Reference.\
The Cancel Request API is a client configurable API that accepts:

1. RequestID
2. Cancel reason

### Server

| REQUEST TYPE | ENDPOINT                                                                                                                                                                                                                          |
| :----------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Post (Test)  | [api.uat-healthdyne.com/v1/refill/cancelrefill](https://api.uat-healthdyne.com/v1/refill/cancelrefill) or [partner.UAT-WellDyne.com/v1/refill/cancelrefill](https://partner.UAT-WellDyne.com/v1/refill/cancelrefill/cancelRefill) |
| Post (Prod)  | [api.healthdyne.com/v1/refill/cancelrefill](https://api.healthdyne.com/v1/refill/cancelrefill) or [partner.WellDyne.com/v1/refill/cancelrefill](https://partner.WellDyne.com/v1/refill/cancelrefill)                              |

### Header

| Key                         | Value                  |
| :-------------------------- | :--------------------- |
| Accept                      | application/json       |
| Content-Type                | application/json       |
| HealthDyne-Subscription-Key | Provided by HealthDyne |

### Body

| Key          | Required / Optional | Value                                                        |
| :----------- | :------------------ | :----------------------------------------------------------- |
| RequestId    | Required            | The unique refill ID from the client sent for refill request |
| CancelReason | Required            | Client defined reason for cancelation                        |

#### Sample Refill Cancellation Request

```json
{
  "refillId": "QARefillNidhi74"
  "cancelReason": "client canceled"
}
```

# Cancel Response

The description below provides a management overview of the response message returned after transmission of a cancel refill request message. Detailed descriptions of the entities contained within the response can be found in the Appendix section of this document as well as the API Reference.

| Code | Description                                                              |
| :--- | :----------------------------------------------------------------------- |
| 200  | Request accepted                                                         |
| 400  | Bad Request – typically incorrect message formatting                     |
| 401  | Unauthorized                                                             |
| 409  | Conflict – typically duplicate RefillId                                  |
| 422  | Unprocessable Entity – correctly formatted but unable to process request |
| 500  | Internal server error                                                    |

### Body

| Key             | Description                          |
| :-------------- | :----------------------------------- |
| RefillId        | ID used to uniquely identify message |
| RequestReceived | Echo of Request Received             |

#### Sample Cancel Response

```json
{
  "cancelRefill": {
    "RefillId": "QARefillNidhi74",
    "cancelReason": "client canceled"
  },
  "receivedUtc": "2023-03-30T13:07:10.6198045Z",
  "Success": true,
  "errors": null
}
```
