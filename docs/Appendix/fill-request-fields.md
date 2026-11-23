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
For current model additions and operation-specific distinctions, see [Current HD Order API Models](doc:current-order-api-models).
<Callout icon="📃" theme="default">
  ### Note:

  An empty string "" is considered a value and validation rules will apply (length/valid code/etc). Only null or missing elements will use default values.
</Callout>

<br />

# Fill Request Status Constant Data Objects

### Submitted

| Field        | Type     | Character Limit                      | Required/Optional | Description                                                                            |
| :----------- | :------- | :----------------------------------- | :---------------- | :------------------------------------------------------------------------------------- |
| eventId      | String   | 4 bytes (32-bit signed int)          | Required          | Unique Event Identifier for the Fill Request.                                          |
| eventDateUtc | DateTime | YYYY-MM-DD T HH:MM:SS.microseconds Z | Required          | Date and time of the event in UTC (ISO 8601).                                          |
| scriptKeys   | Array    | 50 per value                         | Required          | List of Array of scriptKey(s) (scriptKey is unique Id associated with script request). |

### RxVerified

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
        eventId
      </td>

      <td>
        String
      </td>

      <td>
        4 bytes (32-bit signed int)
      </td>

      <td>
        Required
      </td>

      <td>
        Unique Event Identifier for the Fill Request.
      </td>
    </tr>

    <tr>
      <td>
        eventDateUtc
      </td>

      <td>
        DateTime
      </td>

      <td>
        YYYY-MM-DD T HH:MM:SS.microseconds Z
      </td>

      <td>
        Required
      </td>

      <td>
        Date and time of the event in UTC (ISO 8601).
      </td>
    </tr>

    <tr>
      <td>
        scriptKey
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
        Unique ID associated with script request.
      </td>
    </tr>

    <tr>
      <td>
        verifiedDate
      </td>

      <td>
        DateTime?
      </td>

      <td>
        YYYY-MM-DD T HH:MM:SS Z
      </td>

      <td>
        Optional
      </td>

      <td>
        Date and Time of Fill Request verified.
        **Note**: For null value this Field will not appear in response Json.
      </td>
    </tr>

    <tr>
      <td>
        statusMessage
      </td>

      <td>
        String
      </td>

      <td>
        Max
      </td>

      <td>
        Required
      </td>

      <td>
        Status message from Pharmacy.
      </td>
    </tr>
  </tbody>
</Table>

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

### Renewed

| Field        | Type     | Character Limit                      | Required/Optional | Description                                                                            |
| :----------- | :------- | :----------------------------------- | :---------------- | :------------------------------------------------------------------------------------- |
| eventId      | String   | 4 bytes (32-bit signed int)          | Required          | Unique Event Identifier for the Fill Request.                                          |
| eventDateUtc | DateTime | YYYY-MM-DD T HH:MM:SS.microseconds Z | Required          | Date and time of the event in UTC (ISO 8601).                                          |
| scriptKeys   | Array    | 50 per value                         | Required          | List of Array of scriptKey(s) (scriptKey is unique Id associated with script request). |

### Rejected

| Field | Type | Description |
| :--- | :--- | :--- |
| `eventId` | String | HealthDyne event identifier. |
| `eventDateUtc` | Date-time | Event timestamp in UTC. |
| `scriptKeys` | Array of strings | Associated prescription keys when available. |
| `statusMessage` | String | Order rejection reason. |

# Fill Request Data Object

Use this object with `POST /v2/fill`.

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `fillRequestKey` | String | Yes | Client-assigned key. Maximum 50 characters. |
| `scriptKeys` | Array of strings | Yes | One or more unique prescription keys for the same patient. |
| `shipping` | Object | Yes | Address and method. [Shipping Data Object](#shipping-data-object) |
| `insurance` | Object | No | Order-level insurance and payment details. [Insurance Data Object](#insurance-data-object) |

# Shipping Data Object

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `address` | Object | Yes | Delivery address. [Address Data Object](#address-data-object) |
| `shippingCode` | String | Yes | Supported shipping method. Maximum 10 characters. [Shipping Codes](#shipping-codes) |
| `saturdayDelivery` | Boolean | No | Defaults to false. Use true with a shipping method that supports Saturday delivery. |
| `signatureRequired` | Boolean | No | Defaults to false. Use true when delivery requires a signature. |

# Shipping Codes

| Code     | Description                               | Notes             |
| :------- | :---------------------------------------- | :---------------- |
| POS 1C   | USPS Ground Advantage                     | Saturday delivery |
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

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `line1` | String | Yes | Street address, up to 40 characters. |
| `line2` | String | No | Additional address line, up to 40 characters. |
| `line3` | String | No | Additional address line, up to 40 characters. |
| `city` | String | Yes | City, up to 35 characters. |
| `state` | String | Yes | Two-letter state code. |
| `zipCode` | String | Yes | Five-digit ZIP or ZIP+4. |
| `countryCode` | String | No | Two-letter country code when supplied. |

# Insurance Data Object

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `planNumber` | String | Conditional | Supply an existing primary plan number or inline primary details. |
| `secondaryPlanNumber` | String | Conditional | Existing secondary plan number. Secondary coverage is required with tertiary coverage. |
| `tertiaryPlanNumber` | String | No | Existing tertiary plan number. Supply primary and secondary coverage when using this field. |
| `coPay` | String | Yes | Numeric payment amount when insurance is present. Maximum 8 characters. |
| `transactionNumber` | String | Yes | Payment transaction identifier when insurance is present. |
| `personCode` | String | No | Person code when applicable. |
| `bin` | String | For inline details | 4–6 digits. |
| `groupNumber` | String | For inline details | Insurance group number, up to 15 characters. |
| `memberId` | String | For inline details | Member ID, up to 20 characters, without special characters. |
| `pcn` | String | For inline details | Processor control number, up to 10 characters. |
| `relationship` | String | For inline details if relationshipCode is absent | One digit from 0 through 8. [Relationship Codes](#relationship-codes) |
| `relationshipCode` | String | For inline details if relationship is absent | Supported relationship code. |

Use distinct plan numbers across coverage levels.

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

| Field | Type | Description |
| :--- | :--- | :--- |
| `fillRequestKey` | String | Client-assigned key for the Fill Request. |
| `submitted` | Array | [Submitted](#submitted) events. |
| `rxVerified` | Array | [RxVerified](#rxverified) events. |
| `rxShipped` | Array | [RxShipped](#rxshipped) events. |
| `rxIssue` | Array | [RxIssue](#rxissue) events. |
| `rxCanceled` | Array | [RxCanceled](#rxcanceled) events. |
| `rejected` | Array | [Rejected](#rejected) events. |
| `renewed` | Array | [Renewed](#renewed) events. |

Event arrays can be empty. If no matching record is visible, the API returns HTTP 200 with a problem details body whose `detail` is `No record(s) found`.

## SUBMIT Fill Request

#### Request Object

Use this object with `POST /v2/fill`.

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `fillRequestKey` | String | Yes | Client-assigned key. Maximum 50 characters. |
| `scriptKeys` | Array of strings | Yes | One or more unique prescription keys for the same patient. |
| `shipping` | Object | Yes | Address and method. [Shipping Data Object](#shipping-data-object) |
| `insurance` | Object | No | Order-level insurance and payment details. [Insurance Data Object](#insurance-data-object) |

# Shipping Data Object

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `address` | Object | Yes | Delivery address. [Address Data Object](#address-data-object) |
| `shippingCode` | String | Yes | Supported shipping method. Maximum 10 characters. [Shipping Codes](#shipping-codes) |
| `saturdayDelivery` | Boolean | No | Defaults to false. Use true with a shipping method that supports Saturday delivery. |
| `signatureRequired` | Boolean | No | Defaults to false. Use true when delivery requires a signature. |

#### Response Object

| Field          | Type   | Character Limit | Required/Optional | Description                                                               |
| :------------- | :----- | :-------------- | :---------------- | :------------------------------------------------------------------------ |
| fillRequestKey | String | 50              | Required          | Unique ID assigned by sending pharmacy to each fill request for tracking. |
| message        | String | Max             | Required          | Status messages string.                                                   |

***

## SUBMIT Fill Request

#### Request Object

Use this object with `POST /v2/fill/fillRequest`.

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `fillRequestKey` | String | Yes | Client-assigned key. Maximum 50 characters. |
| `scriptsKeys` | Array of objects | Yes | One or more unique entries for the same patient. [Prescription entry](#scriptskeys-data-object) |
| `shipping` | Object | Yes | Address and method. [Shipping Data Object](#shipping-data-object-2) |
| `transactionNumber` | String | Yes | Client transaction reference. |
| `paymentCardSequenceNumber` | String | No | Digits-only sequence number for a card on the patient profile. |
| `otcItems` | Array of objects | No | Eligible over-the-counter items. [OTC item object](#otc-item-data-object) |

# scriptsKeys Data Object

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `scriptsKey` | String | Yes | Prescription key, up to 50 characters. |
| `patientInsurance` | Object or null | No | Omit or send null for applicable default plan handling. [Patient insurance](#patientinsurance-data-object) |

# patientInsurance Data Object

Use flat fields, nested coverage objects, or a combination. Supply primary coverage whenever you send insurance. Tertiary requires primary and secondary. Plans across levels must be distinct. Flat and nested values for the same level must agree.

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `planNumber` | String | Conditional | Supply an existing primary plan number or inline primary details. |
| `secondaryPlanNumber` | String | Conditional | Existing secondary plan number. Secondary coverage is required with tertiary coverage. |
| `tertiaryPlanNumber` | String | No | Existing tertiary plan number. Supply primary and secondary coverage when using this field. |
| `primaryInsurance` | Object | No | Existing plan number or inline coverage details. |
| `secondaryInsurance` | Object | No | Existing plan number or inline coverage details. |
| `tertiaryInsurance` | Object | No | Existing plan number or inline coverage details. |
| `bin, pcn, groupNumber, memberId, relationship` | Strings | Conditional | Inline primary coverage fields in the flat representation. The flat representation also accepts relationshipCode. |
| `clientItemCost` | Number | Yes | Client payment amount. |
| `clientDispenseFee` | Number | Yes | Client payment amount. |
| `clientOtherFee` | Number | Yes | Client payment amount. |
| `clientCoPay` | Number | Yes | Client copay. Its numeric representation is limited to eight characters. |

### Nested coverage objects

| Object | Existing plan number field |
| :--- | :--- |
| `primaryInsurance` | `planNumber` |
| `secondaryInsurance` | `secondaryPlanNumber` |
| `tertiaryInsurance` | `tertiaryPlanNumber` |

For inline details, use these fields. If you also submit a plan number for the same level, it must match the resolved plan.

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `bin` | String | Yes | 4–6 digits. |
| `pcn` | String or null | No | Optional for per-prescription inline details. A nonblank value has a 10-character maximum. Omitted, null, empty, and whitespace-only values are accepted. |
| `groupNumber` | String | Yes | Insurance group number, up to 15 characters. |
| `memberId` | String | Yes | Member ID, up to 20 characters, without special characters. |
| `relationship` | String | Yes | One digit from 0 through 8. [Relationship Codes](#relationship-codes) |

### OTC Item Data Object

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `productId` | String | Yes | Product identifier mapped to an eligible client NDC. Maximum 20 characters. |
| `quantity` | Integer | Yes | Whole number greater than zero. |

Include at least one prescription. Unsupported products and invalid quantities return HTTP 400.

# Shipping Data Object

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `address` | Object | Yes | Delivery address. [Address Data Object](#address-data-object) |
| `shippingCode` | String | Yes | Supported shipping method. Maximum 10 characters. [Shipping Codes](#shipping-codes) |
| `saturdayDelivery` | Boolean | No | Defaults to false. Use true with a shipping method that supports Saturday delivery. |
| `signatureRequired` | Boolean | No | Defaults to false. Use true when delivery requires a signature. |

#### Response Object

| Field          | Type   | Character Limit | Required/Optional | Description                                                               |
| :------------- | :----- | :-------------- | :---------------- | :------------------------------------------------------------------------ |
| fillRequestKey | String | 50              | Required          | Unique ID assigned by sending pharmacy to each fill request for tracking. |
| message        | String | Max             | Required          | Status messages string.                                                   |

<br />

***

## UPDATE Fill Request

#### Request Object

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `fillRequestKey` | String | Yes | Existing Fill Request key. Maximum 50 characters. |
| `shipping` | Object | Yes | Order-level address and method. [Shipping Data Object](#shipping-data-object) |

#### Response Object

| Field          | Type   | Character Limit | Required/Optional | Description                                                               |
| :------------- | :----- | :-------------- | :---------------- | :------------------------------------------------------------------------ |
| fillRequestKey | String | 50              | Required          | Unique ID assigned by sending pharmacy to each fill request for tracking. |
| message        | String | Max             | Required          | Status messages string.                                                   |

***

## CANCEL Fill Request

#### Request Object

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `fillRequestKey` | String | Yes | Existing Fill Request key. Maximum 50 characters. |
| `scriptKeys` | Array of strings | No | Associated lines to cancel. Omit or send an empty array for whole-order cancellation. |
| `cancelReason` | String | Yes | Reason for cancellation. Maximum 255 characters. |

#### Response Object

| Field          | Type   | Character Limit | Required/Optional | Description                                                               |
| :------------- | :----- | :-------------- | :---------------- | :------------------------------------------------------------------------ |
| fillRequestKey | String | 50              | Required          | Unique ID assigned by sending pharmacy to each fill request for tracking. |
| message        | String | Max             | Required          | Status messages string.                                                   |

<br />