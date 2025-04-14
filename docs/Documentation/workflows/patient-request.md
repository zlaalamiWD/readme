---
title: Patient
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
# Patient Request:

See the [Patient](ref:post_v2-patient) API reference for request message fields.

This API lets clients define and update patient information in the HealthDyne system.

Use POST method to add/create a patient and PUT method to update existing patient details.

API field validation information in Appendix [Patient Request Fields](doc:patient-request-fields)

# Get Patient

Once a patient has been registered successfully, the GET Patient API allows clients to retrieve patient details (active details) from HD pharmacy system using PatientKey.

### Server

##### Only https connections are accepted.

| REQUEST TYPE | ENDPOINT                             |
| :----------- | :----------------------------------- |
| GET (Test)   | partner.uat-welldyne.com/v2/Patient? |
| GET (Prod)   | partner.welldyne.com/v2/Patient?     |

#### Sample GET Request

> [https://partner.uat-welldyne.com/v2/Patient?PatientKey=TestreadPatient171](https://partner.uat-welldyne.com/v2/Patient?PatientKey=TestreadPatient171)

This tells the API to query for PatientKey TESTREADPATIENT171 and return relevant details.

# GET Patient Response

The below table lists the potential response codes that can be received in response to a GET request.

| Code | Description                   |
| :--- | :---------------------------- |
| 200  | Patient details returned      |
| 400  | No record returned for search |
| 401  | Unauthorized                  |
| 500  | Internal Server Error         |

#### Sample Status Response

```json
{
    "patientKey": "TESTPATIENT",
    "firstName": "TEST",
    "lastName": "TESTREADPATIENT17",
    "gender": "F",
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
            "contactAddress": "3233731379"
        }
    ],
    "externalMedications": [
        "00002445385",
        "99207012010"
    ],
    "pregnancyIndicator": "N",
    "allergies": [
        "CEPHALOSPORINS",
        "SALICYLATES"
    ]
}
```

# Find Patient

The Find Patient API (GET method) allows clients to lookup patientKey in HD system using following parameters: First Name, Last Name, DOB and Zip code. NOTE: The parameter fields should be separated with an ampersand (&) when using the API endpoint. If a match is found, HD returns matching patientKey to retrieve details using Get Patient API.

### Server

##### Only https connections are accepted.

| REQUEST TYPE | ENDPOINT                                  |
| :----------- | :---------------------------------------- |
| GET (Test)   | partner.uat-welldyne.com/v2/Patient/find? |

#### Sample GET Request

> [https://partner.uat-welldyne.com/v2/Patient/find?FirstName=ABC\&LastName=XYZ\&Birthdate=1981-01-01\&ZipCode=80017](https://partner.uat-welldyne.com/v2/Patient/find?FirstName=ABC\&LastName=XYZ\&Birthdate=1981-01-01\&ZipCode=80017)

# Find Patient Response

The below table lists the potential response codes that can be received in response to a GET Find patient request.

| Code | Description                   |
| :--- | :---------------------------- |
| 200  | Patient details returned      |
| 400  | No record returned for search |
| 401  | Unauthorized                  |
| 500  | Internal Server Error         |

#### Sample Status Response

```json
{
    "patientKey": [
        "TestreadPatient17"
    ],
    "firstName": "TEST",
    "lastName": "TESTLASTNAME",
    "birthDate": "1997-02-03",
    "zipCode": "33810"
}
```

# Get Patient Scripts/prescriptions

The "Get Patient script/Prescription" endpoint allows retrieval of all scripts associated with a specific patient key. If no prescriptions are found for the provided patient key, the endpoint will return a 200 status with the message "No record found."

### Server

##### Only https connections are accepted.

| REQUEST TYPE | ENDPOINT                                                                |
| :----------- | :---------------------------------------------------------------------- |
| GET (Test)   | api.uat-healthdyne.com/v2/patient/prescription?patientKey=\<patientKey> |
| GET (Prod)   | api.healthdyne.com/v2/patient/prescription?patientKey=\<patientKey>     |

### Header

| Key                         | Value                  |
| :-------------------------- | :--------------------- |
| Accept                      | application/json       |
| Content-Type                | application/json       |
| HealthDyne-Subscription-Key | Provided by HealthDyne |

#### Sample GET Request

> \<[https://api.uat-healthdyne.com/v2/patient/prescription?patientKey=4e1e76ca-520f-4e7a-a6c7-d837a9e3cece](https://api.uat-healthdyne.com/v2/patient/prescription?patientKey=4e1e76ca-520f-4e7a-a6c7-d837a9e3cece)

This tells the API to query for patientKey 4e1e76ca-520f-4e7a-a6c7-d837a9e3cece  and return relevant details.

# GET Patient Scripts/prescriptions Response

The below table lists the potential response codes that can be received in response to a GET request.

| Code | Description                                   |
| :--- | :-------------------------------------------- |
| 200  | Prescription details returned                 |
| 204  | No Prescription found                         |
| 400  | Bad Request – typically header is missing key |
| 401  | Unauthorized                                  |
| 500  | Internal Server Error                         |

#### Sample Status Response

```json
{
    "scriptKeys": [
        "0ed290dbb11224ea0f9e27"
    ]
}
```

<br />

# Post Patient

### Server

##### Only https connections are accepted.

| REQUEST TYPE       | ENDPOINT                          |
| :----------------- | :-------------------------------- |
| POST or PUT (Test) | api.uat-healthdyne.com/v2/patient |
| POST or PUT (Prod) | api.healthdyne.com/v2/patient     |

### Header

| Key                         | Value                  |
| :-------------------------- | :--------------------- |
| Accept                      | application/json       |
| Content-Type                | application/json       |
| HealthDyne-Subscription-Key | Provided by HealthDyne |

### Sample Patient Request

```json
{
  "patient": {
    "patientKey":"12389990",
    "firstName": "JANE",
    "lastName": "DOE",
    "birthDate": "1956-03-02",
    "gender": "F",
    "address": {
      "addressType": "HOME",
      "line1": "100 Rivers Edge Dr.",
      "line2": null,
      "line3": null,
      "city": "Temple Terrace",
      "state": "FL",
      "zipCode": "02155",
      "countryCode": "US",
      "defaultAddress":True
    },
    "contact": {
      "contactType": "PHONE",
      "contactAddress": "5712345678"
    },
    "allergies": ["Amoxicillin"],
    "externalMedications": [
      {
        "ndc": "00045049660",
        "startDate": "2022-03-02",
        "endDate": "2022-04-02"
      }
    ]
  }
}
```

# Successful Response Messages

#### Patient Added

```json
{
  "patientKey": "12389990",
  "message": "The patient was added."
}
```

#### Patient Updated

```json
{
  "patientKey": "12389990",
  "message": "The patient was updated."
}
```