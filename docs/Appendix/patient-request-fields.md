---
title: Patient Request Data Object (Schemas)
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
> 📃 Note:
>
> An empty string "" is considered a value and validation rules will apply (length/valid code/etc). Only null or missing elements will use default values.

# Patient Request Data Object

# Patient

| Field               | Type                                                                             | Character Limit | Required/Optional | Description                                                                                                                                                                                                                                                                                                                                   |
| :------------------ | :------------------------------------------------------------------------------- | :-------------- | :---------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| patientKey          | String                                                                           | 50              | Required          | Unique patient ID in Client system.                                                                                                                                                                                                                                                                                                           |
| firstName           | String                                                                           | 35              | Required          | Patient's first name.                                                                                                                                                                                                                                                                                                                         |
| lastName            | String                                                                           | 35              | Required          | Patient's last name.                                                                                                                                                                                                                                                                                                                          |
| birthDate           | DateTime                                                                         | YYYY-MM-DD      | Required          | Patient's Date of Birth                                                                                                                                                                                                                                                                                                                       |
| gender              | String                                                                           | 1               | Required          | Patient’s Gender – M, F or U                                                                                                                                                                                                                                                                                                                  |
| patientLanguage     | String                                                                           | 3               | Optional          | Patient language must be ENG or SPA.                                                                                                                                                                                                                                                                                                          |
| address             | Object [(address)](doc:patient-request-fields#address)                           |                 | Required          | Object containing patient’s address information. See [Address](doc:patient-request-fields#address) table.                                                                                                                                                                                                                                     |
| contact             | Object [(contact)](doc:patient-request-fields#contact)                           |                 | Required          | Object containing patient’s contact information. See [Contact](doc:patient-request-fields#contact) table.                                                                                                                                                                                                                                     |
| allergies           | Array [\[allergies\]](doc:patient-request-fields#allergies)                      |                 | Required          | Array containing patient’s allergy information. See the [Allergies](doc:patient-request-fields#allergies) table for valid list of allergies.                                                                                                                                                                                                  |
| externalMedications | Array [\[externalMedications\]](doc:patient-request-fields#external-medications) |                 | Optional          | Array containing patient’s external medications objects. List any external Medications the patient is taking for pharmacy to know if there is any drug interaction. If there are  external medications, then ensure all the object elements are populated. See [External Medications](doc:patient-request-fields#external-medications) table. |

# Address

| Field          | Type    | Character Limit | Required/Optional | Description                                                                                                                                                        |
| :------------- | :------ | :-------------- | :---------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| addressType    | String  | 15              | Optional          | Defines the type of address. If the filed is not sent by client, then defaults to HOME. Valid values include HOME, PRIMARY OFFICE, TEMPORARY, CORPORATE, ALTERNATE |
| line1          | String  | 40              | Required          | Street Address                                                                                                                                                     |
| line2          | String  | 40              | Optional          | Street Address                                                                                                                                                     |
| line3          | String  | 40              | Optional          | Street Address                                                                                                                                                     |
| city           | String  | 35              | Required          | City                                                                                                                                                               |
| state          | String  | 2               | Required          | US State Abbreviation Code                                                                                                                                         |
| zipCode        | String  | 10              | Required          | Format NNNNN or NNNNN-NNNN                                                                                                                                         |
| countryCode    | String  | 2               | Optional          | ISO-3166 2 character country code. Defaults to US.                                                                                                                 |
| defaultAddress | Boolean |                 | Optional          | Values = true/false. When the address is to be used as the default address for patient, then populate True; otherwise default to FALSE.                            |

# Contact

| Field          | Type   | Character Limit | Required/Optional | Description                                                                                        |
| :------------- | :----- | :-------------- | :---------------- | :------------------------------------------------------------------------------------------------- |
| contactType    | String | 15              | Optional          | Patient Contact – Phone, Home Phone, Day Phone, Work Phone, Fax Number, Cellular Number, Alternate |
| contactAddress | String | 10              | Required          | Contact Details. For instance: Populate phone number if contact type is phone. Format:XXXXXXXXXX   |

\*Required if the Contact object is being provided in the Patient object.

# Allergies

| Field     | Type  | Character Limit | Required/Optional | Description                                                                                                                                                                |
| :-------- | :---- | :-------------- | :---------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| allergies | Array | 40              | Required          | Array of string. Character limit is for each string in Array. See valid allergy types below. The allergies field is required, if patient has no allergies pass "NO KNOWN". |

| Allergy Name                           | Allergy Class                          |
| :------------------------------------- | :------------------------------------- |
| ACE INHIBITORS                         | ACE INHIBITORS                         |
| ACETAMINOPHEN                          | ACETAMINOPHEN                          |
| Amoxicillin                            | Penicillins                            |
| Aspirin                                | Salicylates                            |
| Atenolol                               | BETA ADRENERGIC BLOCKERS               |
| Atorvastatin                           | STATINS                                |
| Benazepril                             | ACE INHIBITORS                         |
| BETA ADRENERGIC BLOCKERS               | BETA ADRENERGIC BLOCKERS               |
| Cephalosporins                         | Cephalosporins                         |
| Ciprofloxacin                          | QUINOLONES                             |
| Codeine                                | Morphine and Related                   |
| Demerol                                | MEPERIDINE AND RELATED                 |
| Erythromycin                           | Macrolides and Ketolides               |
| Fosinopril                             | ACE INHIBITORS                         |
| IBUPROFEN                              | NSAIDS                                 |
| IODIDES                                | IODINATED CONTRAST MEDIA               |
| IODINATED CONTRAST MEDIA               | IODINATED CONTRAST MEDIA               |
| IODINATED DIAGNOSTIC AGENTS            | IODINATED CONTRAST MEDIA               |
| Levofloxacin                           | QUINOLONES                             |
| Lisinopril                             | ACE INHIBITORS                         |
| Macrolides and Ketolides               | Macrolides and Ketolides               |
| MEPERIDINE AND RELATED                 | MEPERIDINE AND RELATED                 |
| Metoprolol                             | BETA ADRENERGIC BLOCKERS               |
| MISC. SULFONAMIDE CONTAINING COMPOUNDS | MISC. SULFONAMIDE CONTAINING COMPOUNDS |
| Morphine and Related                   | Morphine and Related                   |
| No Known                               | No Known Drug Allergy                  |
| No Known Drug Allergy                  | No Known Drug Allergy                  |
| NSAIDS                                 | NSAIDS                                 |
| Penicillins                            | Penicillins                            |
| QUINOLONES                             | QUINOLONES                             |
| Rosuvastatin                           | STATINS                                |
| Salicylates                            | Salicylates                            |
| SHELLFISH-DERIVED PRODUCTS             | SHELLFISH-DERIVED PRODUCTS             |
| Simvastatin                            | STATINS                                |
| STATINS                                | STATINS                                |
| Sulfa                                  | Sulfa Antibiotics                      |
| Sulfa Antibiotics                      | Sulfa Antibiotics                      |
| Tetracyclines                          | Tetracyclines & Related                |
| Tetracyclines & Related                | Tetracyclines & Related                |

> 📃 Additional Allergy Information
>
> Allergy information not matching the defined allergy list will still be accepted. However the information will be added in the HealthDyne system under the "notes" section of the Patient's profile for pharmacist to review. Each non-defined allergy list entry has a 40 character limit.

# External Medications

| Field     | Type     | Character Limit | Required/Optional | Description                      |
| :-------- | :------- | :-------------- | :---------------- | :------------------------------- |
| ndc       | String   | 11              | Required\*        | NDC of the medication            |
| startDate | DateTime | YYYY-MM-DD      | Optional          | Date when medication was started |
| endDate   | DateTime | YYYY-MM-DD      | Optional          | Date when medication was ended   |

\*NDC is required if the External Medications object is being provided in the Patient object.

## GET Patient Request

#### Query Parameter

| Field      | Type   | Character Limit | Required/Optional | Description                         |
| :--------- | :----- | :-------------- | :---------------- | :---------------------------------- |
| patientKey | String | 50              | Required          | Unique patient ID in Client system. |

#### Response Object

| Field               | Type                                                                                                                | Character Limit | Required/Optional | Description                                                                                                                                                                                                                                                                                                                                   |
| :------------------ | :------------------------------------------------------------------------------------------------------------------ | :-------------- | :---------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| patientKey          | String                                                                                                              | 50              | Required          | Unique patient ID in Client system.                                                                                                                                                                                                                                                                                                           |
| firstName           | String                                                                                                              | 35              | Required          | Patient's first name.                                                                                                                                                                                                                                                                                                                         |
| lastName            | String                                                                                                              | 35              | Required          | Patient's last name.                                                                                                                                                                                                                                                                                                                          |
| gender              | String                                                                                                              | 1               | Required          | Patient’s Gender – M, F or U                                                                                                                                                                                                                                                                                                                  |
| patientLanguage     | String                                                                                                              | 3               | Required          | Patient language must be ENG or SPA.                                                                                                                                                                                                                                                                                                          |
| birthDate           | DateTime                                                                                                            | YYYY-MM-DD      | Required          | Patient's Date of Birth                                                                                                                                                                                                                                                                                                                       |
| healthCondition     | Array                                                                                                               |                 | Optional          | Patient's health condition.                                                                                                                                                                                                                                                                                                                   |
| address             | Object [(address)](doc:patient-request-fields#address)                                                              |                 | Required          | Object containing patient’s address information. See [Address](doc:patient-request-fields#address) table.                                                                                                                                                                                                                                     |
| contact             | Object [(contact)](doc:patient-request-fields#contact)                                                              |                 | Required          | Object containing patient’s contact information. See [Contact](doc:patient-request-fields#contact) table.                                                                                                                                                                                                                                     |
| externalMedications | Array \[[externalMedications](https://docs.healthdyne.com/v2.171/docs/patient-request-fields#external-medications)] |                 | Optional          | Array containing patient’s external medications objects. List any external Medications the patient is taking for pharmacy to know if there is any drug interaction. If there are  external medications, then ensure all the object elements are populated. See [External Medications](doc:patient-request-fields#external-medications) table. |
| pregnancyIndicator  | String                                                                                                              | 1               | Required          | Patient's pregnancy status.                                                                                                                                                                                                                                                                                                                   |
| allergies           | Array [\[allergies\]](doc:patient-request-fields#allergies)                                                         |                 | Optional          | Array containing patient’s allergy information. See the [Allergies](doc:patient-request-fields#allergies) table for valid list of allergies.                                                                                                                                                                                                  |

# Find Patient Request

#### Query Parameter

| Field     | Type     | Character Limit | Required/Optional | Description                |
| :-------- | :------- | :-------------- | :---------------- | :------------------------- |
| firstName | String   | 35              | Required          | Patient's first name.      |
| lastName  | String   | 35              | Required          | Patient's last name.       |
| birthDate | DateTime | YYYY-MM-DD      | Required          | Patient's Date of Birth    |
| zipCode   | String   | 10              | Required          | Format NNNNN or NNNNN-NNNN |

#### Response Object

| Field      | Type     | Character Limit | Required/Optional | Description                                                   |
| :--------- | :------- | :-------------- | :---------------- | :------------------------------------------------------------ |
| patientKey | Array    |                 | Required          | Array of patientKey(s) (Unique patient ID in Client system.). |
| firstName  | String   | 35              | Required          | Patient's first name.                                         |
| lastName   | String   | 35              | Required          | Patient's last name.                                          |
| birthDate  | DateTime | YYYY-MM-DD      | Required          | Patient's Date of Birth                                       |
| zipCode    | String   | 10              | Required          | Format NNNNN or NNNNN-NNNN                                    |

# Get Patient Scripts/Prescriptions Request

#### Query Parameter

| Field      | Type   | Character Limit | Required/Optional | Description                         |
| :--------- | :----- | :-------------- | :---------------- | :---------------------------------- |
| patientKey | String | 50              | Required          | Unique patient ID in Client system. |

#### Response Object

| Field      | Type  | Character Limit | Required/Optional | Description                                  |
| :--------- | :---- | :-------------- | :---------------- | :------------------------------------------- |
| scriptKeys | Array | 255 per value   | Required          | Array of scriptKey(s) associated to Patient. |

# Create Patient Request

#### Request Object

| Field   | Type                                                                                       | Character Limit | Required/Optional | Description                                       |
| :------ | :----------------------------------------------------------------------------------------- | :-------------- | :---------------- | :------------------------------------------------ |
| patient | Object [(patient)](https://docs.healthdyne.com/v2.171/docs/patient-request-fields#patient) |                 | Required          | Object containing patient’s personal information. |

#### Response Object

| Field      | Type   | Character Limit | Required/Optional | Description                         |
| :--------- | :----- | :-------------- | :---------------- | :---------------------------------- |
| patientKey | String | 50              | Required          | Unique patient ID in Client system. |
| message    | String | max             | Required          | Status messages string.             |

# Update Patient Request

#### Request Object

| Field   | Type                                                                                       | Character Limit | Required/Optional | Description                                       |
| :------ | :----------------------------------------------------------------------------------------- | :-------------- | :---------------- | :------------------------------------------------ |
| patient | Object [(patient)](https://docs.healthdyne.com/v2.171/docs/patient-request-fields#patient) |                 | Required          | Object containing patient’s personal information. |

#### Response Object

| Field      | Type   | Character Limit | Required/Optional | Description                         |
| :--------- | :----- | :-------------- | :---------------- | :---------------------------------- |
| patientKey | String | 50              | Required          | Unique patient ID in Client system. |
| message    | String | max             | Required          | Status messages string.             |