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

<Table align={["left","left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Type
      </th>

      <th>
        Character Limit
      </th>

      <th>
        Required/Optional
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        contactType
      </td>

      <td>
        String
      </td>

      <td>
        15
      </td>

      <td>
        Optional
      </td>

      <td>
        Patient Contact – Phone, Home Phone, Day Phone, Work Phone, Fax Number, Cellular Number, Alternate
      </td>
    </tr>

    <tr>
      <td>
        contactAddress
      </td>

      <td>
        String
      </td>

      <td>
        10
      </td>

      <td>
        Required
      </td>

      <td>
        Contact Details. For instance: Populate phone number if contact type is phone. Format:XXXXXXXXXX
      </td>
    </tr>

    <tr>
      <td>
        emailAddress
      </td>

      <td>
        String
      </td>

      <td>
        60
      </td>

      <td>
        Optional
      </td>

      <td>
        Patient Email Address or Email Id.
        **Note**: This field will be visible only if value is not null.
      </td>
    </tr>
  </tbody>
</Table>

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

<Table align={["left","left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Type
      </th>

      <th>
        Character Limit
      </th>

      <th>
        Required/Optional
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        patientKey
      </td>

      <td>
        String
      </td>

      <td>
        50
      </td>

      <td>
        Required
      </td>

      <td>
        Unique patient ID in Client system.
      </td>
    </tr>

    <tr>
      <td>
        firstName
      </td>

      <td>
        String
      </td>

      <td>
        35
      </td>

      <td>
        Required
      </td>

      <td>
        Patient's first name.
      </td>
    </tr>

    <tr>
      <td>
        lastName
      </td>

      <td>
        String
      </td>

      <td>
        35
      </td>

      <td>
        Required
      </td>

      <td>
        Patient's last name.
      </td>
    </tr>

    <tr>
      <td>
        gender
      </td>

      <td>
        String
      </td>

      <td>
        1
      </td>

      <td>
        Required
      </td>

      <td>
        Patient’s Gender – M, F or U
      </td>
    </tr>

    <tr>
      <td>
        epostPatientNumber
      </td>

      <td>
        String
      </td>

      <td>

      </td>

      <td>
        Optional
      </td>

      <td>
        Patient's ePost Number.
        **Note**: This field will only be visible for DTC client.
      </td>
    </tr>

    <tr>
      <td>
        patientLanguage
      </td>

      <td>
        String
      </td>

      <td>
        3
      </td>

      <td>
        Required
      </td>

      <td>
        Patient language must be ENG or SPA.
      </td>
    </tr>

    <tr>
      <td>
        birthDate
      </td>

      <td>
        DateTime
      </td>

      <td>
        YYYY-MM-DD
      </td>

      <td>
        Required
      </td>

      <td>
        Patient's Date of Birth
      </td>
    </tr>

    <tr>
      <td>
        healthCondition
      </td>

      <td>
        Array
      </td>

      <td>

      </td>

      <td>
        Optional
      </td>

      <td>
        Patient's health condition.
      </td>
    </tr>

    <tr>
      <td>
        address
      </td>

      <td>
        Object [(address)](doc:patient-request-fields#address)
      </td>

      <td>

      </td>

      <td>
        Required
      </td>

      <td>
        Object containing patient’s address information. See [Address](doc:patient-request-fields#address) table.
      </td>
    </tr>

    <tr>
      <td>
        contact
      </td>

      <td>
        Object [(contact)](doc:patient-request-fields#contact)
      </td>

      <td>

      </td>

      <td>
        Required
      </td>

      <td>
        Object containing patient’s contact information. See [Contact](doc:patient-request-fields#contact) table.
      </td>
    </tr>

    <tr>
      <td>
        externalMedications
      </td>

      <td>
        Array \[[externalMedications](doc:patient-request-fields#external-medications)]
      </td>

      <td>

      </td>

      <td>
        Optional
      </td>

      <td>
        Array containing patient’s external medications objects. List any external Medications the patient is taking for pharmacy to know if there is any drug interaction. If there are  external medications, then ensure all the object elements are populated. See [External Medications](doc:patient-request-fields#external-medications) table.
      </td>
    </tr>

    <tr>
      <td>
        pregnancyIndicator
      </td>

      <td>
        String
      </td>

      <td>
        1
      </td>

      <td>
        Required
      </td>

      <td>
        Patient's pregnancy status.
      </td>
    </tr>

    <tr>
      <td>
        allergies
      </td>

      <td>
        Array [\[allergies\]](doc:patient-request-fields#allergies)
      </td>

      <td>

      </td>

      <td>
        Optional
      </td>

      <td>
        Array containing patient’s allergy information. See the [Allergies](doc:patient-request-fields#allergies) table for valid list of allergies.
      </td>
    </tr>
  </tbody>
</Table>

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
| scriptKeys | Array | 50 per value    | Required          | Array of scriptKey(s) associated to Patient. |

# Create Patient Request

#### Request Object

| Field   | Type                                               | Character Limit | Required/Optional | Description                                       |
| :------ | :------------------------------------------------- | :-------------- | :---------------- | :------------------------------------------------ |
| patient | Object [(patient)](patient-request-fields#patient) |                 | Required          | Object containing patient’s personal information. |

#### Response Object

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Type
      </th>

      <th>
        Character Limit
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        patientKey
      </td>

      <td>
        String
      </td>

      <td>
        50
      </td>

      <td>
        Unique patient ID in Client system.
      </td>
    </tr>

    <tr>
      <td>
        message
      </td>

      <td>
        String
      </td>

      <td>
        max
      </td>

      <td>
        Status messages string.
      </td>
    </tr>

    <tr>
      <td>
        epostPatientNumber
      </td>

      <td>
        Integer
      </td>

      <td>

      </td>

      <td>
        Unique patient number from ePost.
        **Note**: This field will appear in response only if EPostRxPatientNumberEnabled flag for client is enabled.
      </td>
    </tr>
  </tbody>
</Table>

# Update Patient Request

#### Request Object

| Field   | Type                                               | Character Limit | Required/Optional | Description                                       |
| :------ | :------------------------------------------------- | :-------------- | :---------------- | :------------------------------------------------ |
| patient | Object [(patient)](patient-request-fields#patient) |                 | Required          | Object containing patient’s personal information. |

#### Response Object

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Type
      </th>

      <th>
        Character Limit
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        patientKey
      </td>

      <td>
        String
      </td>

      <td>
        50
      </td>

      <td>
        Unique patient ID in Client system.
      </td>
    </tr>

    <tr>
      <td>
        message
      </td>

      <td>
        String
      </td>

      <td>
        max
      </td>

      <td>
        Status messages string.
      </td>
    </tr>

    <tr>
      <td>
        epostPatientNumber
      </td>

      <td>
        Integer
      </td>

      <td>

      </td>

      <td>
        Unique patient number from ePost.
        **Note**: This field will appear in response only if EPostRxPatientNumberEnabled flag for client is enabled.
      </td>
    </tr>
  </tbody>
</Table>