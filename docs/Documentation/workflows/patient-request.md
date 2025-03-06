---
title: Patient
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
# Patient Request:

See the [Patient](ref:post_v2-patient) API reference for request message fields.

This API lets clients define and update patient information in the HealthDyne system.

Use POST method to add/create a patient and PUT method to update existing patient details.

API field validation information in Appendix [Patient Request Fields](doc:patient-request-fields)

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
			"line1":  "100 Rivers Edge Dr.",
			"line2": null,
			"line3": null,
			"city": "Temple Terrace",
			"state": "FL",
			"zipCode": "02155",
			"countryCode": "US",
			"defaultAddress": "True"
		},
		"contact": {
			"contactType": "PHONE",
			"contactAddress": "5712345678"
		},
		"allergies": [
			"Amoxicillin"
		],
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