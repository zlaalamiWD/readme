---
title: Payment Cards
excerpt: >-
  This section provides an overview of the patient payment card features and
  functionality.
deprecated: false
hidden: true
metadata:
  robots: index
---
# Payment Card Request:

See the Payment Card API reference for request message fields.

This API lets clients add and update patient payment cards information in the HealthDyne system. A client can also use the GET method of patient payment request to retrieve patient payment card information.

Use POST method to add a payment card to the patient profile  and PUT method to update existing patient payment card details.

# Get Patient Payment card

Once a patient payment card has been registered successfully, the GET Patient Payment Card API allows clients to retrieve Payment Card details (active details) from HD pharmacy system using PatientKey.

### Server

##### Only HTTPS connections are accepted.

| METHOD TYPE | ENDPOINT                                            |
| :---------- | :-------------------------------------------------- |
| GET (Test)  | api.uat-healthdyne.com/v2/\<patientKey>/paymentcard |
| GET (Prod)  | api.healthdyne.com/v2/\<patientKey>/paymentcard     |

### Header

| Key                         | Value                       |
| :-------------------------- | :-------------------------- |
| Accept                      | application/json (optional) |
| HealthDyne-Subscription-Key | Provided by HealthDyne      |

#### Sample GET Patient Request

`GET https://api.uat-healthdyne.com/v2/TestreadPatient171/paymentcard`

#### Sample GET Patient Payment Card Response

```json
{
    "patientKey": "TestreadPatient171",
    "cards": [
        {
            "cardType": 1,
            "cardNumber": "*********************1111",
            "cardHolderFirstName": "Test",
            "cardHolderLastName": "Partient",
            "cardExpireMonth": 3,
            "cardExpireYear": 2027,
            "defaultCard": true
        }
    ]
}
```

Click here to see [Get Patient Payment Card Response Data Object](https://docs.healthdyne.com/docs/patient-payment-card-fields#response-object)

The below table lists the potential response codes that can be received in response to a GET request.

| Code | Description                            |
| :--- | :------------------------------------- |
| 200  | Patient Payment Cards details returned |
| 204  | No record returned for search          |
| 401  | Unauthorized                           |
| 500  | Internal Server Error                  |

<br />

# Add Patient Payment card

The POST Patient Payment Card API allows clients to add Payment Card details to HD pharmacy system.

### Server

##### Only HTTPS connections are accepted.

| METHOD TYPE | ENDPOINT                              |
| :---------- | :------------------------------------ |
| GET (Test)  | api.uat-healthdyne.com/v2/paymentcard |
| GET (Prod)  | api.healthdyne.com/v2/paymentcard     |

### Header

| Key                         | Value                  |
| :-------------------------- | :--------------------- |
| Accept                      | application/json       |
| Content-type                | application/json       |
| HealthDyne-Subscription-Key | Provided by HealthDyne |

#### Sample POST Patient Payment Card Request

```json
{
    "patientKey": "TestreadPatient171",
    "returnUrl" : "www.callbackurl.com"
}
```

#### Sample GET Patient Payment Card Response

```json
{
    "returnUrl": "https://cardcenter.qa-healthdyne.com/AddCard/c440977f-dba1-4d5f-aa5f-2862cd81"
}
```

Click here to see [Add Patient Payment Card Response Data Object](https://docs.healthdyne.com/docs/add-patient-payment-card-fields)

The below table lists the potential response codes that can be received in response to a GET request.

| Code | Description                               |
| :--- | :---------------------------------------- |
| 200  | Patient Payment Cards details returned    |
| 400  | Patient Key provided does not exist in HD |
| 401  | Unauthorized                              |
| 500  | Internal Server Error                     |
