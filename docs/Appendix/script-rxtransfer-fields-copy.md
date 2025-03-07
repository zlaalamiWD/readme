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

<HTMLBlock>{`
<table style="width: 100%; border-collapse: collapse;">
<thead>
<tr>
  <th style="border: 1px solid #ddd; padding: 8px;">Field</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Type</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Character Limit</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Required/Optional</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Description</th>
</tr>
</thead>
<tbody>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>prescriber</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Object</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Required</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Object containing prescriber information. See <a href="doc:script-rxtransfer-fields#prescriber">Prescriber</a> table.</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>rxNumber</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>12</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Required</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Rx number of the prescription as per client&#39;s system.</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>prescribedDrugName</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>60</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Required</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Name of the medication as prescribed by the prescriber.</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>prescribedNdc</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>11</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Required</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>NDC prescribed by the prescriber.</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>dispenseNdc</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>11</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Required</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>NDC dispensed by the pharmacy.</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>dispenseDrugName</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>60</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Required</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Name of the medication to be dispensed.</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>drugDosageForm</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>30</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Required</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Dosage form for the dispensed medication. For example: TABS,SWAB,CHEW etc.</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>drugStrength</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>15</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Required</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Medication Strength corresponding to dispensed drug as prescribed by provider.</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>daysSupply</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Int32</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Required</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Number of days the medication covers as prescribed by the provider.</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>quantityWritten</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Double</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Required</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Total Quantity (in Metric units) as prescribed by the provider.</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>firstFillDispensedQuantity</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Double</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Required</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Quantity (in Metric units) that has been dispensed by the pharmacy in the** first fill**. Populate 0 if the transferring pharmacy has not dispensed any medication for the Rx.</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>quantityDispensedToDate</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Double</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Required</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Quantity (in Metric units) that has been dispensed by the pharmacy till Date. Populate 0 if the transferring pharmacy has not dispensed any medication for the Rx.</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>remainingQuantity</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Double</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Required</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Quantity (in Metric units) that is yet to be dispensed. It must be equal to quantityWritten - quantityDispensedtoDate.</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>labelDirections</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>200</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Required</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Prescription usage instructions. Also commonly referred to as the Instructions/Signature. This must be populated in English language and must not contain following characters:<br>| (Pipe), ^ (component separator), ~ (field repetition separator), (escape character), &amp; (Sub-component separator)</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>writtenDate</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Date-time</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>YYYY-MM-DD</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Required</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Written date of the prescription; Format YYYYMMDD.</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>expirationDate</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Date-time</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>YYYY-MM-DD</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Required</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Prescription’s expiration date; Format YYYYMMDD.</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>dawCode</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>1</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Required</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>DAW code as prescriber by prescriber.</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>refillsAuthorized</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>2</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Required</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Counts of <strong>refills</strong> authorized by prescriber.<br>If the prescriber authorized 4 refills, populate 4</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>lastFillDate</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Date-time</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>YYYY-MM-DD</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Optional</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Date when <strong>last</strong> fill occurred. Format YYYY-MM-DD. Must populate for Transfer.<br>If the transfer pharmacy has not fulfilled any order yet, then populate NULL.</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>firstFillDate</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Date-time</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>YYYY-MM-DD</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Optional</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Date when <strong>first</strong> fill occurred. Format YYYY-MM-DD.Must populate for Transfer.<br>If the transfer pharmacy has not fulfilled any order yet, then populate NULL.</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>fillsToDate</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Int32</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Required</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Total number of fills fulfilled for the Rx till Date. If the transfer pharmacy has not fulfilled any order yet, then populate 0.<br>If the provider authorized 4 refills and 2 fills have been fulfilled, then populate 2</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>refillsLeft</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Int32</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Required</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Total number of fills remaining. Should be equal to fillsAuthorized -fillsToDate.</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>refillsTransferred</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Int32</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Required</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Number of refills being transferred to HD for fulfillment.<br>If the provider authorized 4 refills and 2 fills have been fulfilled, then populate 3</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>currentFillNumber</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>2</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Required</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Populate the current fill number. If there is no order fulfilled yet, populate 00.<br>If the provider authorized 4 refills and 2 fills have been fulfilled, then populate 02</p>
</td>
</tr>
</tbody>
</table>
`}</HTMLBlock>

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