---
title: Fill Request Fields (Updated Fields)
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

# Fill Request

| Field          | Type   | Character Limit | Required/Optional | Description                                                                                                   |
| :------------- | :----- | :-------------- | :---------------- | :------------------------------------------------------------------------------------------------------------ |
| fillRequestKey | String | 255             | Required          | Unique ID assigned by sending pharmacy to each fill request for tracking.                                     |
| scriptKeys     | Array  |                 | Optional          | List of Array of scriptKey(s) (scriptKey is unique Id associated with script request).                        |
| shipping       | Object |                 | Required          | Object containing shipping information for the order. See [Shipping](doc:fill-request-fields#shipping) table. |

# Shipping

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

# Address

| Field       | Type   | Character Limit | Required/Optional | Description                                        |
| :---------- | :----- | :-------------- | :---------------- | :------------------------------------------------- |
| line1       | String | 40              | Required          | Street Address                                     |
| line2       | String | 40              | Optional          | Street Address                                     |
| line3       | String | 40              | Optional          | Street Address                                     |
| city        | String | 20              | Required          | City                                               |
| state       | String | 2               | Required          | US State Abbreviation Code                         |
| zipCode     | String | 5               | Required          | Format NNNNN                                       |
| countryCode | String | 2               | Optional          | ISO-3166 2 character country code. Defaults to US. |