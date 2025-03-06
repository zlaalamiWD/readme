---
title: New Prescription Request
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
# Prescription Request

View the [Prescription Request](ref:post_v1-prescriptionrequest) API Reference for detailed request body information.

This endpoint should be used to submit a new prescription request. The description below provides a management overview of the request message.  Detailed descriptions of the entities contained within the request can be found in the Appendix section of this document as well as the API Reference.\
The Prescription API is a client configurable API that accepts Order and Patient/Customer Data to include:

1. Patient/Customer verification including allergies, External medications
2. Insurance verification including policy holder ID, relationship code, BIN, group ID, PCN
3. GPI, NDC, Provider and Pharmacy information
4. Shipping information\
   The API allows for multiple Member and Prescription requests to be received from a client. Once the order request is received and validated in the HealthDyne system, a patient profile with a unique Member ID is created with HealthDyne which is shared with the client for future new order/refill requests.

### Server

| REQUEST TYPE | ENDPOINT                                                                                                           |
| :----------- | :----------------------------------------------------------------------------------------------------------------- |
| Post (Test)  | [https://partner.UAT-WellDyne.com/v1/prescriptionrequest](https://partner.UAT-WellDyne.com/v1/prescriptionrequest) |
| Post (Prod)  | [https://partner.WellDyne.com/v1/prescriptionrequest](https://partner.WellDyne.com/v1/prescriptionrequest)         |

### Header

| Key                         | Value                  |
| :-------------------------- | :--------------------- |
| Accept                      | application/json       |
| Content-Type                | application/json       |
| HealthDyne-Subscription-Key | Provided by HealthDyne |

### Body

| Key            | Value                                 |
| :------------- | :------------------------------------ |
| RequestId      | The unique request ID from the client |
| LineofBusiness | Members Plan-Group information        |
| Patient        | Person receiving prescription         |
| Prescriptions  | Array of prescriptions                |
| Shipping       | Delivery address                      |

#### Sample Prescription Request

```json
{
  "requestid": "RID0244",
  "lineofBusiness": "LOB",
  "patient": {
    "memberid": "",
    "firstName": "First",
    "lastName": "Last",
    "birthDate": "01/01/1960",
    "Address": {
      "addresstype": "HOME",
      "line1": "123 Main Street",
      "line2": "",
      "line3": "",
      "city": "Centennial",
      "phone": "7201234567",
      "state": "CO",
      "zipCode": "80016",
      "defaultaddress": true
    },
    "contact": {
      "contacttype": "PHONE",
      "contactaddress": "7201234567"
    },
    "gender": "M",
    "allergies": [
      "Amoxicillin"
    ],
    "externalMedications": [
      {
        "ndc": "00045049660",
        "notes": "TYLENOL      TAB 325MG",
        "startDate": "01/03/2021",
        "endDate": "01/12/2022"
      }
    ]
  },
  "prescriptions": [
    {
      "ndc": "13533070501",
      "ndcName": "PROLASTIN-C INJ 1000MG",
      "quantity": 30
    }
  ],
  "shipping": {
    "shippingCode": "POS 1C",
    "signatureRequired": false,
    "saturdayDelivery": false,
    "address": {
      "addressType": "Home",
      "line1": "123 Main Street",
      "line2": "",
      "line3": "",
      "city": "Centennial",
      "phone": null,
      "state": "CO",
      "zipCode": "80016"
    },
    "notificationEmail": "email@healthdyne.com"
  }
}
```

# Prescription Response

The description below provides a management overview of the response message returned after transmission of a prescription request message. Detailed descriptions of the entities contained within the response can be found in the Appendix section of this document as well as the API Reference.

| Code | Description                                                              |
| :--- | :----------------------------------------------------------------------- |
| 200  | Request accepted                                                         |
| 400  | Bad Request – Typically incorrect message formatting                     |
| 401  | Unauthorized                                                             |
| 409  | Conflict – Typically Duplicate RequestId                                 |
| 422  | Unprocessable Entity – Correctly formatted but unable to process request |
| 500  | Internal Server Error                                                    |

#### Sample Prescription Response

```json JSON
{
  "prescriptionRequest": {
    "requestId": "RID0244",
    "lineOfBusiness": "LOB",
    "patient": {
      "memberId": "",
      "firstName": "First",
      "lastName": "Last",
      "birthDate": "1960-01-01T00:00:00",
      "address": {
        "addressType": "HOME",
        "addressName": null,
        "line1": "123 Main Street",
        "line2": "",
        "line3": "",
        "city": "Centennial",
        "state": "CO",
        "zipCode": "80016",
        "defaultAddress": true,
        "contact": null
      },
      "contact": {
        "contactType": "PHONE",
        "contactAddress": "7201234567"
      },
      "gender": "M",
      "allergies": [
        "Amoxicillin"
      ],
      "externalMedications": [
        {
          "ndc": "00045049660",
          "notes": "TYLENOL      TAB 325MG",
          "startDate": "2021-03-01T00:00:00",
          "endDate": "2022-12-01T00:00:00"
        }
      ]
    },
    "prescriptions": [
      {
        "rxNumber": null,
        "drugName": null,
        "ndc": "13533070501",
        "providerNpi": "",
        "pharmacyNpi": "",
        "quantity": 30
      }
    ],
    "shipping": {
      "address": {
        "addressType": "Home",
        "addressName": null,
        "line1": "123 Main Street",
        "line2": "",
        "line3": "",
        "city": "Centennial",
        "state": "CO",
        "zipCode": "80016",
        "defaultAddress": false,
        "contact": null
      },
      "shippingCode": "POS 1C",
      "saturdayDelivery": false,
      "signatureRequired": false,
      "bulkShipment": false
    }
  },
  "receivedUtc": "2022-06-22T19:26:44.5170817Z",
  "success": true,
  "errors": null
}
```
