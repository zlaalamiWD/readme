---
title: Renewal Request Data Object (Schemas)
deprecated: false
hidden: false
metadata:
  robots: index
---
> 📃 Note:
>
> An empty string "" is considered a value and validation rules will apply (length/valid code/etc). Only null or missing elements will use default values.

# Renewal Request Data Object

| Field          | Type                                                                                                | Character Limit | Description                                                                  |
| :------------- | :-------------------------------------------------------------------------------------------------- | :-------------- | :--------------------------------------------------------------------------- |
| fillRequestKey | String                                                                                              | 50              | Unique ID assigned by sending pharmacy to each renewal request for tracking. |
| scriptKeys     | Object [scriptKeys](https://docs.healthdyne.com/docs/renewal-request-fields#scriptkeys-data-object) | 50 per value    | List of Array of scriptKeys Object.                                          |
| shipping       | Object [(shipping)](https://docs.healthdyne.com/docs/renewal-request-fields#shipping-data-object)   |                 | Object containing shipping information for the order.                        |

# scriptKeys Data Object

| Field            | Type                                                                                                            | Character Limit | Required/Optional | Description                                           |
| :--------------- | :-------------------------------------------------------------------------------------------------------------- | :-------------- | :---------------- | :---------------------------------------------------- |
| scriptKey        | String                                                                                                          | 50              | Required          | Unique Id associated with script request              |
| patientInsurance | Object [patientInsurance](https://docs.healthdyne.com/docs/renewal-request-fields#patientinsurance-data-object) |                 | Required          | Object containing shipping information for the order. |

# patientInsurance Data Object

| Field               | Type   | Character Limit | Required/Optional | Description                                                                                                   |
| :------------------ | :----- | :-------------- | :---------------- | :------------------------------------------------------------------------------------------------------------ |
| planNumber          | String | 10              | Required          | An identifier representing a specific insurance or benefit plan associated with a transaction for the client. |
| secondaryPlanNumber | String | 10              | Required          | An identifier representing a specific insurance or benefit plan associated with a transaction for the client. |
| tertiaryPlanNumber  | String | 10              | Required          | An identifier representing a specific insurance or benefit plan associated with a transaction for the client. |

# Shipping Data Object

| Field   | Type                                                                                            | Character Limit | Required/Optional | Description                                                       |
| :------ | :---------------------------------------------------------------------------------------------- | :-------------- | :---------------- | :---------------------------------------------------------------- |
| address | Object [(address)](https://docs.healthdyne.com/docs/renewal-request-fields#address-data-object) |                 | Required          | Object containing address information for order to be shipped to. |

# Address Data Object

| Field       | Type   | Character Limit | Required/Optional | Description                                        |
| :---------- | :----- | :-------------- | :---------------- | :------------------------------------------------- |
| line1       | String | 40              | Required          | Street Address                                     |
| line2       | String | 40              | Optional          | Street Address                                     |
| line3       | String | 40              | Optional          | Street Address                                     |
| city        | String | 35              | Required          | City                                               |
| state       | String | 2               | Required          | US State Abbreviation Code                         |
| zipCode     | String | 10              | Required          | Format NNNNN or NNNNN-NNNN                         |
| countryCode | String | 2               | Optional          | ISO-3166 2 character country code. Defaults to US. |