---
title: Script / RxTransfer Fields (Updated Field Types)
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
> 📃 Note:
> 
> An empty string "" is considered a value and validation rules will apply (length/valid code/etc). Only null or missing elements will use default values.

# Script Request

| Field             | Type          | Character Limit | Required/Optional | Description                                                                                                                                                                              |
| :---------------- | :------------ | :-------------- | :---------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| scriptKey         | String        | 255             | Required          | Unique ID assigned by sending pharmacy to each prescription transfer request for tracking.                                                                                               |
| sendingPharmacy   | Object        |                 | Required          | Contains information about the pharmacy transferring the prescription - see [Pharmacy](doc:script-rxtransfer-fields#pharmacy) table.                                                     |
| receivingPharmacy | Object        |                 | Required          | Contains information about the pharmacy the prescription is being transferred to - see [Pharmacy](doc:script-rxtransfer-fields#pharmacy) table.                                          |
| patientKey        | String        | 30              | Required          | Unique patient ID in Client system. This key will be sent on the order status message. The patientKey must be unique and patient must exist in the system when sending Transfer Request. |
| prescription      | Object        |                 | Required          | Contains the prescription information. See [Prescription](doc:script-rxtransfer-fields#prescription) table.                                                                              |
| transferFileType  | String        | xml/png         | Required          | The file type for the transfer file. Acceptable values are xml and png.                                                                                                                  |
| transferFileUrl   | urlSafeBase64 | 2048            | Required          | Base 64 encoded URL where the XML or PNG transfer file can be downloaded from.                                                                                                           |
| orTransfer        | Boolean       | true/false      | Required          | If this is a prescription transfer the value is true, for triage the value is false                                                                                                      |

# Pharmacy

| Field         | Type   | Character Limit | Required/Optional | Description                                                                                                          |
| :------------ | :----- | :-------------- | :---------------- | :------------------------------------------------------------------------------------------------------------------- |
| pharmacyName  | String | 70              | Required          | Name of the pharmacy                                                                                                 |
| pharmacyNpi   | String | 15              | Required          | Pharmacy NPI ID                                                                                                      |
| pharmacyNcPdp | String | 15              | Optional          | Pharmacy NCPDP ID                                                                                                    |
| deaNumber     | String | 15              | Optional          | Pharmacy DEA number                                                                                                  |
| phone         | String | 10              | Required          | Pharmacy Phone number                                                                                                |
| fax           | String | 10              | Optional          | Pharmacy Fax number                                                                                                  |
| pharmacist    | Object |                 | Required          | Object containing information on the pharmacist. See [Pharmacist](doc:script-rxtransfer-fields#pharmacist) table.    |
| contact       | Object |                 | Required          | Object containing contact information for the pharmacist. See [Contact](doc:script-rxtransfer-fields#contact) table. |
| address       | Object |                 | Required          | Object containing the pharmacy address information. See [Address](doc:script-rxtransfer-fields#address) table.       |

# Pharmacist

| Field     | Type   | Character Limit | Required/Optional | Description               |
| :-------- | :----- | :-------------- | :---------------- | :------------------------ |
| firstName | String | 35              | Required          | First Name of pharmacist. |
| lastName  | String | 35              | Required          | Last Name of pharmacist.  |

# Contact

| Field          | Type   | Character Limit | Required/Optional | Description                                                                                        |
| :------------- | :----- | :-------------- | :---------------- | :------------------------------------------------------------------------------------------------- |
| contactType    | String | 15              | Optional          | Patient Contact – Phone, Home Phone, Day Phone, Work Phone, Fax Number, Cellular Number, Alternate |
| contactAddress | String | 10              | Required          | Contact Details. For instance: Populate phone number if contact type is phone. Format:XXXXXXXXXX   |

# Address

| Field   | Type   | Character Limit | Required/Optional | Description                |
| :------ | :----- | :-------------- | :---------------- | :------------------------- |
| line1   | String | 40              | Required          | Street Address             |
| line2   | String | 40              | Optional          | Street Address             |
| city    | String | 20              | Required          | City                       |
| state   | String | 2               | Required          | US State Abbreviation Code |
| zipCode | String | 5               | Required          | Format NNNNN               |

# Prescription

[block:parameters]
{
  "data": {
    "h-0": "Field",
    "h-1": "Type",
    "h-2": "Character Limit",
    "h-3": "Required/Optional",
    "h-4": "Description",
    "0-0": "prescriber",
    "0-1": "Object",
    "0-2": "",
    "0-3": "Required",
    "0-4": "Object containing prescriber information. See [Prescriber](doc:script-rxtransfer-fields#prescriber) table.",
    "1-0": "rxNumber",
    "1-1": "String",
    "1-2": "12",
    "1-3": "Required",
    "1-4": "Rx number of the prescription as per client's system.",
    "2-0": "prescribedDrugName",
    "2-1": "String",
    "2-2": "60",
    "2-3": "Required",
    "2-4": "Name of the medication as prescribed by the prescriber.",
    "3-0": "prescribedNdc",
    "3-1": "String",
    "3-2": "11",
    "3-3": "Required",
    "3-4": "NDC prescribed by the prescriber.",
    "4-0": "dispenseNdc",
    "4-1": "String",
    "4-2": "11",
    "4-3": "Required",
    "4-4": "NDC dispensed by the pharmacy.",
    "5-0": "dispenseDrugName",
    "5-1": "String",
    "5-2": "60",
    "5-3": "Required",
    "5-4": "Name of the medication to be dispensed.",
    "6-0": "drugDosageForm",
    "6-1": "String",
    "6-2": "30",
    "6-3": "Required",
    "6-4": "Dosage form for the dispensed medication. For example: TABS,SWAB,CHEW etc.",
    "7-0": "drugStrength",
    "7-1": "String",
    "7-2": "15",
    "7-3": "Required",
    "7-4": "Medication Strength corresponding to dispensed drug as prescribed by provider.",
    "8-0": "daysSupply",
    "8-1": "Int32",
    "8-2": "",
    "8-3": "Required",
    "8-4": "Number of days the medication covers as prescribed by the provider.",
    "9-0": "quantityWritten",
    "9-1": "Double",
    "9-2": "",
    "9-3": "Required",
    "9-4": "Total Quantity (in Metric units) as prescribed by the provider.",
    "10-0": "firstFillDispensedQuantity",
    "10-1": "Double",
    "10-2": "",
    "10-3": "Required",
    "10-4": "Quantity (in Metric units) that has been dispensed by the pharmacy in the** first fill**. Populate 0 if the transferring pharmacy has not dispensed any medication for the Rx.",
    "11-0": "quantityDispensedToDate",
    "11-1": "Double",
    "11-2": "",
    "11-3": "Required",
    "11-4": "Quantity (in Metric units) that has been dispensed by the pharmacy till Date. Populate 0 if the transferring pharmacy has not dispensed any medication for the Rx.",
    "12-0": "remainingQuantity",
    "12-1": "Double",
    "12-2": "",
    "12-3": "Required",
    "12-4": "Quantity (in Metric units) that is yet to be dispensed. It must be equal to quantityWritten - quantityDispensedtoDate.",
    "13-0": "labelDirections",
    "13-1": "String",
    "13-2": "200",
    "13-3": "Required",
    "13-4": "Prescription usage instructions. Also commonly referred to as the Instructions/Signature. This must be populated in English language and must not contain following characters:  \n| (Pipe), ^ (component separator), ~ (field repetition separator), \\(escape character), & (Sub-component separator)",
    "14-0": "writtenDate",
    "14-1": "Date-time",
    "14-2": "YYYY-MM-DD",
    "14-3": "Required",
    "14-4": "Written date of the prescription; Format YYYYMMDD.",
    "15-0": "expirationDate",
    "15-1": "Date-time",
    "15-2": "YYYY-MM-DD",
    "15-3": "Required",
    "15-4": "Prescription’s expiration date; Format YYYYMMDD.",
    "16-0": "dawCode",
    "16-1": "String",
    "16-2": "1",
    "16-3": "Required",
    "16-4": "DAW code as prescriber by prescriber.",
    "17-0": "refillsAuthorized",
    "17-1": "String",
    "17-2": "2",
    "17-3": "Required",
    "17-4": "Counts of **refills** authorized by prescriber.  \nIf the prescriber authorized 4 refills, populate 4",
    "18-0": "lastFillDate",
    "18-1": "Date-time",
    "18-2": "YYYY-MM-DD",
    "18-3": "Optional",
    "18-4": "Date when **last** fill occurred. Format YYYY-MM-DD. Must populate for Transfer.  \nIf the transfer pharmacy has not fulfilled any order yet, then populate NULL.",
    "19-0": "firstFillDate",
    "19-1": "Date-time",
    "19-2": "YYYY-MM-DD",
    "19-3": "Optional",
    "19-4": "Date when **first** fill occurred. Format YYYY-MM-DD.Must populate for Transfer.  \nIf the transfer pharmacy has not fulfilled any order yet, then populate NULL.",
    "20-0": "fillsToDate",
    "20-1": "Int32",
    "20-2": "",
    "20-3": "Required",
    "20-4": "Total number of fills fulfilled for the Rx till Date. If the transfer pharmacy has not fulfilled any order yet, then populate 0.  \nIf the provider authorized 4 refills and 2 fills have been fulfilled, then populate 2",
    "21-0": "refillsLeft",
    "21-1": "Int32",
    "21-2": "",
    "21-3": "Required",
    "21-4": "Total number of fills remaining. Should be equal to fillsAuthorized -fillsToDate.",
    "22-0": "refillsTransferred",
    "22-1": "Int32",
    "22-2": "",
    "22-3": "Required",
    "22-4": "Number of refills being transferred to HD for fulfillment.  \nIf the provider authorized 4 refills and 2 fills have been fulfilled, then populate 3",
    "23-0": "currentFillNumber",
    "23-1": "String",
    "23-2": "2",
    "23-3": "Required",
    "23-4": "Populate the current fill number. If there is no order fulfilled yet, populate 00.  \nIf the provider authorized 4 refills and 2 fills have been fulfilled, then populate 02"
  },
  "cols": 5,
  "rows": 24,
  "align": [
    "left",
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]

# Prescriber

| Field                | Type   | Character Limit | Required/Optional | Description                                                                                  |
| :------------------- | :----- | :-------------- | :---------------- | :------------------------------------------------------------------------------------------- |
| firstName            | String | 35              | Required          | Prescriber (Doctor's) First Name                                                             |
| lastName             | String | 35              | Required          | Prescriber (Doctor's) Last Name                                                              |
| npi                  | String | 15              | Required          | Prescriber's NPI ID                                                                          |
| dea                  | String | 15              | Optional          | Prescriber's DEA number                                                                      |
| phoneNumber          | String | 10              | Required          | Prescriber's phone number                                                                    |
| phoneNumberExtension | String | 8               | Optional          | Prescriber's phone extension                                                                 |
| faxNumber            | String | 10              | Required          | Prescriber's fax number                                                                      |
| address              | Object |                 | Required          | Prescriber's address information. See [Address](doc:script-rxtransfer-fields#address) table. |