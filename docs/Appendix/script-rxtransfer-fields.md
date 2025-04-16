---
title: Script / RxTransfer Fields
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
> 📃 Note:
>
> An empty string "" is considered a value and validation rules will apply (length/valid code/etc). Only null or missing elements will use default values.

# Script Request

| Field             | Type    | Character Limit | Required/Optional | Description                                                                                                                                                                              |
| :---------------- | :------ | :-------------- | :---------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| scriptKey         | String  | 50              | Required          | Unique ID assigned by sending pharmacy to each prescription transfer request for tracking.                                                                                               |
| sendingPharmacy   | Object  |                 | Required          | Contains information about the pharmacy transferring the prescription - see [Pharmacy](doc:script-rxtransfer-fields#pharmacy) table.                                                     |
| receivingPharmacy | Object  |                 | Required          | Contains information about the pharmacy the prescription is being transferred to - see [Pharmacy](doc:script-rxtransfer-fields#pharmacy) table.                                          |
| patientKey        | String  | 50              | Required          | Unique patient ID in Client system. This key will be sent on the order status message. The patientKey must be unique and patient must exist in the system when sending Transfer Request. |
| prescription      | Object  |                 | Required          | Contains the prescription information. See [Prescription](doc:script-rxtransfer-fields#prescription) table.                                                                              |
| transferFileType  | String  | 3               | Required          | The file type for the transfer file. Acceptable values are xml, png, and pdf.                                                                                                            |
| transferFileUrl   | String  | 2048            | Required          | Base 64 encoded URL where the XML or PNG transfer file can be downloaded from.                                                                                                           |
| orTransfer        | Boolean |                 | Required          | If this is a prescription transfer the value is true, for triage the value is false                                                                                                      |

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

| Field     | Type   | Character Limit | Required/Optional | Description                                                                                   |
| :-------- | :----- | :-------------- | :---------------- | :-------------------------------------------------------------------------------------------- |
| firstName | String | 35              | Optional          | First name of pharmacy or IT personnel to contact for details of the transferred prescription |
| lastName  | String | 35              | Optional          | Last name of pharmacy or IT personnel to contact for details of the transferred prescription  |
| phone     | String | 10              | Optional          | Phone number of contact. Format:XXXXXXXXXX                                                    |
| fax       | String | 10              | Optional          | Fax number of contact Format:XXXXXXXXXX                                                       |

# Address

| Field   | Type   | Character Limit | Required/Optional | Description                |
| :------ | :----- | :-------------- | :---------------- | :------------------------- |
| line1   | String | 40              | Required          | Street Address             |
| line2   | String | 40              | Optional          | Street Address             |
| city    | String | 35              | Required          | City                       |
| state   | String | 2               | Required          | US State Abbreviation Code |
| zipCode | String | 10              | Required          | Format NNNNN or NNNNN-NNNN |

# Prescription

| Field                      | Type    | Character Limit | Required/Optional | Description                                                                                                |
| :------------------------- | :------ | :-------------- | :---------------- | :--------------------------------------------------------------------------------------------------------- |
| rxNumber                   | String  | 12              | Required          | Rx number of the prescription as per client's system.                                                      |
| prescribedDrugName         | String  | 105             | Required          | Name of the medication as prescribed by the prescriber.                                                    |
| prescribedNdc              | String  | 11              | Required          | NDC prescribed by the prescriber.                                                                          |
| dispenseNdc                | String  | 11              | Optional          | Field is required if orTransfer is True. NDC dispensed by the pharmacy.                                    |
| dispenseDrugName           | String  | 105             | Optional          | Field is required if orTransfer is True. Name of the medication to be dispensed                            |
| drugDosageForm             | String  | 30              | Required          | Dosage form for the dispensed medication. For example: TABS, SWAB, CHEW, etc.                              |
| drugStrength               | String  | 10              | Required          | Drug strength (e.g., 125mcg).                                                                              |
| daysSupply                 | Integer |                 | Required          | Number of days the medication is intended to last.                                                         |
| quantityDispensedToDate    | Decimal |                 | Optional          | Total quantity dispensed so far.                                                                           |
| remainingQuantity          | Decimal |                 | Optional          | Remaining quantity left to dispense.                                                                       |
| labelDirections            | String  | 255             | Required          | Directions for taking the medication.                                                                      |
| writtenDate                | String  | 10              | Required          | Date the prescription was written.                                                                         |
| expirationDate             | String  | 10              | Optional          | Date the prescription expires.                                                                             |
| dawCode                    | String  | 1               | Required          | Dispense As Written code.                                                                                  |
| lastFillDate               | String  | 10              | Optional          | Date of the last fill, if any.                                                                             |
| firstFillDate              | String  | 10              | Optional          | Date of the first fill.                                                                                    |
| fillsToDate                | Integer |                 | Optional          | Number of fills already made.                                                                              |
| refillsAuthorized          | Integer |                 | Required          | Total refills authorized by the prescriber.                                                                |
| refillsLeft                | Integer |                 | Optional          | Refills remaining.                                                                                         |
| refillsTransferred         | Integer |                 | Optional          | Number of refills transferred to another pharmacy.                                                         |
| inactiveIndicator          | Boolean |                 | Required          | Indicates if the prescription is inactive.                                                                 |
| quantityWritten            | Decimal |                 | Required          | Quantity prescribed.                                                                                       |
| firstFillDispensedQuantity | Decimal |                 | Optional          | Quantity dispensed on the first fill.                                                                      |
| currentFillNumber          | Integer |                 | Optional          | Fill number of the current dispense action.                                                                |
| prescriber                 | Object  |                 | Required          | Object containing prescriber information. See [Prescriber](doc:script-rxtransfer-fields#prescriber) table. |

# Prescriber

| Field                | Type   | Character Limit | Required/Optional | Description                                                                                                        |
| :------------------- | :----- | :-------------- | :---------------- | :----------------------------------------------------------------------------------------------------------------- |
| firstName            | String | 35              | Required          | Prescriber (Doctor's) First Name                                                                                   |
| lastName             | String | 35              | Required          | Prescriber (Doctor's) Last Name                                                                                    |
| npi                  | String | 15              | Required          | Prescriber's NPI ID                                                                                                |
| dea                  | String | 15              | Optional          | Prescriber's DEA number                                                                                            |
| phoneNumber          | String | 10              | Required          | Prescriber's phone number                                                                                          |
| phoneNumberExtension | String | 8               | Optional          | Prescriber's phone extension                                                                                       |
| faxNumber            | String | 10              | Required          | Prescriber's fax number                                                                                            |
| address              | Object |                 | Required          | Prescriber's address information. See [Prescriber Address](doc:script-rxtransfer-fields#prescriber-address) table. |

***

# Prescriber Address

| Field   | Type   | Character Limit | Required/Optional | Description                |
| :------ | :----- | :-------------- | :---------------- | :------------------------- |
| line1   | String | 40              | Required          | Street Address             |
| line2   | String | 40              | Optional          | Street Address             |
| city    | String | 35              | Required          | City                       |
| state   | String | 2               | Required          | US State Abbreviation Code |
| zipCode | String | 10              | Required          | Format NNNNN or NNNNN-NNNN |

## GET Script Request

#### Query Parameter

| Field     | Type   | Character Limit | Required/Optional | Description |
| :-------- | :----- | :-------------- | :---------------- | :---------- |
| scriptKey | String | 50              | Required          |             |

#### Response Object

| Field        | Type   | Character Limit | Required/Optional | Description                                                                                           |
| :----------- | :----- | :-------------- | :---------------- | :---------------------------------------------------------------------------------------------------- |
| scriptKey    | String | 50              | Required          |                                                                                                       |
| prescription | Object |                 | Required          | See [Prescription Response Detail](doc:script-rxtransfer-fields#prescription-response-detail)  table. |

# Prescription Response Detail

| Field                | Type   | Character Limit | Description                                                                                                                                         |
| :------------------- | :----- | :-------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------- |
| rxNumber             | String | 20              | Rx number of the prescription                                                                                                                       |
| rxStatus             | String | 20              | Name of the medication as prescribed by the prescriber.                                                                                             |
| medicationPrescribed | Object |                 | Object containing medication prescribed information. See [Medication Prescribed](doc:script-rxtransfer-fields#medication-prescribed) table.         |
| medicationDispense   | Object |                 | Object containing medication dispensed information. See [Medication Dispensed](doc:script-rxtransfer-fields#medication-dispensed)  table.           |
| lastFillDate         | String | 10              | Date of the most recent fill.                                                                                                                       |
| patientKey           | String | 10              | Identifier associated with the patient.                                                                                                             |
| fillsRemaining       | String | 2               | Number of refills still available.                                                                                                                  |
| quantityRemaining    | String | 4               | Remaining quantity allowed to be filled.                                                                                                            |
| metricQuantity       | String | 10              | Quantity in metric units, if available.                                                                                                             |
| nextFillDate         | String | 10              | Next eligible fill date.                                                                                                                            |
| provider             | Object |                 | Information about the prescribing provider. Object containing provider  information. See [Provider](doc:script-rxtransfer-fields#provider)   table. |
| supervisor           | Object |                 | Optional supervisor information. Object containing  supervisor information. See [Supervisor](doc:script-rxtransfer-fields#supervisor)    table.     |

# Medication Prescribed

| Field           | Type    | Character Limit | Description                                     |
| :-------------- | :------ | :-------------- | :---------------------------------------------- |
| writtenDrugName | String  | 100             | Name of the drug as written by the provider.    |
| writtenDrugNdc  | String  | 11              | NDC of the written medication.                  |
| writtenGPI      | String  | 20              | Generic Product Identifier code.                |
| quantityWritten | Integer |                 | Quantity prescribed.                            |
| writtenDate     | String  | 10              | Date when the prescription was written.         |
| expirationDate  | String  | 10              | Date the prescription expires.                  |
| strength        | String  | 10              | Strength of the medication.                     |
| strengthUOM     | String  | 10              | Unit of measurement for strength.               |
| dosageForm      | String  | 50              | Form of the medication (e.g., Tablet, Capsule). |

# Medication Dispensed

| Field             | Type   | Character Limit | Description                                                  |
| :---------------- | :----- | :-------------- | :----------------------------------------------------------- |
| drugNdc           | String | 11              | NDC of the dispensed drug.                                   |
| drugGPI           | String | 20              | Generic Product Identifier for the dispensed drug.           |
| drugName          | String | 100             | Name of the dispensed drug.                                  |
| daysSupply        | String | 3               | Number of days the dispensed medication is intended to last. |
| strength          | String | 10              | Strength of the dispensed drug.                              |
| strengthUOM       | String | 10              | Unit of measurement for strength.                            |
| dosageFOrm        | String | 50              | Form of the dispensed medication.                            |
| sigInstructions   | String | 255             | Instructions for use (SIG).                                  |
| daw               | String | 1               | Dispense As Written code.                                    |
| refillsAuthorized | String | 2               | Number of refills authorized.                                |

# Provider

| Field              | Type   | Character Limit | Description                   |
| :----------------- | :----- | :-------------- | :---------------------------- |
| name               | String | 100             | Provider’s name.              |
| npi                | String | 10              | National Provider Identifier. |
| stateLicenseNumber | String | 20              | State license number.         |
| dea                | String | 20              | DEA number of the provider.   |

# Supervisor

| Field              | Type   | Character Limit | Description                        |
| :----------------- | :----- | :-------------- | :--------------------------------- |
| lastName           | String | 50              | Supervisor's last name.            |
| firstName          | String | 50              | Supervisor's first name.           |
| npi                | String | 10              | Supervisor’s NPI number.           |
| dea                | String | 20              | DEA number of the provider.        |
| stateLicenseNumber | String | 20              | Supervisor’s state license number. |

## GET Patient Scripts/Prescriptions Request

#### Query Parameter

| Field      | Type   | Character Limit | Required/Optional | Description                         |
| :--------- | :----- | :-------------- | :---------------- | :---------------------------------- |
| patientKey | String | 50              | Required          | Unique patient ID in Client system. |

#### Response Object

| Field      | Type  | Description                                                                               |
| :--------- | :---- | :---------------------------------------------------------------------------------------- |
| scriptKeys | Array | List of Unique IDs assigned by client to each prescription transfer request for tracking. |