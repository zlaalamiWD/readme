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

# Fill Request Status Constant Data Objects

### Submitted

| Field        | Type     | Character Limit | Required/Optional | Description                                                                            |
| :----------- | :------- | :-------------- | :---------------- | :------------------------------------------------------------------------------------- |
| eventId      | String   |                 | Required          | TBD                                                                                    |
| eventDateUtc | DateTime |                 | Required          | TBD                                                                                    |
| scriptKeys   | Array    |                 | Required          | List of Array of scriptKey(s) (scriptKey is unique Id associated with script request). |

### RxVerified

| Field         | Type     | Character Limit | Required/Optional | Description |
| :------------ | :------- | :-------------- | :---------------- | :---------- |
| eventId       | String   |                 | Required          | TBD         |
| eventDateUtc  | DateTime |                 | Required          | TBD         |
| scriptKey     | String   |                 | Required          |             |
| verifiedDate  | DateTime |                 | Required          |             |
| statusMessage | String   | Max             | Required          |             |

### RxShipped

| Field          | Type     | Character Limit | Required/Optional | Description |
| :------------- | :------- | :-------------- | :---------------- | :---------- |
| eventId        | String   |                 | Required          | TBD         |
| eventDateUtc   | DateTime |                 | Required          | TBD         |
| scriptKey      | String   |                 | Required          |             |
| shipmentDate   | DateTime |                 | Required          |             |
| trackingNumber | String   | 40              | Required          |             |

### RxIssue

| Field        | Type     | Character Limit | Required/Optional | Description |
| :----------- | :------- | :-------------- | :---------------- | :---------- |
| eventId      | String   |                 | Required          | TBD         |
| eventDateUtc | DateTime |                 | Required          | TBD         |
| scriptKey    | String   |                 | Required          |             |
| issueMessage | String   | Max             | Required          |             |

### RxCanceled

| Field         | Type     | Character Limit | Required/Optional | Description |
| :------------ | :------- | :-------------- | :---------------- | :---------- |
| eventId       | String   |                 | Required          | TBD         |
| eventDateUtc  | DateTime |                 | Required          | TBD         |
| scriptKey     | String   |                 | Required          |             |
| statusMessage | String   | Max             | Required          |             |

# Fill Request Data Object

| Field          | Type   | Character Limit | Required/Optional | Description                                                                                                   |
| :------------- | :----- | :-------------- | :---------------- | :------------------------------------------------------------------------------------------------------------ |
| fillRequestKey | String | 50              | Required          | Unique ID assigned by sending pharmacy to each fill request for tracking.                                     |
| scriptKeys     | Array  |                 | Required          | List of Array of scriptKey(s) (scriptKey is unique Id associated with script request).                        |
| shipping       | Object |                 | Required          | Object containing shipping information for the order. See [Shipping](doc:fill-request-fields#shipping) table. |
| insurance      | Object |                 | Optional          | Optionally specify insurance information to be used on the fill request.                                      |

# Shipping Data Object

| Field             | Type    | Character Limit | Required/Optional | Description                                                                                                                                                                                                        |
| :---------------- | :------ | :-------------- | :---------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| address           | Object  |                 | Required          | Object containing address information for order to be shipped to. See [Address](doc:fill-request-fields#address) table.                                                                                            |
| ShippingCode      | String  | 10              | Required          | Shipping method to be used for the order. See [Shipping Codes](doc:fill-request-fields#shipping-codes)below                                                                                                        |
| SaturdayDelivery  | Boolean | true/false      | Optional          | Values: True/False. Saturday Delivery is an option for certain shipping codes depending on the carrier. To have an order delivered on a Saturday, select the correct Shipping Code and then set this flag to true. |
| SignatureRequired | Boolean | true/false      | Optional          | Values: True/False. Select the option if the package requires a signature                                                                                                                                          |

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

| Field             | Type   | Character Limit | Required/Optional | Description                                                                                                          |
| :---------------- | :----- | :-------------- | :---------------- | :------------------------------------------------------------------------------------------------------------------- |
| planNumber        | String | 40              | Required          | Insurance plan number to be used on order that was previously provided by HealthDyne on a create Insurance response. |
| coPay             | String | 6               | Required          | Payment collected from the patient at checkout. Format "xx.xx" or "xxx.xx"                                           |
| transactionNumber | String |                 | Required          | The payment transaction number. This should be the stripe transaction number if payment is managed by HealthDyne.    |

***

<br />

## GET Fill Request

#### Query Parameter

| Field          | Type   | Character Limit | Required/Optional | Description                                                               |
| :------------- | :----- | :-------------- | :---------------- | :------------------------------------------------------------------------ |
| fillRequestKey | String | 50              | Required          | Unique ID assigned by sending pharmacy to each fill request for tracking. |

#### Response Object

| Field          | Type                                                                                       | Character Limit | Required/Optional | Description                                                               |
| :------------- | :----------------------------------------------------------------------------------------- | :-------------- | :---------------- | :------------------------------------------------------------------------ |
| fillRequestKey | String                                                                                     | 50              | Required          | Unique ID assigned by sending pharmacy to each fill request for tracking. |
| submitted      | Array [submitted](https://docs.healthdyne.com/v2.171/docs/fill-request-fields#submitted)   |                 | Optional          | Array of submitted Objects containing event details.                      |
| rxVerified     | Array [rxVerified](https://docs.healthdyne.com/v2.171/docs/fill-request-fields#rxverified) |                 | Optional          | Array of rxVerified objects containing verified information.              |
| rxShipped      | Array [rxshipped](https://docs.healthdyne.com/v2.171/docs/fill-request-fields#rxshipped)   |                 | Optional          | Array of rxShipped objects containing tracking/shipping information.      |
| rxIssue        | Array [rxissue](https://docs.healthdyne.com/v2.171/docs/fill-request-fields#rxissue)       |                 | Optional          | Array of rxIssue objects containing issued information.                   |
| rxCanceled     | Array [rxcanceled](https://docs.healthdyne.com/v2.171/docs/fill-request-fields#rxcanceled) |                 | Optional          | Array of rxCanceled objects containing cancel reason information.         |

<br />

## SUBMIT Fill Request

#### Request Object

| Field          | Type   | Character Limit | Required/Optional | Description                                                                                                   |
| :------------- | :----- | :-------------- | :---------------- | :------------------------------------------------------------------------------------------------------------ |
| fillRequestKey | String | 50              | Required          | Unique ID assigned by sending pharmacy to each fill request for tracking.                                     |
| scriptKeys     | Array  |                 | Required          | List of Array of scriptKey(s) (scriptKey is unique Id associated with script request).                        |
| shipping       | Object |                 | Required          | Object containing shipping information for the order. See [Shipping](doc:fill-request-fields#shipping) table. |
| insurance      | Object |                 | Optional          | Optionally specify insurance information to be used on the fill request.                                      |

#### Response Object

| Field          | Type   | Character Limit | Required/Optional | Description                                                               |
| :------------- | :----- | :-------------- | :---------------- | :------------------------------------------------------------------------ |
| fillRequestKey | String | 50              | Required          | Unique ID assigned by sending pharmacy to each fill request for tracking. |
| message        | String |                 | Required          | Status messages string.                                                   |

<br />

## UPDATE Fill Request

#### Request Object

| Field          | Type   | Character Limit | Required/Optional | Description                                                                                                   |
| :------------- | :----- | :-------------- | :---------------- | :------------------------------------------------------------------------------------------------------------ |
| fillRequestKey | String | 50              | Required          | Unique ID assigned by sending pharmacy to each fill request for tracking.                                     |
| scriptKeys     | Array  |                 | Required          | List of Array of scriptKey(s) (scriptKey is unique Id associated with script request).                        |
| shipping       | Object |                 | Required          | Object containing shipping information for the order. See [Shipping](doc:fill-request-fields#shipping) table. |

#### Response Object

| Field          | Type   | Character Limit | Required/Optional | Description                                                               |
| :------------- | :----- | :-------------- | :---------------- | :------------------------------------------------------------------------ |
| fillRequestKey | String | 50              | Required          | Unique ID assigned by sending pharmacy to each fill request for tracking. |
| message        | String |                 | Required          | Status messages string.                                                   |

<br />

## CANCEL Fill Request

#### Request Object

| Field          | Type   | Character Limit | Required/Optional | Description                                                                            |
| :------------- | :----- | :-------------- | :---------------- | :------------------------------------------------------------------------------------- |
| fillRequestKey | String | 50              | Required          | Unique ID assigned by sending pharmacy to each fill request for tracking.              |
| scriptKeys     | Array  |                 | Required          | List of Array of scriptKey(s) (scriptKey is unique Id associated with script request). |
| cancelReason   | String |                 | Required          | TBD                                                                                    |

#### Response Object

| Field          | Type   | Character Limit | Required/Optional | Description                                                               |
| :------------- | :----- | :-------------- | :---------------- | :------------------------------------------------------------------------ |
| fillRequestKey | String | 50              | Required          | Unique ID assigned by sending pharmacy to each fill request for tracking. |
| message        | String |                 | Required          | Status messages string.                                                   |