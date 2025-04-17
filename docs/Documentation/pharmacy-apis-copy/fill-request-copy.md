---
title: Fill Request
deprecated: false
hidden: true
metadata:
  robots: index
next:
  pages:
    - slug: mailbox-copy-1
      title: Mailbox
      type: basic
---
The Rx Fill API provides the ability to submit new prescription fill requests and to retrieve status messages for previously sent prescription fill requests.#

## Submit Fill Request

See [RxFill]() API reference for request message fields.

![](https://files.readme.io/10b333b9fe319a0bcefff7827b285ad51b27abbfd94eeb64c640b806b6c8341f-image.png)

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