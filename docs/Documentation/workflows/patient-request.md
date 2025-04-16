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

Click here to see [GET Patient Request Query Data](https://docs.healthdyne.com/v2.171/docs/patient-request-fields#get-patient-request)

#### Sample GET Patient Response

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

Click here to see [Get Fill Response Data Object](https://docs.healthdyne.com/v2.171/docs/patient-request-fields#response-object)

The below table lists the potential response codes that can be received in response to a GET request.

| Code | Description                   |
| :--- | :---------------------------- |
| 200  | Patient details returned      |
| 400  | No record returned for search |
| 401  | Unauthorized                  |
| 500  | Internal Server Error         |

<br />

# Find Patient

The Find Patient API (GET method) allows clients to lookup patientKey in HD system using following parameters: First Name, Last Name, DOB and Zip code. NOTE: The parameter fields should be separated with an ampersand (&) when using the API endpoint. If a match is found, HD returns matching patientKey to retrieve details using Get Patient API.

### Server

##### Only HTTPS connections are accepted.

| METHOD TYPE | ENDPOINT                                                                                                                      |
| :---------- | :---------------------------------------------------------------------------------------------------------------------------- |
| GET (Test)  | api.uat-healthdyne.com/v2/patient/find?firstname=\<firstName>lastname=\<lastName>\&birthdate=\<birthDate>\&zipcode=\<zipCode> |
| GET (Prod)  | api.healthdyne.com/v2/patient/find?firstname=\<firstName>lastname=\<lastName>\&birthdate=\<birthDate>\&zipcode=\<zipCode>     |

### Header

| Key                         | Value                  |
| :-------------------------- | :--------------------- |
| Accept                      | application/json       |
| Content-Type                | application/json       |
| HealthDyne-Subscription-Key | Provided by HealthDyne |

#### Sample GET Find Patient Request

`GET https://api.uat-healthdyne.com/v2/patient/find?firstname=ABC&lastname=XYZ&birthdate=1981-01-01&zipcode=80017`

Click here to see [GET Find Patient Request Query Data](https://docs.healthdyne.com/v2.171/docs/patient-request-fields#find-patient-request)

#### Sample GET Find Patient Response

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

Click here to see [Get Find Patient Response Data Object](https://docs.healthdyne.com/v2.171/docs/patient-request-fields#response-object-1)

The below table lists the potential response codes that can be received in response to a GET Find patient request.

| Code | Description                   |
| :--- | :---------------------------- |
| 200  | Patient details returned      |
| 400  | No record returned for search |
| 401  | Unauthorized                  |
| 500  | Internal Server Error         |

# Get Patient Scripts/Prescriptions

The "Get Patient Script/Prescription" endpoint allows retrieval of all scripts associated with a specific patient key. If no prescriptions are found for the provided patient key, the endpoint will return a 200 status with the message "No record found."

### Server

##### Only https connections are accepted.

| METHOD TYPE | ENDPOINT                                                                |
| :---------- | :---------------------------------------------------------------------- |
| GET (Test)  | api.uat-healthdyne.com/v2/patient/prescription?patientkey=\<patientKey> |
| GET (Prod)  | api.healthdyne.com/v2/patient/prescription?patientkey=\<patientKey>     |

### Header

| Key                         | Value                  |
| :-------------------------- | :--------------------- |
| Accept                      | application/json       |
| Content-Type                | application/json       |
| HealthDyne-Subscription-Key | Provided by HealthDyne |

#### Sample GET Patient Scripts/Prescriptions Request

`GET https://api.uat-healthdyne.com/v2/patient/prescription?patientKey=4e1e76ca-520f-4e7a-a6c7-d837a9e3cece`

Click here to see [GET Patient Scripts/Prescriptions Request Query Data](https://docs.healthdyne.com/v2.171/docs/patient-request-fields#get-patient-scriptsprescriptions-request)

#### Sample GET Patient Scripts/Prescriptions Response

```json
{
    "scriptKeys": [
        "0ed290dbb11224ea0f9e27"
    ]
}
```

Click here to see [GET Patient Scripts/Prescriptions Response Data Object](https://docs.healthdyne.com/v2.171/docs/patient-request-fields#response-object-2)

The below table lists the potential response codes that can be received in response to a GET request.

| Code | Description                                   |
| :--- | :-------------------------------------------- |
| 200  | Prescription details returned                 |
| 200  | No Prescription found                         |
| 400  | Bad Request – typically header is missing key |
| 401  | Unauthorized                                  |
| 500  | Internal Server Error                         |

<br />

# Create Patient

The "Create Patient" endpoint uses the POST method to add a new patient record. The request body must include all required patient information. Upon successful creation, the endpoint returns a 200 status along with a confirmation message. If any mandatory fields are missing or invalid, a corresponding error message will be returned.

### Server

##### Only HTTPS connections are accepted.

| METHOD TYPE | ENDPOINT                          |
| :---------- | :-------------------------------- |
| POST (Test) | api.uat-healthdyne.com/v2/patient |
| POST (Prod) | api.healthdyne.com/v2/patient     |

### Header

| Key                         | Value                  |
| :-------------------------- | :--------------------- |
| Accept                      | application/json       |
| Content-Type                | application/json       |
| HealthDyne-Subscription-Key | Provided by HealthDyne |

### Sample Create Patient Request

`POST https://api.uat-healthdyne.com/v2/patient`

### Sample Create Patient Request Body

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
      "defaultAddress":true
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

Click here to see [POST Create Patient Request Data Object](https://docs.healthdyne.com/v2.171/docs/patient-request-fields#create-patient-request)

#### Sample Create Patient Response

```json
{
  "patientKey": "12389990",
  "message": "The patient was added."
}
```

Click here to see [Create Patient Response Data Object](https://docs.healthdyne.com/v2.171/docs/patient-request-fields#response-object-3)

<br />

# Update Patient

The "Update Patient" endpoint uses the PUT method to modify the details of an existing patient. The request must include the patientKey along with the updated information in the request body. A successful update returns a 200 status and a confirmation message. If the patient is not found or the input data is invalid, an appropriate error response will be provided.

### Server

##### Only HTTPS connections are accepted.

| REQUEST TYPE | ENDPOINT                          |
| :----------- | :-------------------------------- |
| PUT (Test)   | api.uat-healthdyne.com/v2/patient |
| PUT (Prod)   | api.healthdyne.com/v2/patient     |

### Header

| Key                         | Value                  |
| :-------------------------- | :--------------------- |
| Accept                      | application/json       |
| Content-Type                | application/json       |
| HealthDyne-Subscription-Key | Provided by HealthDyne |

### Sample Update Patient Request

`PUT https://api.uat-healthdyne.com/v2/patient`

### Sample Update Patient Request Body

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
      "defaultAddress":true
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

Click here to see [PUT Patient Request Data Object]()

#### Sample Update Patient Response

```json
{
  "patientKey": "12389990",
  "message": "The patient was updated."
}
```

Click here to see [PUT Patient Response Data Object](https://docs.healthdyne.com/v2.171/docs/patient-request-fields#/)