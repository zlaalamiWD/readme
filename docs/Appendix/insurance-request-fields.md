---
title: Insurance Request Fields
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

# Insurance Request

| Field      | Type   | Character Limit | Required/Optional | Description                                        |
| :--------- | :----- | :-------------- | :---------------- | :------------------------------------------------- |
| patientKey | String | 50              | Required          | Unique patient ID in Client system.                |
| insurance  | object |                 | Required          | Object containing patient's insurance information. |

# Insurance Object

| Field            | Type   | Character Limit | Required/Optional | Description                                              |
| :--------------- | :----- | :-------------- | :---------------- | :------------------------------------------------------- |
| policyHolderId   | string | 20              | Required          | Insurance policy/member ID.                              |
| bin              | String | 4-6             | Required          | Insurance BIN information. Minimum of 4 digits required. |
| groupId          | String | 15              | Optional          | Insurance group Id information.                          |
| pcn              | String | 10              | Optional          | Insurance PCN information.                               |
| personCode       | String | 3               | Optional          | Number 0 to 9.                                           |
| relationshipCode | String | 1               | Optional          | Number 0 to 9. See relationship code table below.        |

# Relationship Codes

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