---
title: Mailbox Data Object (Schemas)
deprecated: false
hidden: false
metadata:
  robots: index
---
> 📃 Note:
>
> An empty string "" is considered a value and validation rules will apply (length/valid code/etc). Only null or missing elements will use default values.

# Mailbox fetch parameters

#### Query Parameter

| Parameter    | Type | Character Limit | Required/Optional | Description                                                                                                                                            |
| :----------- | :--- | :-------------- | :---------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------- |
| messageCount | Int  | 3               | Required          | used to define how many messages should be returned per batch. Maximum will be 100 messages. if no value passed, the default is 100 messages per batch |

# RxTransfer event Type

#### RxTransfer Response Object

| Field         | Type                                                                                                          | Character Limit | Description                                                                              |
| :------------ | :------------------------------------------------------------------------------------------------------------ | :-------------- | :--------------------------------------------------------------------------------------- |
| eventId       | String                                                                                                        | max             | Unique event identifier in HealthDyne system.                                            |
| eventDateUtc  | String                                                                                                        | 27              | UTC timestamp of when the event occurred.                                                |
| eventType     | String                                                                                                        | 50              | Type of event, e.g., "RXTRANSFER".                                                       |
| status        | String                                                                                                        | 20              | Current status of the event.                                                             |
| statusMessage | String                                                                                                        | max             | Descriptive message explaining the status.                                               |
| scriptKey     | String                                                                                                        | 50              | Unique identifier for the script being transferred which is initially defined by client. |
| detail        | [RxTransferDetailObject](https://docs.healthdyne.com/docs/mailbox-data-object-schemas#rxtransferdetailobject) |                 | Nested object containing extra details specific to the event type                        |

#### RxTransferDetailObject

| Field      | Type   | Character Limit | Description                        |
| :--------- | :----- | :-------------- | :--------------------------------- |
| patientKey | String | 50              | Unique identifier for the patient. |
| rxNumber   | String | 30              | Prescription number                |

# RxStatus event Type

#### RxStatus Response Object

| Field         | Type                                                                                                      | Character Limit | Description                                                                              |
| :------------ | :-------------------------------------------------------------------------------------------------------- | :-------------- | :--------------------------------------------------------------------------------------- |
| eventId       | String                                                                                                    | max             | Unique event identifier in HealthDyne system.                                            |
| eventDateUtc  | String                                                                                                    | 27              | UTC timestamp of when the event occurred.                                                |
| eventType     | String                                                                                                    | 50              | Type of event, e.g., "RXTRANSFER".                                                       |
| status        | String                                                                                                    | 20              | Current status of the event.                                                             |
| statusMessage | String                                                                                                    | max             | Descriptive message explaining the status.                                               |
| scriptKey     | String                                                                                                    | 50              | Unique identifier for the script being transferred which is initially defined by client. |
| patientKey    | String                                                                                                    | 50              | Unique identifier for the patient.                                                       |
| detail        | [RxStatusDetailObject](https://docs.healthdyne.com/docs/mailbox-data-object-schemas#rxstatusdetailobject) |                 | Nested object containing extra details specific to the event type                        |

#### RxStatusDetailObject

| Field  | Type   | Character Limit | Description                  |
| :----- | :----- | :-------------- | :--------------------------- |
| reason | String | 255             | Reason for the status if any |

# FillRequest event Type

#### FillRequest Response Object

| Field          | Type                                                                                                            | Character Limit | Description                                                                   |
| :------------- | :-------------------------------------------------------------------------------------------------------------- | :-------------- | :---------------------------------------------------------------------------- |
| eventId        | String                                                                                                          | max             | Unique event identifier in HealthDyne system.                                 |
| eventDateUtc   | String                                                                                                          | 27              | UTC timestamp of when the event occurred.                                     |
| eventType      | String                                                                                                          | 50              | Type of event, e.g., "RXTRANSFER".                                            |
| status         | String                                                                                                          | 20              | Current status of the event.                                                  |
| statusMessage  | String                                                                                                          | max             | Descriptive message explaining the status.                                    |
| fillRequestKey | String                                                                                                          | 50              | Unique identifier for the fill request  which is initially defined by client. |
| detail         | [FillRequestDetailObject](https://docs.healthdyne.com/docs/mailbox-data-object-schemas#fillrequestdetailobject) |                 | Nested object containing extra details specific to the event type             |

#### FillRequestDetailObject

| Field            | Type                                                                                             | Character Limit | Description                                                                              |
| :--------------- | :----------------------------------------------------------------------------------------------- | :-------------- | :--------------------------------------------------------------------------------------- |
| orderNumber      | String                                                                                           | 100             | order number                                                                             |
| scriptKey        | String                                                                                           | 50              | Unique identifier for the script being transferred which is initially defined by client. |
| fillNumber       | Int                                                                                              |                 | Shows how many fills have been fulfilled for this Rx                                     |
| remainingRefills | String                                                                                           | 10              | Show how many fill remaing for the Rx                                                    |
| refillByDate     | String                                                                                           |                 | Date recommended for refill                                                              |
| shipments        | \[[ShipmentObject](https://docs.healthdyne.com/docs/mailbox-data-object-schemas#shipmentobject)] |                 | shipment information                                                                     |

#### ShipmentObject

| Field          | Type                                                                                            | Character Limit | Description                                        |
| :------------- | :---------------------------------------------------------------------------------------------- | :-------------- | :------------------------------------------------- |
| address        | \[[AddressObject](https://docs.healthdyne.com/docs/mailbox-data-object-schemas#addressobject) ] |                 | address information.                               |
| trackingNumber | String                                                                                          | 50              | Package tracking number.                           |
| shipmentCode   | String                                                                                          | 20              | Code representing the shipment type.               |
| trackingUrl    | String                                                                                          | 10              | URL for tracking the shipment.                     |
| weight         | Int                                                                                             |                 | Weight of the shipment.                            |
| cost           | Int                                                                                             |                 | Shipping cost.                                     |
| dispensedQty   | String                                                                                          | 20              | Quantity of medication dispensed.                  |
| daysSupply     | String                                                                                          | 20              | Number of days the dispensed medication will last. |
| shipmentDate   | String                                                                                          | 30              | The date the shipment was sent.                    |

#### AddressObject

| Field    | Type   | Character Limit | Description            |
| :------- | :----- | :-------------- | :--------------------- |
| address1 | String | 255             | address 1 information. |
| address2 | String | 50              | address 2 information. |
| city     | String | 40              | Shipped to city.       |
| state    | String | 2               | Shipped to state.      |
| zipcode  | String | 5               | Shipped to zip code.   |

<br />

### Submitted

| Field        | Type     | Character Limit                      | Required/Optional | Description                                                                            |
| :----------- | :------- | :----------------------------------- | :---------------- | :------------------------------------------------------------------------------------- |
| eventId      | String   | 4 bytes (32-bit signed int)          | Required          | Unique Event Identifier for the Fill Request.                                          |
| eventDateUtc | DateTime | YYYY-MM-DD T HH:MM:SS.microseconds Z | Required          | Date and time of the event in UTC (ISO 8601).                                          |
| scriptKeys   | Array    | 50 per value                         | Required          | List of Array of scriptKey(s) (scriptKey is unique Id associated with script request). |

### RxVerified

| Field          | Type                                                                                                       | Character Limit                      | Description                                         |
| :------------- | :--------------------------------------------------------------------------------------------------------- | :----------------------------------- | :-------------------------------------------------- |
| eventId        | String                                                                                                     | 4 bytes (32-bit signed int)          | Unique Event Identifier for the Fill Request.       |
| eventDateUtc   | DateTime                                                                                                   | YYYY-MM-DD T HH:MM:SS.microseconds Z | Date and time of the event in UTC (ISO 8601).       |
| scriptKey      | String                                                                                                     | 50                                   | Unique ID associated with script request.           |
| verifiedDate   | DateTime                                                                                                   | YYYY-MM-DD T HH:MM:SS Z              | Date and Time of Fill Request verified.             |
| statusMessage  | String                                                                                                     | Max                                  | Status message from Pharmacy.                       |
| FillRequestKey | String                                                                                                     | 50                                   | Unique ID associated with fill request.             |
| detail         | Object [RxVerified detail](https://docs.healthdyne.com/docs/mailbox-data-object-schemas#rxverified-detail) |                                      | Contains details of fill request that was verified. |

### RxVerified detail

<br />

| Field        | Type                                                                                              | Character Limit             | Description                                          |
| :----------- | :------------------------------------------------------------------------------------------------ | :-------------------------- | :--------------------------------------------------- |
| orderNumber  | String                                                                                            | 4 bytes (32-bit signed int) | Unique Event Identifier for the Fill Request.        |
| scriptKey    | String                                                                                            | 50                          | Unique ID associated with script request.            |
| fillNumber   | String                                                                                            | 50                          | Shows how many fills have been fulfilled for this Rx |
| dispenseDrug | Object [dispenseDrug](https://docs.healthdyne.com/docs/mailbox-data-object-schemas#dispense-drug) |                             | Dispensed drug object.                               |

### Dispense Drug

| Field            | Type   | Character Limit             | Description                      |
| :--------------- | :----- | :-------------------------- | :------------------------------- |
| dispenseNDC      | String | 4 bytes (32-bit signed int) | NDC of drug that was dispensed.  |
| dispenseDrugName | String | 50                          | Drug name that was dispensed.    |
| daysSupply       | String | 50                          | Days the supply will last for.   |
| dispenseQuantity | String | 50                          | Dispensed quantity               |
| labelDirections  | String | 50                          | Drug usage label direction text. |
| dosageForm       | String | 50                          | Drug dosage form.                |
| drugStrength     | String | 50                          | Shows strength of the drug.      |
| drugStrengthUOM  | String | 50                          | Drug strength unit of measure.   |

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