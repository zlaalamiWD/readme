---
title: Prescription / Refill / Cancel Request Fields
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
# Prescription Request 

| Field          | Type         | Character Limit | Required/Optional | Description                           |
| :------------- | :----------- | :-------------- | :---------------- | :------------------------------------ |
| RequestId      | String       | 255             | Required          | The unique request ID from the client |
| LineOfBusiness | String       | 15              | Required          | Contains Group ID Information         |
| Patient        | Patient      |                 | Optional          | Member Information                    |
| Prescriptions  | Prescription |                 | Required          | Array – 1 or more prescriptions       |
| Shipping       | Shipping     |                 | Required          | Shipping information of the Order     |

# Patient

| Field                | Type    | Character Limit | Required/Optional | Description                                                                       |
| :------------------- | :------ | :-------------- | :---------------- | :-------------------------------------------------------------------------------- |
| PatientId            | String  | 20              | Optional          | Unique Patient Identifier that identifies a patient of which an Rx is prescribed. |
| MemberId             | String  | 20              | Optional          | Unique Member Identifier that identifies a patient of which an Rx is prescribed.  |
| FirstName            | String  | 50              | Required          | Patient first name                                                                |
| LastName             | String  | 50              | Required          | Patient last name                                                                 |
| BirthDate            | Date    | MM/DD/YYYY      | Required          | Patient's Date of Birth                                                           |
| Gender               | String  | 1               | Required          | Patient’s Gender – M, F or U                                                      |
| Address              | Address |                 | Required          | Patient’s Address Information                                                     |
| Contact              | Contact |                 | Required          | Patient’s Contact Information                                                     |
| Allergies            | String  |                 | Required          | Contains Allergy list                                                             |
| External Medications | String  |                 | Optional          | Contains Medication list                                                          |

# Address

| Field          | Type    | Character Limit | Required/Optional | Description                                                                                                                                                                                                                            |
| :------------- | :------ | :-------------- | :---------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| addressType    | String  | 20              | Optional          | Address Type (Home, Temporary,  Corporate, Alternate, Primary Office)                                                                                                                                                                  |
| line1          | String  | 60              | Required          | Street Address                                                                                                                                                                                                                         |
| line2          | String  | 60              | Optional          | Street Address                                                                                                                                                                                                                         |
| line3          | String  | 40              | Optional          | Street Address                                                                                                                                                                                                                         |
| city           | String  | 35              | Required          | City                                                                                                                                                                                                                                   |
| state          | String  | 2               | Required          | US State Abbreviation Code                                                                                                                                                                                                             |
| zip            | String  | 5,9             | Required          | Format NNNNN, NNNNNNNNN                                                                                                                                                                                                                |
| defaultAddress | Boolean | 1               | Required          | Values = T/F (Ship the order to this Address). This is the address for the patient and where the order will be shipped unless there is an address registered already with HealthDyne Then the order will be delivered to that address. |

# Contact

| Field          | Type   | Character Limit | Required/Optional | Description                                                                                        |
| :------------- | :----- | :-------------- | :---------------- | :------------------------------------------------------------------------------------------------- |
| contactType    | String | 15              | Required          | Patient Contact – Phone, Home Phone, Day Phone, Work Phone, Fax Number, Cellular Number, Alternate |
| contactAddress |        | 10              | Required          | Contact Details. For instance: Populate phone number if contact type is phone.                     |

# Insurance

| Field             | Type   | Character Limit | Required/Optional | Description                                                                                              |
| :---------------- | :----- | :-------------- | :---------------- | :------------------------------------------------------------------------------------------------------- |
| Relationship Code | String | 1               | Optional          | See [Relationship Codes Table](doc:prescription-request#relationship-codes) below for Relationship Codes |
| BIN               | String | 6               | Optional          | NCPDP Processor ID Number                                                                                |
| Group             | String | 15              | Optional          | Plan Group Number                                                                                        |
| PCN               | String | 10              | Optional          | Processor Control Number                                                                                 |
| PolicyHolderID    | String | 20              | Optional          | Patient’s insurance policyholderID                                                                       |

# Relationship Codes

| Type               | Code |
| :----------------- | :--- |
| Not Specified      | 0    |
| Cardholder         | 1    |
| Spouse             | 2    |
| Child              | 3    |
| Other Dependent    | 4    |
| Student Dependent  | 5    |
| Disabled Dependent | 6    |
| Adult Dependent    | 7    |
| Significant Other  | 8    |

# Allergy

| Field   | Type           | Character Limit | Required/Optional | Description                   |
| :------ | :------------- | :-------------- | :---------------- | :---------------------------- |
| Allergy | String/[Array] |                 | Required          | See valid allergy types below |

- No Known
- Amoxicillin
- Aspirin
- Cephalosporins
- Codeine
- Erythromycin
- Penicillin
- Sulfa
- Tetracyclines
- Others

# External Medication

| Field     | Type    | Character Limit | Required/Optional | Description                                |
| :-------- | :------ | :-------------- | :---------------- | :----------------------------------------- |
| NDC       | Integer | 11              | Required          | NDC of the medication                      |
| Notes     | String  | 1500            | Optional          | Information such as Drug Name, Drug Dosage |
| StartDate | Date    | MM/DD/YYYY      | Required          | Date when medication was started           |
| EndDate   | Date    | MM/DD/YYYY      | Required          | Date when medication was ended             |

# Prescription

| Field       | Type    | Character Limit | Required/Optional | Description                                                                               |
| :---------- | :------ | :-------------- | :---------------- | :---------------------------------------------------------------------------------------- |
| Rx          | String  | 20              | Optional          | RX number for the Prescription Required if it is a refill or a status update              |
| NDCName     | String  | 60              | Optional          | Name of the medication                                                                    |
| NDC         | Integer | 11              | Required          | NDC for the prescription                                                                  |
| ProviderNPI | String  | 10              | Optional          | Optional by Client if requesting HealthDyne to reach out to get the prescription          |
| PharmacyNPI | String  | 10              | Optional          | Optional by Client if requesting the prescription to be transferred from another pharmacy |
| Quantity    | Integer | 1000            | Required          | Quantity to be dispensed for the requested prescription and must be greater than 0        |

# Shipping

| Field             | Type    | Character Limit | Required/Optional | Description                                                                                                                                                                                                        |
| :---------------- | :------ | :-------------- | :---------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ShippingCode      | String  | 10              | Optional          | See [Shipping Codes Table](doc:prescription-request#shipping-codes) below                                                                                                                                          |
| SignatureRequired | Boolean | 1               | Optional          | Values: True/False. Select the option if the package requires a signature                                                                                                                                          |
| SaturdayDelivery  | Boolean | 1               | Optional          | Values: True/False. Saturday Delivery is an option for certain shipping codes depending on the carrier. To have an order delivered on a Saturday, select the correct Shipping Code and then set this flag to true. |
| Address           | Address |                 | Optional          | Shipping Address                                                                                                                                                                                                   |

# Shipping Codes

| Code     | Description                               | Notes             |
| :------- | :---------------------------------------- | :---------------- |
| POS 1C   | USPS 1st Class                            | Saturday delivery |
| POS 1M   | USPS Priority                             | Saturday delivery |
| UPS 1D   | UPS Next Day Air (12:00 PM Delivery)      | Saturday delivery |
| UPS 1DAM | UPS Next Day Air AM Delivery              | Saturday delivery |
| UPS 1S   | UPS Next Day Air Saver (3:00 PM Delivery) | Saturday delivery |
| UPS 2D   | UPS 2nd Day (12:00 PM Delivery)           | Saturday delivery |
| UPS 2DAM | UPS 2nd Day (Morning Delivery)            | Saturday delivery |
| UPS GR   | UPS Ground                                |                   |
| UPS MID  | Mail Innovations                          |                   |
| UPS 3 DS | UPS 3 Day Select                          | Saturday delivery |
| UPS USG  | UPS-USPS Sure Post                        | Saturday delivery |