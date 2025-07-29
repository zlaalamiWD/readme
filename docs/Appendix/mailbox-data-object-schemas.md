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

| Field             | Type   | Character Limit | Description                                                                                             |
| :---------------- | :----- | :-------------- | :------------------------------------------------------------------------------------------------------ |
| patientKey        | String | 50              | Unique identifier for the patient.                                                                      |
| rxNumber          | String | 30              | Prescription number                                                                                     |
| receivingPharmacy | String | 40              | receivingPharmacy will be added only for Script Outbound API mailbox Events of Routed and RoutingFailed |
| issueMessage      | String | 255             | issueMessage will be added only for Script Outbound API mailbox Events of RoutingFailed                 |

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

| Field          | Type                                                                                                     | Character Limit                      | Description                                         |
| :------------- | :------------------------------------------------------------------------------------------------------- | :----------------------------------- | :-------------------------------------------------- |
| eventId        | String                                                                                                   | 4 bytes (32-bit signed int)          | Unique Event Identifier for the Fill Request.       |
| eventDateUtc   | DateTime                                                                                                 | YYYY-MM-DD T HH:MM:SS.microseconds Z | Date and time of the event in UTC (ISO 8601).       |
| eventType      | String                                                                                                   | 50                                   | Event type description.                             |
| status         | String                                                                                                   | 20                                   | Current status of the event.                        |
| statusMessage  | String                                                                                                   | max                                  | Descriptive message explaining the status.          |
| FillRequestKey | String                                                                                                   | 50                                   | Unique ID associated with fill request.             |
| detail         | [Submitted detail](https://docs.healthdyne.com/v2.181/docs/mailbox-data-object-schemas#submitted-detail) |                                      | Contains details of fill request that was verified. |

### Submitted detail

| Field       | Type   | Character Limit | Description                                                                 |
| :---------- | :----- | :-------------- | :-------------------------------------------------------------------------- |
| orderNumber | String | 50              | Order number used to track this order.                                      |
| scriptKey   | String | Max             | Can have multiple comma (,) separated unique ID associated with script key. |
| fillNumber  | String | 50              | Fill number that was dispensed.                                             |

<br />

### RxVerified

| Field          | Type                                                                                                | Character Limit                      | Description                                         |
| :------------- | :-------------------------------------------------------------------------------------------------- | :----------------------------------- | :-------------------------------------------------- |
| eventId        | String                                                                                              | 4 bytes (32-bit signed int)          | Unique Event Identifier for the Fill Request.       |
| eventDateUtc   | DateTime                                                                                            | YYYY-MM-DD T HH:MM:SS.microseconds Z | Date and time of the event in UTC (ISO 8601).       |
| eventType      | String                                                                                              | 50                                   | Event type description.                             |
| status         | String                                                                                              | 20                                   | Current status of the event.                        |
| statusMessage  | String                                                                                              | max                                  | Descriptive message explaining the status.          |
| FillRequestKey | String                                                                                              | 50                                   | Unique ID associated with fill request.             |
| detail         | [RxVerified detail](https://docs.healthdyne.com/docs/mailbox-data-object-schemas#rxverified-detail) |                                      | Contains details of fill request that was verified. |

<br />

### RxVerified detail

| Field        | Type                                                                                       | Character Limit | Description                            |
| :----------- | :----------------------------------------------------------------------------------------- | :-------------- | :------------------------------------- |
| orderNumber  | String                                                                                     | 50              | Order number used to track this order. |
| scriptKey    | String                                                                                     | 50              | Unique ID associated with script key.  |
| fillNumber   | String                                                                                     | 50              | Fill number that was dispensed.        |
| dispenseDrug | [dispenseDrug](https://docs.healthdyne.com/docs/mailbox-data-object-schemas#dispense-drug) |                 | Dispensed drug object.                 |

<br />

### Dispense Drug

| Field            | Type   | Character Limit | Description                      |
| :--------------- | :----- | :-------------- | :------------------------------- |
| dispenseNDC      | String | 50              | NDC of drug that was dispensed.  |
| dispenseDrugName | String | 50              | Drug name that was dispensed.    |
| daysSupply       | String | 50              | Days the supply will last for.   |
| dispenseQuantity | String | 50              | Dispensed quantity               |
| labelDirections  | String | 50              | Drug usage label direction text. |
| dosageForm       | String | 50              | Drug dosage form.                |
| drugStrength     | String | 50              | Shows strength of the drug.      |
| drugStrengthUOM  | String | 50              | Drug strength unit of measure.   |

### RxShipped

| Field          | Type                                                                                              | Character Limit                      | Description                                   |
| :------------- | :------------------------------------------------------------------------------------------------ | :----------------------------------- | :-------------------------------------------- |
| eventId        | String                                                                                            | 4 bytes (32-bit signed int)          | Unique Event Identifier for the Fill Request. |
| eventDateUtc   | DateTime                                                                                          | YYYY-MM-DD T HH:MM:SS.microseconds Z | Date and time of the event in UTC (ISO 8601). |
| eventType      | String                                                                                            | 50                                   | Event type description.                       |
| status         | String                                                                                            | 20                                   | Current status of the event.                  |
| statusMessage  | String                                                                                            | max                                  | Descriptive message explaining the status.    |
| FillRequestKey | String                                                                                            | 50                                   | Unique ID associated with fill request.       |
| trackingNumber | String                                                                                            | 40                                   | Shipment tracking number.                     |
| detail         | [RxShipped detail](https://docs.healthdyne.com/docs/mailbox-data-object-schemas#RxShipped-detail) |                                      | Shipments info object.                        |

### RxShipped detail

| Field       | Type                                                                                | Character Limit | Description                            |
| :---------- | :---------------------------------------------------------------------------------- | :-------------- | :------------------------------------- |
| orderNumber | String                                                                              | 50              | Order number used to track this order. |
| scriptKey   | String                                                                              | 50              | Unique ID associated with script key.  |
| shipments   | [shipments](https://docs.healthdyne.com/docs/mailbox-data-object-schemas#shipments) |                 | Shipments info object.                 |

### shipments

| Field          | Type   | Character Limit         | Description                                                                        |
| :------------- | :----- | :---------------------- | :--------------------------------------------------------------------------------- |
| address        | object |                         | Contains shipment address information (note that currently it will always be null) |
| trackingNumber | String | 50                      | Order tracking number.                                                             |
| shipmentCode   | String | 50                      | Shipment code used to ship the order.                                              |
| trackingUrl    | String | 50                      | URL to track the order shipment status.                                            |
| weight         | String | 50                      | Package weight.                                                                    |
| dispensedQty   | String | 50                      | Dispensed quantity in shipped order.                                               |
| daysSupply     | String | 50                      | Day supply in the order.                                                           |
| shipmentDate   | String | YYYY-MM-DD T HH:MM:SS Z | Date order was shipped.                                                            |

### RxIssue

| Field          | Type                                                                                          | Character Limit                      | Description                                   |
| :------------- | :-------------------------------------------------------------------------------------------- | :----------------------------------- | :-------------------------------------------- |
| eventId        | String                                                                                        | 4 bytes (32-bit signed int)          | Unique Event Identifier for the Fill Request. |
| eventDateUtc   | DateTime                                                                                      | YYYY-MM-DD T HH:MM:SS.microseconds Z | Date and time of the event in UTC (ISO 8601). |
| eventType      | String                                                                                        | 50                                   | Event type description.                       |
| status         | String                                                                                        | 20                                   | Current status of the event.                  |
| statusMessage  | String                                                                                        | max                                  | Descriptive message explaining the status.    |
| FillRequestKey | String                                                                                        | 50                                   | Unique ID associated with fill request.       |
| detail         | [RxIssue detail](https://docs.healthdyne.com/docs/mailbox-data-object-schemas#RxIssue-detail) |                                      | Shipments info object.                        |

### RxIssue detail

| Field        | Type   | Character Limit | Description                                          |
| :----------- | :----- | :-------------- | :--------------------------------------------------- |
| orderNumber  | String | 50              | Order number used to track this order.               |
| scriptKey    | String | 50              | Unique ID associated with script key.                |
| fillNumber   | Int    | 2               | Shows how many fills have been fulfilled for this Rx |
| issueMessage | String | 50              | Descriptive message explaining the issue.            |

### RxCanceled

| Field          | Type                                                                                                | Character Limit                      | Description                                   |
| :------------- | :-------------------------------------------------------------------------------------------------- | :----------------------------------- | :-------------------------------------------- |
| eventId        | String                                                                                              | 4 bytes (32-bit signed int)          | Unique Event Identifier for the Fill Request. |
| eventDateUtc   | DateTime                                                                                            | YYYY-MM-DD T HH:MM:SS.microseconds Z | Date and time of the event in UTC (ISO 8601). |
| eventType      | String                                                                                              | 50                                   | Event type description.                       |
| status         | String                                                                                              | 20                                   | Current status of the event.                  |
| statusMessage  | String                                                                                              | max                                  | Descriptive message explaining the status.    |
| FillRequestKey | String                                                                                              | 50                                   | Unique ID associated with fill request.       |
| detail         | [RxCanceled detail](https://docs.healthdyne.com/docs/mailbox-data-object-schemas#RxCanceled-detail) |                                      | Shipments info object.                        |

### RxCanceled detail

| Field                   | Type   | Character Limit | Description                                                              |
| :---------------------- | :----- | :-------------- | :----------------------------------------------------------------------- |
| orderNumber             | String | 50              | Order number used to track this order.                                   |
| scriptKey               | String | 50              | Unique ID associated with script key.                                    |
| fillNumber              | Int    | 2               | Shows how many fills have been fulfilled for this Rx                     |
| orderCanceledReasonCode | String | 2               | Code reason why the order was canceled                                   |
| orderCanceledReasonDesc | String | max             | Code reason description to explain the reason why the order was canceled |

### Received Event

| Field         | Type                                                                                            | Character Limit | Description                                                                              |
| :------------ | :---------------------------------------------------------------------------------------------- | :-------------- | :--------------------------------------------------------------------------------------- |
| eventId       | String                                                                                          | max             | Unique event identifier in HealthDyne system.                                            |
| eventDateUtc  | String                                                                                          | 27              | UTC timestamp of when the event occurred.                                                |
| eventType     | String                                                                                          | 50              | Type of event, e.g., "RXTRANSFER".                                                       |
| status        | String                                                                                          | 20              | Current status of the event.                                                             |
| statusMessage | String                                                                                          | max             | Descriptive message explaining the status.                                               |
| scriptKey     | String                                                                                          | 50              | Unique identifier for the script being transferred which is initially defined by client. |
| patientKey    | String                                                                                          | 50              | Unique identifier for the patient.                                                       |
| detail        | [Received Detail](https://docs.healthdyne.com/docs/mailbox-data-object-schemas#Received-detail) |                 | Nested object containing extra details specific to the event type                        |

#### Received Detail

| Field  | Type   | Character Limit | Description                  |
| :----- | :----- | :-------------- | :--------------------------- |
| reason | String | 255             | Reason for the status if any |

<br />

### Clarified Event

| Field         | Type                                                                                            | Character Limit | Description                                                                              |
| :------------ | :---------------------------------------------------------------------------------------------- | :-------------- | :--------------------------------------------------------------------------------------- |
| eventId       | String                                                                                          | max             | Unique event identifier in HealthDyne system.                                            |
| eventDateUtc  | String                                                                                          | 27              | UTC timestamp of when the event occurred.                                                |
| eventType     | String                                                                                          | 50              | Type of event, e.g., "RXSTATUS".                                                         |
| status        | String                                                                                          | 20              | Current status of the event.                                                             |
| statusMessage | String                                                                                          | max             | Descriptive message explaining the status.                                               |
| scriptKey     | String                                                                                          | 50              | Unique identifier for the script being transferred which is initially defined by client. |
| patientKey    | String                                                                                          | 50              | Unique identifier for the patient.                                                       |
| detail        | [Received Detail](https://docs.healthdyne.com/docs/mailbox-data-object-schemas#Received-detail) |                 | Nested object containing extra details specific to the event type                        |

#### Clarified Detail

| Field  | Type   | Character Limit | Description                  |
| :----- | :----- | :-------------- | :--------------------------- |
| reason | String | 255             | Reason for the status if any |