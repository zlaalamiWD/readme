---
title: Refill Prescription Request
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
# Refill Request

View the [Refill Request](ref:post_v1-refill) API Reference for detailed request body information.

This endpoint should be used to submit a refill request. The description below provides a management overview of the refill request message. Detailed descriptions of the entities contained within the request can be found in the Appendix section of this document as well as the API Reference.\
The Refill API is a client configurable API that accepts Prescription Refill and Consumer Data:

1. Member/Patient verification including allergies
2. Rx Number, GPI, NDC, Provider and Pharmacy information
3. Shipping information

### Server

| REQUEST TYPE | ENDPOINT                                                                                               |
| :----------- | :----------------------------------------------------------------------------------------------------- |
| Post (Test)  | [https://partner.UAT-WellDyne.com/v1/orders/refill](https://partner.UAT-WellDyne.com/v1/orders/refill) |
| Post (Prod)  | [https://partner.WellDyne.com/v1/orders/refill](https://partner.WellDyne.com/v1/orders/refill)         |

### Header

| Key                         | Value                  |
| :-------------------------- | :--------------------- |
| Accept                      | application/json       |
| Content-Type                | application/json       |
| HealthDyne-Subscription-Key | Provided by HealthDyne |

### Body

| Key           | Value                                |
| :------------ | :----------------------------------- |
| RefillId      | The unique refill ID from the client |
| CAG           | Members Plan-Group information       |
| Patient       | Person receiving prescription        |
| Prescriptions | Array of prescriptions               |
| Shipping      | Delivery address                     |

#### Sample Refill Request

```json
{
  "refillId": "123456789",
  "prescriptions": [
    {
      "rxNumber": "10493553",
      "gpi": null,
      "ndc": "00456045701"
    }
  ],
  "member": {
    "memberId": "ME1234571770",
    "firstName": "FDIFFF",
    "lastName": "14SEP2022032538555",
    "dateOfBirth": "1900-01-01T00:00:00.000Z"
  },
  "shipping": {
    "address": {
      "addressType": null,
      "addressName": null,
      "line1": "14SEP2022032538555",
      "line2": null,
      "line3": null,
      "city": "Lakeland",
      "state": "FL",
      "zipCode": "33810",
      "phoneNumber": null,
      "phoneExtension": null
    },
    "shippingCode": "POS 1C",
    "signatureRequired": false,
    "saturdayDelivery": false,
    "bulkShipment": false
  }
}
```

# Refill Response

The description below provides a management overview of the response message returned after transmission of a refill request message. Detailed descriptions of the entities contained within the response can be found in the Appendix section of this document as well as the API Reference.

| Code | Description                                                              |
| :--- | :----------------------------------------------------------------------- |
| 200  | Request accepted                                                         |
| 400  | Bad Request – typically incorrect message formatting                     |
| 401  | Unauthorized                                                             |
| 409  | Conflict – typically duplicate RefillId                                  |
| 422  | Unprocessable Entity – correctly formatted but unable to process request |
| 500  | Internal server error                                                    |

### Body

| Key             | Description                                        |
| :-------------- | :------------------------------------------------- |
| RefillId        | HealthDyne Guide used to uniquely identify message |
| RequestReceived | Echo of Request Received                           |

#### Sample Refill Response

```json
{
    "refillRequest": {
        "refillId": "fill_request_123456",
        "requestId": null,
        "prescriptions": [{
                "rxNumber": "11111111",
                "gpi": null,
                "ndc": "11111111111"
            }
        ],
        "member": {
            "memberId": "1304",
            "firstName": "First",
            "lastName": "Last",
            "dateOfBirth": "1999-01-01T00:00:00"
        },
        "shipping": {
            "address": null,
            "shippingCode": null,
            "signatureRequired": false,
            "saturdayDelivery": false,
            "bulkShipment": false
        }
    },
    "created": "2022-12-29T21:00:16.4508762Z",
    "success": false,
    "errorMessages": ["\u0027RequestId\u0027 must not be empty.", "The field value must Not be Blank and Maximum allowed \u003C 11 digits but greater than 9 digit value", "\u0027ShippingCode\u0027 must not be empty."]
}
```
