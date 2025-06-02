---
title: Fill Request Data Object (Schemas)
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

<br />

# Fill Request Status Constant Data Objects

### Submitted

| Field        | Type     | Character Limit                      | Required/Optional | Description                                                                            |
| :----------- | :------- | :----------------------------------- | :---------------- | :------------------------------------------------------------------------------------- |
| eventId      | String   | 4 bytes (32-bit signed int)          | Required          | Unique Event Identifier for the Fill Request.                                          |
| eventDateUtc | DateTime | YYYY-MM-DD T HH:MM:SS.microseconds Z | Required          | Date and time of the event in UTC (ISO 8601).                                          |
| scriptKeys   | Array    | 50 per value                         | Required          | List of Array of scriptKey(s) (scriptKey is unique Id associated with script request). |

### RxVerified

| Field         | Type     | Character Limit                      | Required/Optional | Description                                   |
| :------------ | :------- | :----------------------------------- | :---------------- | :-------------------------------------------- |
| eventId       | String   | 4 bytes (32-bit signed int)          | Required          | Unique Event Identifier for the Fill Request. |
| eventDateUtc  | DateTime | YYYY-MM-DD T HH:MM:SS.microseconds Z | Required          | Date and time of the event in UTC (ISO 8601). |
| scriptKey     | String   | 50                                   | Required          | Unique ID associated with script request.     |
| verifiedDate  | DateTime | YYYY-MM-DD T HH:MM:SS Z              | Required          | Date and Time of Fill Request verified.       |
| statusMessage | String   | Max                                  | Required          | Status message from Pharmacy.                 |

### RxShipped

| Field          | Type     | Character Limit                      | Required/Optional | Description                                   |
| :------------- | :------- | :----------------------------------- | :---------------- | :-------------------------------------------- |
| eventId        | String   | 4 bytes (32-bit signed int)          | Required          | Unique Event Identifier for the Fill Request. |
| eventDateUtc   | DateTime | YYYY-MM-DD T HH:MM:SS.microseconds Z | Required          | Date and time of the event in UTC (ISO 8601). |
| scriptKey      | String   | 50                                   | Required          | Unique ID associated with script request.     |
| shipmentDate   | DateTime | YYYY-MM-DD T HH:MM:SS Z              | Required          | Date and Time of Fill Request Shipped.        |
| trackingNumber | String   | 40                                   | Required          | Shipment tracking number.                     |

### RxIssue

| Field        | Type     | Character Limit                      | Required/Optional | Description                                   |
| :----------- | :------- | :----------------------------------- | :---------------- | :-------------------------------------------- |
| eventId      | String   | 4 bytes (32-bit signed int)          | Required          | Unique Event Identifier for the Fill Request. |
| eventDateUtc | DateTime | YYYY-MM-DD T HH:MM:SS.microseconds Z | Required          | Date and time of the event in UTC (ISO 8601). |
| scriptKey    | String   | 50                                   | Required          | Unique ID associated with script request.     |
| issueMessage | String   | Max                                  | Required          | Issue message from Pharmacy.                  |

### RxCanceled

| Field         | Type     | Character Limit                      | Required/Optional | Description                                   |
| :------------ | :------- | :----------------------------------- | :---------------- | :-------------------------------------------- |
| eventId       | String   | 4 bytes (32-bit signed int)          | Required          | Unique Event Identifier for the Fill Request. |
| eventDateUtc  | DateTime | YYYY-MM-DD T HH:MM:SS.microseconds Z | Required          | Date and time of the event in UTC (ISO 8601). |
| scriptKey     | String   | 50                                   | Required          | Unique ID associated with script request.     |
| statusMessage | String   | Max                                  | Required          | Status message from Pharmacy.                 |

# Fill Request Data Object

| Field          | Type                                                                                             | Character Limit | Required/Optional | Description                                                                            |
| :------------- | :----------------------------------------------------------------------------------------------- | :-------------- | :---------------- | :------------------------------------------------------------------------------------- |
| fillRequestKey | String                                                                                           | 50              | Required          | Unique ID assigned by sending pharmacy to each fill request for tracking.              |
| scriptKeys     | Array                                                                                            | 50              | Required          | List of Array of scriptKey(s) (scriptKey is unique Id associated with script request). |
| shipping       | Object [(shipping)](https://docs.healthdyne.com/docs/fill-request-fields#shipping-data-object)   |                 | Required          | Object containing shipping information for the order.                                  |
| insurance      | Object [(insurance)](https://docs.healthdyne.com/docs/fill-request-fields#insurance-data-object) |                 | Optional          | Optionally specify insurance information to be used on the fill request.               |

# Shipping Data Object

| Field             | Type                                                                                         | Character Limit | Required/Optional | Description                                                                                                                                                                                                         |
| :---------------- | :------------------------------------------------------------------------------------------- | :-------------- | :---------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| address           | Object [(address)](https://docs.healthdyne.com/docs/fill-request-fields#address-data-object) |                 | Required          | Object containing address information for order to be shipped to.                                                                                                                                                   |
| ShippingCode      | String                                                                                       | 10              | Required          | Shipping method to be used for the order. See [Shipping Codes](https://docs.healthdyne.com/docs/fill-request-fields#shipping-codes)below                                                                            |
| SaturdayDelivery  | Boolean                                                                                      | true/false      | Optional          | Values: True/False. Saturday Delivery is an option for certain shipping codes, depending on the carrier. To have an order delivered on a Saturday, select the correct Shipping Code and then set this flag to true. |
| SignatureRequired | Boolean                                                                                      | true/false      | Optional          | Values: True/False. Select the option if the package requires a signature                                                                                                                                           |

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
| UPS 3DS  | UPS 3 Day Select                          | Saturday delivery |
| UPS USG  | UPS-USPS Sure Post                        | Saturday delivery |

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

# Insurance Data Object

| Field               | Type   | Character Limit | Required/Optional | Description                                                                                                                                                                                                                                                                                                                                      |
| :------------------ | :----- | :-------------- | :---------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| planNumber          | String | 100             | Required          | Insurance plan number to be used on order previously provided by HealthDyne on a create Insurance response.                                                                                                                                                                                                                                      |
| secondaryPlanNumber | String | 10              | Optional          | An identifier representing an additional insurance or benefit plan that serves as a secondary source of coverage for the client in a transaction is used when the primary plan does not fully cover the service or product. (Note: This attribute is only required if you are planning to provide tertiary insurance, otherwise it is optional.) |
| tertiaryPlanNumber  | String | 10              | Optional          | An identifier representing a third-tier insurance or benefit plan provides supplemental coverage when both the primary and secondary plans do not fully cover the transaction for the client.                                                                                                                                                    |
| coPay               | String | 6               | Required          | Payment collected from the patient at checkout. Format "xx.xx" or "xxx.xx"                                                                                                                                                                                                                                                                       |
| transactionNumber   | String | Max             | Required          | The payment transaction number. This should be the stripe transaction number if payment is managed by HealthDyne.                                                                                                                                                                                                                                |
| personCode          | String | 3               | Optional          | Number 0 to 9.                                                                                                                                                                                                                                                                                                                                   |
| relationshipCode    | String | 1               | Optional          | Number 0 to 9. See relationship code table \[[below](https://docs.healthdyne.com/docs/fill-request-fields#relationship-codes)]                                                                                                                                                                                                                   |

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

***

## GET Fill Request

#### Query Parameter

| Field          | Type   | Character Limit | Required/Optional | Description                                                               |
| :------------- | :----- | :-------------- | :---------------- | :------------------------------------------------------------------------ |
| fillRequestKey | String | 50              | Required          | Unique ID assigned by sending pharmacy to each fill request for tracking. |

#### Response Object

| Field          | Type                                                                                         | Character Limit | Required/Optional | Description                                                               |
| :------------- | :------------------------------------------------------------------------------------------- | :-------------- | :---------------- | :------------------------------------------------------------------------ |
| fillRequestKey | String                                                                                       | 50              | Required          | Unique ID assigned by sending pharmacy to each fill request for tracking. |
| submitted      | Array \[[submitted](https://docs.healthdyne.com/docs/mailbox-data-object-schemas#submitted)] |                 | Optional          | Array of submitted Objects containing event details.                      |
| rxVerified     | Array \[[rxVerified](https://docs.healthdyne.com/docs/fill-request-fields#rxverified)]       |                 | Optional          | Array of rxVerified objects containing verified information.              |
| rxShipped      | Array \[[rxshipped](https://docs.healthdyne.com/docs/fill-request-fields#rxshipped)]         |                 | Optional          | Array of rxShipped objects containing tracking/shipping information.      |
| rxIssue        | Array \[[rxissue](https://docs.healthdyne.com/docs/fill-request-fields#rxissue)]             |                 | Optional          | Array of rxIssue objects containing issued information.                   |
| rxCanceled     | Array \[[rxcanceled](https://docs.healthdyne.com/docs/fill-request-fields#rxcanceled)]       |                 | Optional          | Array of rxCanceled objects containing cancel reason information.         |
| renewed        | Array \[[renewed](https://docs.healthdyne.com/docs/fill-request-fields#submitted)]           |                 | Optional          | Array of submitted Objects containing event details.                      |

***

## SUBMIT Fill Request

#### Request Object

| Field          | Type                                                                                             | Character Limit | Required/Optional | Description                                                                            |
| :------------- | :----------------------------------------------------------------------------------------------- | :-------------- | :---------------- | :------------------------------------------------------------------------------------- |
| fillRequestKey | String                                                                                           | 50              | Required          | Unique ID assigned by sending pharmacy to each fill request for tracking.              |
| scriptKeys     | Array                                                                                            | 50 per value    | Required          | List of Array of scriptKey(s) (scriptKey is unique Id associated with script request). |
| shipping       | Object [(shipping)](https://docs.healthdyne.com/docs/fill-request-fields#shipping-data-object)   |                 | Required          | Object containing shipping information for the order.                                  |
| insurance      | Object [(insurance)](https://docs.healthdyne.com/docs/fill-request-fields#insurance-data-object) |                 | Optional          | Optionally specify insurance information to be used on the fill request.               |

# Shipping Data Object

| Field             | Type                                                                                         | Character Limit | Required/Optional | Description                                                                                                                                                                                                         |
| :---------------- | :------------------------------------------------------------------------------------------- | :-------------- | :---------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| address           | Object [(address)](https://docs.healthdyne.com/docs/fill-request-fields#address-data-object) |                 | Required          | Object containing address information for order to be shipped to.                                                                                                                                                   |
| ShippingCode      | String                                                                                       | 10              | Required          | Shipping method to be used for the order. See [Shipping Codes](https://docs.healthdyne.com/docs/fill-request-fields#shipping-codes)below                                                                            |
| SaturdayDelivery  | Boolean                                                                                      | true/false      | Optional          | Values: True/False. Saturday Delivery is an option for certain shipping codes, depending on the carrier. To have an order delivered on a Saturday, select the correct Shipping Code and then set this flag to true. |
| SignatureRequired | Boolean                                                                                      | true/false      | Optional          | Values: True/False. Select the option if the package requires a signature                                                                                                                                           |

#### Response Object

| Field          | Type   | Character Limit | Required/Optional | Description                                                               |
| :------------- | :----- | :-------------- | :---------------- | :------------------------------------------------------------------------ |
| fillRequestKey | String | 50              | Required          | Unique ID assigned by sending pharmacy to each fill request for tracking. |
| message        | String | Max             | Required          | Status messages string.                                                   |

***

## SUBMIT Fill Request

#### Request Object

| Field             | Type                                                                                               | Character Limit | Required/Optional | Description                                                               |
| :---------------- | :------------------------------------------------------------------------------------------------- | :-------------- | :---------------- | :------------------------------------------------------------------------ |
| fillRequestKey    | String                                                                                             | 50              | Required          | Unique ID assigned by sending pharmacy to each fill request for tracking. |
| scriptsKeys       | Object [scriptsKeys](https://docs.healthdyne.com/docs/fill-request-fields#scriptskeys-data-object) | 50 per value    | Required          | List of Array of scriptsKeys Object.                                      |
| shipping          | Object [(shipping)](https://docs.healthdyne.com/docs/fill-request-fields#shipping-data-object)     |                 | Required          | Object containing shipping information for the order.                     |
| transactionNumber | String                                                                                             |                 | Required          | A unique identifier assigned to each transaction by the client.           |

# scriptsKeys Data Object

| Field            | Type                                                                                                         | Character Limit | Required/Optional | Description                                           |
| :--------------- | :----------------------------------------------------------------------------------------------------------- | :-------------- | :---------------- | :---------------------------------------------------- |
| scriptsKey       | String                                                                                                       | 50              | Required          | Unique Id associated with script request              |
| patientInsurance | Object [patientInsurance](https://docs.healthdyne.com/docs/fill-request-fields#patientinsurance-data-object) |                 | Required          | Object containing shipping information for the order. |

# patientInsurance Data Object

| Field               | Type    | Character Limit | Required/Optional | Description                                                                                                                                                                                                                                                                                                                                      |
| :------------------ | :------ | :-------------- | :---------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| planNumber          | String  | 10              | Required          | An identifier representing a specific insurance or benefit plan associated with a transaction for the client.                                                                                                                                                                                                                                    |
| secondaryPlanNumber | String  | 10              | Optional          | An identifier representing an additional insurance or benefit plan that serves as a secondary source of coverage for the client in a transaction is used when the primary plan does not fully cover the service or product. (Note: This attribute is only required if you are planning to provide tertiary insurance, otherwise it is optional.) |
| tertiaryPlanNumber  | String  | 10              | Optional          | An identifier representing a third-tier insurance or benefit plan provides supplemental coverage when both the primary and secondary plans do not fully cover the transaction for the client.                                                                                                                                                    |
| clientItemCost      | Decimal |                 | Required          | The base cost of the item (e.g., medication, product, or service) billed to the client before any additional fees or discounts.                                                                                                                                                                                                                  |
|                     |         |                 |                   |                                                                                                                                                                                                                                                                                                                                                  |
| clientDispenseFee   | Decimal |                 | Required          | A fee charged to the client for the dispensing or handling of the item.                                                                                                                                                                                                                                                                          |
| clientOtherFee      | Decimal |                 | Required          | An additional fee billed to the client that does not fall under item cost or dispensing.                                                                                                                                                                                                                                                         |
| clientCoPay         | Decimal |                 | Required          | The portion of the transaction that the client is required to pay out-of-pocket.                                                                                                                                                                                                                                                                 |

# Shipping Data Object

| Field             | Type                                                                                         | Character Limit | Required/Optional | Description                                                                                                                                                                                                         |
| :---------------- | :------------------------------------------------------------------------------------------- | :-------------- | :---------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| address           | Object [(address)](https://docs.healthdyne.com/docs/fill-request-fields#address-data-object) |                 | Required          | Object containing address information for order to be shipped to.                                                                                                                                                   |
| ShippingCode      | String                                                                                       | 10              | Required          | Shipping method to be used for the order. See [Shipping Codes](https://docs.healthdyne.com/docs/fill-request-fields#shipping-codes)below                                                                            |
| SaturdayDelivery  | Boolean                                                                                      | true/false      | Optional          | Values: True/False. Saturday Delivery is an option for certain shipping codes, depending on the carrier. To have an order delivered on a Saturday, select the correct Shipping Code and then set this flag to true. |
| SignatureRequired | Boolean                                                                                      | true/false      | Optional          | Values: True/False. Select the option if the package requires a signature                                                                                                                                           |

#### Response Object

| Field          | Type   | Character Limit | Required/Optional | Description                                                               |
| :------------- | :----- | :-------------- | :---------------- | :------------------------------------------------------------------------ |
| fillRequestKey | String | 50              | Required          | Unique ID assigned by sending pharmacy to each fill request for tracking. |
| message        | String | Max             | Required          | Status messages string.                                                   |

<br />

***

## UPDATE Fill Request

#### Request Object

| Field          | Type                                                                                           | Character Limit | Required/Optional | Description                                                                            |
| :------------- | :--------------------------------------------------------------------------------------------- | :-------------- | :---------------- | :------------------------------------------------------------------------------------- |
| fillRequestKey | String                                                                                         | 50              | Required          | Unique ID assigned by sending pharmacy to each fill request for tracking.              |
| scriptKeys     | Array                                                                                          | 50 per value    | Required          | List of Array of scriptKey(s) (scriptKey is unique Id associated with script request). |
| shipping       | Object [(shipping)](https://docs.healthdyne.com/docs/fill-request-fields#shipping-data-object) |                 | Required          | Object containing shipping information for the order.                                  |

#### Response Object

| Field          | Type   | Character Limit | Required/Optional | Description                                                               |
| :------------- | :----- | :-------------- | :---------------- | :------------------------------------------------------------------------ |
| fillRequestKey | String | 50              | Required          | Unique ID assigned by sending pharmacy to each fill request for tracking. |
| message        | String | Max             | Required          | Status messages string.                                                   |

***

## CANCEL Fill Request

#### Request Object

| Field          | Type   | Character Limit | Required/Optional | Description                                                                            |
| :------------- | :----- | :-------------- | :---------------- | :------------------------------------------------------------------------------------- |
| fillRequestKey | String | 50              | Required          | Unique ID assigned by sending pharmacy to each fill request for tracking.              |
| scriptKeys     | Array  | 50 per value    | Required          | List of Array of scriptKey(s) (scriptKey is unique Id associated with script request). |
| cancelReason   | String | Max             | Required          | TBD                                                                                    |

#### Response Object

| Field          | Type   | Character Limit | Required/Optional | Description                                                               |
| :------------- | :----- | :-------------- | :---------------- | :------------------------------------------------------------------------ |
| fillRequestKey | String | 50              | Required          | Unique ID assigned by sending pharmacy to each fill request for tracking. |
| message        | String | Max             | Required          | Status messages string.                                                   |