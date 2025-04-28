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
The Rx Fill API provides the ability to submit new prescription fill requests and to retrieve status messages for previously sent prescription fill requests.

## Submit Fill Request

See [RxFill]() API reference for request message fields.

![](https://files.readme.io/0cbbce628e8a6d0759beef64779c19e2816e823f4153986627972ebdf9c1c039-image.png)

### Server

##### Only https connections are accepted.

| REQUEST TYPE | ENDPOINT                              |
| :----------- | :------------------------------------ |
| POST (Test)  | api.uat-healthdyne.com/v2/fillrequest |
| POST (Prod)  | api.healthdyne.com/v2/fillrequest     |

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
	"messageid": "z79v4c1g-1w09-4514-b4fc-1286reae0egb07-v2-12",
	"ordernumber": "TST1234RVVL-v2-12",
	"pharmacy": {
		"name": "HEALTHDYNE PHARMACY",
		"address": {
			"address1": "500 EAGLES LANDING DRIVE",
			"city": "LAKELAND",
			"phone": "",
			"state": "FL",
			"zip": "33801"
		},
		"npi": "1740363274"
	},
	"patient": {
		"id": "1569928",
		"accountNumber": "1569928", 
		"firstName": "FIRSTNAME",
		"lastName": LASTNAME
		"preferredLanguage": "ENG"
	},
	"prescriptions": [
		{
			"rxNumber": "645917",
			"drug": {
				"ndc": "00002143380",
				"manufacturer": "GRIFOLS USA",
				"name": "MARPLAN TAB 10MG",
				"strength": "1000",
				"substituteDrugName": "",
				"unitOfMeasure": "ML"
			},
			"quantity": 1,
			"refill": {
				"fillNumber": 13,
				"nextRefillDate": "2021-01-12T00:00:03",
				"refillsPrescribed": 13,
				"refillsDispensed": 13,
				"refillsRemaining": 0
			},
			"prescriber": {
				"deaNumber": "1235",
				"firstName": "John",
				"lastName": "Doe"
			},
			"writtenDrugName": "MARPLAN TAB 10MG",
			"writtenDate": "2021-02-02T12:28:59",
			"dispensedDate": "2020-12-15T00:00:03",
			"expirationDate": "2021-12-14T00:00:03",
			"unitprice": 1.02,
			"copayamount": 1.03,
			"referencedata": [],
			"pharmacist": {
				"initials": null,
				"FirstName": "Test",
				"LastName": "TestLname"
			},
			"vialLabel": {
				"sig": "TAKE 1 TABLET BY MOUTH DAILY",
				"additionalSig": null,
				"braille": false,
				"largePrint": false,
				"audioLabel": false
			}
		}
	],
	"shipping": {
		"shippingCode": "UPS 1D",
		"signatureRequired": false,
		"saturdayDelivery": false,
		"address": {
			"name": "John Robertson",
			"address1": "407 N CAROLINE ST ",
			"address2": "",
			"city": "BALTIMORE",
			"phone": "7743866854",
			"state": "MD",
			"zip": "21231",
			"clinicId": null
		},
		"deliveryInstructions": "",
		"holdAddress": {
			"name": "",
			"address1": "",
			"address2": "",
			"city": "",
			"phone": "",
			"state": "",
			"zip": ""
		},
		"notificationEmail": ""
	},
	"CustomData": []
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