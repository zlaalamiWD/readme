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
# Add Payment Card Request:

This API lets clients define and update patient information in the HealthDyne system. A client can also use the GET method of Patient Request to retrieve patient.

Use POST method to add/create a patient and PUT method to update existing patient details.

# Get Patient

Once a patient has been registered successfully, the GET Patient API allows clients to retrieve patient details (active details) from HD pharmacy system using PatientKey.

### Server

##### Only HTTPS connections are accepted.

| METHOD TYPE | ENDPOINT                                                   |
| :---------- | :--------------------------------------------------------- |
| GET (Test)  | api.uat-healthdyne.com/v2/patient?patientkey=\<patientKey> |
| GET (Prod)  | api.healthdyne.com/v2/patient?patientkey=\<patientKey>     |

### Header

| Key                         | Value                  |
| :-------------------------- | :--------------------- |
| Accept                      | application/json       |
| Content-Type                | application/json       |
| HealthDyne-Subscription-Key | Provided by HealthDyne |

#### Sample GET Patient Request

`GET https://api.uat-healthdyne.com/v2/patient?patientkey=TestreadPatient171`

Click here to see [GET Patient Request Query Data](https://docs.healthdyne.com/docs/patient-request-fields#query-parameter)

#### Sample GET Patient Response

```json
{
  "patientKey": "TESTPATIENT",
  "firstName": "TEST",
  "lastName": "TESTREADPATIENT17",
  "gender": "F",
  "epostPatientNum": 727793,
  "patientLanguage": "ENG",
  "birthDate": "1997-02-03",
  "healthCondition": [],
  "address": [
    {
      "line1": "123 Main St",
      "line2": null,
      "line3": null,
      "city": "LAKELAND",
      "state": "FL",
      "zipCode": "33810",
      "countryCode": "US",
      "addressType": "HOME",
      "defaultAddress": true
    },
    {
      "line1": "678 Main St",
      "line2": null,
      "line3": null,
      "city": "LAKELAND",
      "state": "FL",
      "zipCode": "33810",
      "countryCode": "US",
      "addressType": "HOME",
      "defaultAddress": false
    }
  ],
  "contact": [
    {
      "contactType": "HOME PHONE",
      "contactAddress": "3233731379",
      "emailAddress": "testemail@domain.com"
    }
  ],
  "externalMedications": [
    "00002445385",
    "99207012010"
  ],
  "identification": {
    "patientId": "DR987EF007",
    "patientIdCode": "02",
    "patientIdExpiration": "2030-01-15"
  },
  "pregnancyIndicator": "N",
  "allergies": [
    "CEPHALOSPORINS",
    "SALICYLATES"
  ]
}
```

Click here to see [Get Patient Response Data Object](https://docs.healthdyne.com/docs/patient-request-fields#response-object)

The below table lists the potential response codes that can be received in response to a GET request.

| Code | Description                   |
| :--- | :---------------------------- |
| 200  | Patient details returned      |
| 400  | No record returned for search |
| 401  | Unauthorized                  |
| 500  | Internal Server Error         |
