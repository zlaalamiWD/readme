---
title: Script / RxTransfer Request
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
# Script / Transfer Rx

See [Script](ref:script) API reference for request message fields.

This API lets HealthDyne clients send a prescription transfer request from their pharmacy to HealthDyne. It also provides clients the ability to share the URL for HealthDyne to retrieve either: 

1. A PNG image of the prescription.
2. A XML file containing only the Surescript XML

API field validation information in Appendix [Script / RxTransfer Fields](doc:script-rxtransfer-fields)

![](https://files.readme.io/e54bd23-small-Script_Request.png)

### Server

##### Only https connections are accepted.

| REQUEST TYPE | ENDPOINT                         |
| :----------- | :------------------------------- |
| POST (Test)  | api.uat-healthdyne.com/v2/script |
| POST (Prod)  | api.healthdyne.com/v2/script     |

### Header

| Key                         | Value                  |
| :-------------------------- | :--------------------- |
| Accept                      | application/json       |
| Content-Type                | application/json       |
| HealthDyne-Subscription-Key | Provided by HealthDyne |

### Sample Script Request

```json
{
  "scriptKey": "e156daa5-1905-42c5-9e2e",
  "sendingPharmacy": {
    "pharmacyName": "MyPharmacy",
    "pharmacyNpi": "981000000999",
    "pharmacyNcPdp": "981000000999",
    "deaNumber": "981000000999",
    "phone": "1234567890",
    "fax": null,
    "pharmacist": {
      "firstName": "John",
      "lastName": "Doe"
    },
    "contact": {
      "contactType": "Phone",
      "contactAddress": "6789012345"
    },
    "address": {
      "line1": "401 My Pharmacy Dr.",
      "line2": null,
      "city": "Lakeland",
      "state": "FL",
      "zipCode": "33810"
    }
  },
	"receivingPharmacy": {
		"pharmacyName": "HEALTHDYNE",
		"pharmacyNpi": "1093974982",
    	"pharmacyNcPdp": "1093974982",
		"deaNumber": "1093974982",
		"phone": "3456789012",
		"fax": null,
		"pharmacist": {
			"firstName": "Phil",
			"lastName": "Doe"
		},
    "contact": {
      "contactType": "Phone",
      "contactAddress": "3456789012"
    },
    "address": {
      "line1": "500 Eagles Landing Dr.",
      "line2": null,
      "city": "Lakeland",
      "state": "FL",
      "zipCode": "33810"
    }
  },
  "patientKey": "12389990",
  "prescription": {
    "prescriber":{
      "firstName":"Doctor",
      "lastName":"Doe",
      "npi":"1093456789",
      "dea": "1093456789",
      "phoneNumber": "5556667777",
      "phoneNumberExtension": null,
      "faxNumber": null,
      "address": {
        "line1": "123 Doctor Lane",
        "line2": null,
        "city": "Lakeland",
        "state": "FL",
        "zipCode": "33810"
      }
    },
    "rxNumber": "45678",
    "prescribedNdc": "56789010211",
    "prescribedDrugName": "Tylenol",
    "dispenseNdc": "56789010212",
    "dispenseDrugName": "Ibuprofen",
    "drugDosageForm": "TABS",
    "drugStrength": "500mg",
    "daysSupply": 90,
    "quantityWritten": 180,
    "firstFillDispensedQuantity": 90,
    "quantityDispensedToDate":90,
    "remainingQuantity": 90,
    "labelDirections": "TAKE 1 TABLET DAILY",
    "writtenDate": "2022-04-04",
    "expirationDate": "2022-06-04",
    "dawCode": "0",
    "refillsAuthorized": "1",
    "lastFillDate": "2022-04-04",
    "firstFillDate": "2022-04-04",
    "fillsToDate": 1,
    "refillsLeft": 1,
    "refillsTransferred": 1,
    "currentFillNumber": "2"
  },
  "transferFileType": "PNG",
  "transferFileUrl": "aHR0cDpcXFNjb29ieURvb2J5RG9vLmNvbQ",
  "ortransfer": false
}
```

# Status Events

Please see the [RxTransfer](doc:mail-box#rxtransfer-status-events) status events under the [Mailbox](doc:mail-box) API guide for a detailed list of status events.

## Rejected Status

When a RxTransfer request can't be validated, HealthDyne generates a rejection event with status "Rejected". RxTransfers will be rejected if the PNG or XML download was unsuccessful after two (2) failed attempts. See [RxTransfer Rejected Status Event](doc:mail-box#rejected).

## Transferred Status

Once the PNG or XML has been successfully downloaded, HealthDyne will store the file and create the prescription record in HealthDyne's pharmacy management system. Once the Rx has been created, HealthDyne will generate a ‘Transferred’ event. See [RxTransfer Transferred Status Event](doc:mail-box#transferred).