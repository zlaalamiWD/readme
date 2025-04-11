---
title: Insurance
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
# Insurance Plan Request:

See the [Insurance](ref:get_v2-patient-insurance) API reference for request message fields.

This API lets clients define and update insurance information in the HealthDyne system.

Use POST method to add/create an insurance plan and assign to an existing patientKey. Use the GET method to retrieve insurance plan information for a patient. The DELETE method can be used to set an insurance plan to inactive for a patient.

### Server

##### Only https connections are accepted.

| REQUEST TYPE                | ENDPOINT                                    |
| :-------------------------- | :------------------------------------------ |
| GET, POST, or DELETE (Test) | api.uat-healthdyne.com/v2/patient/insurance |
| GET, POST, or DELETE (Prod) | api.healthdyne.com/v2/patient/insurance     |

### Header

| Key                         | Value                  |
| :-------------------------- | :--------------------- |
| Accept                      | application/json       |
| Content-Type                | application/json       |
| HealthDyne-Subscription-Key | Provided by HealthDyne |

### Sample Insurance Plan GET Request

[https://api.uat-healthdyne.com/v2/patient/insurance?patientKey=ds76sa5765sad](https://api.uat-healthdyne.com/v2/patient/insurance?patientKey=ds76sa5765sad)

### Sample Get Insurance Plan Response

```json
{
  "patientKey": "ds76sa5765sad",
  "insurance":[
    {
      "planNumber":"209235",
      "bin": "123456",
      "groupId": "123456789",
      "pcn": "15948546",
      "personCode": "001",
      "relationshipCode": "1",
      "insuranceMemberID": "23456"
    },
    {
      "planNumber": "162311",
      "bin": "",
      "groupId": "ABCD123",
      "pcn": "",
      "personCode": "001",
      "relationshipCode": "1",
      "insuranceMemberID": "67844"
    }
  ]
}
```

Click here to see [Get Insurance Data Object](https://docs.healthdyne.com/v2.171/docs/insurance-request-fields#get-insurance-request-path-query-parameter)

# POST / Create

### Sample Insurance Plan POST Request

```json
{
  "patientKey": "ds76sa5765sad",
  "insurance": {
    "policyHolderId": "68945143",
    "bin": "123456", 
    "groupId": "123456789",
    "pcn": "15948546",
    "personCode": "1",
    "relationshipCode": "1"
    "insuranceMemberID": "67844"
  }
}
```

#### Successful Add Insurance Plan Response Message

```json
{
  "patientKey": "ds76sa5765sad",
  "planNumber": "209235",
  "message": "Plan added to patient profile."
}
```

Click here to see [Create Insurance Data Object](https://docs.healthdyne.com/v2.171/docs/insurance-request-fields#create-insurance-request-data-object)

# DELETE

### Sample DELETE insurance plan request

[https://api.uat-healthdyne.com/v2/patient/insurance?patientKey=ds76sa5765sad\&planNumber=209235](https://api.uat-healthdyne.com/v2/patient/insurance?patientKey=ds76sa5765sad\&planNumber=209235)

### Successful DELETE Insurance Plan Response Message

```json
{
  "patientKey": "ds76sa5765sad",
  "planNumber": "209235",
  "message": "Patient Insurance plan number is inactivated successfully"
}
```

Click here to see [Delete Insurance Data Object](https://docs.healthdyne.com/v2.171/docs/insurance-request-fields#/)