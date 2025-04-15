---
title: Insurance Data Object (Schemas)
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

# Get Insurance Data Object

#### Query Parameter

| Parameter  |    | Type   | Character Limit | Required/Optional | Description                         |
| :--------- | :- | :----- | :-------------- | :---------------- | :---------------------------------- |
| patientKey |    | String | 50              | Required          | Unique patient ID in Client system. |

**Response Object**

| Field      |    | Type                                                                                                                 | Character Limit | Required/Optional | Description                                        |
| :--------- | :- | :------------------------------------------------------------------------------------------------------------------- | :-------------- | :---------------- | :------------------------------------------------- |
| patientKey |    | String                                                                                                               | 50              | Required          | Unique patient ID in Client system.                |
| insurance  |    | Object\[[InsuranceDataObject](https://docs.healthdyne.com/v2.171/docs/insurance-request-fields#insurancedataobject)] |                 | Required          | Object containing patient's insurance information. |

#### InsuranceDataObject

| Field             | Type   | Character Limit | Required/Optional | Description                                                                                                                                |
| :---------------- | :----- | :-------------- | :---------------- | :----------------------------------------------------------------------------------------------------------------------------------------- |
| policyHolderId    | string | 20              | Required          | Insurance policy holder ID                                                                                                                 |
| bin               | String | 4-6             | Required          | Insurance BIN information. Minimum of 4 digits required.                                                                                   |
| groupId           | String | 15              | Optional          | Insurance group Id information.                                                                                                            |
| pcn               | String | 10              | Optional          | Insurance PCN information.                                                                                                                 |
| personCode        | String | 3               | Optional          | Number 0 to 9.                                                                                                                             |
| relationshipCode  | String | 1               | Optional          | Number 0 to 9. See relationship code table \[[below](https://docs.healthdyne.com/v2.171/docs/insurance-request-fields#relationship-codes)] |
| insuranceMemberId | String | 20              | Optional          | HealthDyne Member ID                                                                                                                       |

#### Relationship Codes

| code | Description                    |
| :--- | :----------------------------- |
| 0    | Relation is  NOT SPECIFIED     |
| 1    | Relation is CARDHOLDER         |
| 2    | Relation is SPOUSE             |
| 3    | Relation is CHILD              |
| 4    | Relation is OTHER DEPENDENT    |
| 5    | Relation is STUDENT DEPENDENT  |
| 6    | Relation is DISABLED DEPENDENT |
| 7    | Relation is ADULT DEPENDENT    |
| 8    | Relation is SIGNIFICANT OTHER  |

# Create Insurance Data Object

#### Request Object

| Field      | Type                                                                                                                              | Character Limit | Required/Optional | Description                                        |
| :--------- | :-------------------------------------------------------------------------------------------------------------------------------- | :-------------- | :---------------- | :------------------------------------------------- |
| patientKey | String                                                                                                                            | 50              | Required          | Unique patient ID in Client system.                |
| insurance  | Object\[[CreateInsuranceDataObject](https://docs.healthdyne.com/v2.171/docs/insurance-request-fields#createinsurancedataobject) ] |                 | Required          | Object containing patient's insurance information. |

#### CreateInsuranceDataObject

| Field             | Type   | Character Limit | Required/Optional | Description                                              |
| :---------------- | :----- | :-------------- | :---------------- | :------------------------------------------------------- |
| policyHolderId    | string | 20              | Required          | Insurance policy holder ID                               |
| bin               | String | 4-6             | Required          | Insurance BIN information. Minimum of 4 digits required. |
| groupId           | String | 15              | Optional          | Insurance group Id information.                          |
| pcn               | String | 10              | Optional          | Insurance PCN information.                               |
| personCode        | String | 3               | Optional          | Number 0 to 9.                                           |
| relationshipCode  | String | 1               | Optional          | Number 0 to 9. See relationship code table below.        |
| insuranceMemberID | String | 20              | Optional          | HealthDyne Member ID                                     |

#### Response Object

| Field      | Type   | Character Limit | Required/Optional | Description                         |
| :--------- | :----- | :-------------- | :---------------- | :---------------------------------- |
| patientKey | String | 50              | Required          | Unique patient ID in Client system. |
| planNumber | String | 40              | Required          | Insurance Plan Number               |
| message    | String | Max             | Required          | Plan added to patient profile.      |

# Delete Insurance Data Object

#### Query Parameter

| Parameter  |    | Type   | Character Limit | Required/Optional | Description                         |
| :--------- | :- | :----- | :-------------- | :---------------- | :---------------------------------- |
| patientKey |    | String | 50              | Required          | Unique patient ID in Client system. |
| planNumber |    | String | 40              | Required          | Insurance Plan Number               |

#### Response Object

| Field      | Type   | Character Limit | Required/Optional | Description                                               |
| :--------- | :----- | :-------------- | :---------------- | :-------------------------------------------------------- |
| patientKey | String | 50              | Required          | Unique patient ID in Client system.                       |
| planNumber | String | 40              | Required          | Insurance Plan Number                                     |
| message    | String | Max             | Required          | Patient Insurance plan number is inactivated successfully |