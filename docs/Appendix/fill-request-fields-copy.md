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

Use this object with `POST /v2/fill`.

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `fillRequestKey` | String | Yes | Client-assigned key. Maximum 50 characters. |
| `scriptKeys` | Array of strings | Yes | One or more unique prescription keys for the same patient. |
| `shipping` | Object | Yes | Address and method. [Shipping Data Object](doc:fill-request-fields#shipping-data-object) |
| `insurance` | Object | No | Order-level insurance and payment details. [Insurance Data Object](doc:fill-request-fields#insurance-data-object) |

[Per-prescription request object](doc:fill-request-fields#request-object-1)

# Shipping

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `address` | Object | Yes | Delivery address. [Address Data Object](#address) |
| `shippingCode` | String | Yes | Supported shipping method. Maximum 10 characters. [Shipping Codes](#shipping-codes) |
| `saturdayDelivery` | Boolean | No | Defaults to false. Use true with a shipping method that supports Saturday delivery. |
| `signatureRequired` | Boolean | No | Defaults to false. Use true when delivery requires a signature. |

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

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `line1` | String | Yes | Street address, up to 40 characters. |
| `line2` | String | No | Additional address line, up to 40 characters. |
| `line3` | String | No | Additional address line, up to 40 characters. |
| `city` | String | Yes | City, up to 35 characters. |
| `state` | String | Yes | Two-letter state code. |
| `zipCode` | String | Yes | Five-digit ZIP or ZIP+4. |
| `countryCode` | String | No | Two-letter country code when supplied. |

