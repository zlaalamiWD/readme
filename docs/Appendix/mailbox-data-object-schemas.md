---
title: Mailbox Data Object Schemas
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
| messageCount | int  | 3               | Required          | used to define how many messages should be returned per batch. Maximum will be 100 messages. if no value passed, the default is 100 messages per batch |

# RxTransfer event Type

\*\* RxTransfer Response Object\*\*

| Field         | Type                                                                                                                 | Character Limit | Description                                                                              |
| :------------ | :------------------------------------------------------------------------------------------------------------------- | :-------------- | :--------------------------------------------------------------------------------------- |
| eventId       | string                                                                                                               | max             | Unique event identifier in HealthDyne system.                                            |
| eventDateUtc  | string                                                                                                               | 27              | UTC timestamp of when the event occurred.                                                |
| eventType     | string                                                                                                               | 50              | Type of event, e.g., "RXTRANSFER".                                                       |
| status        | string                                                                                                               | 20              | Current status of the event.                                                             |
| statusMessage | string                                                                                                               | max             | Descriptive message explaining the status.                                               |
| scriptKey     | string                                                                                                               | 255             | Unique identifier for the script being transferred which is initially defined by client. |
| detail        | [RxTransferDetailObject](https://docs.healthdyne.com/v2.171/docs/mailbox-data-object-schemas#RxTransferDetailObject) |                 | Nested object containing extra details specific to the event type                        |

#### RxTransferDetailObject

| Field      | Type   | Character Limit | Description                        |
| :--------- | :----- | :-------------- | :--------------------------------- |
| patientKey | string | 255             | Unique identifier for the patient. |
| rxNumber   | string | 30              | Prescription number                |

# RxStatus event Type

\*\* RxStatus Response Object\*\*

| Field         | Type                                                                                                                 | Character Limit | Description                                                                              |
| :------------ | :------------------------------------------------------------------------------------------------------------------- | :-------------- | :--------------------------------------------------------------------------------------- |
| eventId       | string                                                                                                               | max             | Unique event identifier in HealthDyne system.                                            |
| eventDateUtc  | string                                                                                                               | 27              | UTC timestamp of when the event occurred.                                                |
| eventType     | string                                                                                                               | 50              | Type of event, e.g., "RXTRANSFER".                                                       |
| status        | string                                                                                                               | 20              | Current status of the event.                                                             |
| statusMessage | string                                                                                                               | max             | Descriptive message explaining the status.                                               |
| scriptKey     | string                                                                                                               | 255             | Unique identifier for the script being transferred which is initially defined by client. |
| patientKey    | string                                                                                                               | 255             | Unique identifier for the patient.                                                       |
| detail        | [RxTransferDetailObject](https://docs.healthdyne.com/v2.171/docs/mailbox-data-object-schemas#RxTransferDetailObject) |                 | Nested object containing extra details specific to the event type                        |

#### RxTransferDetailObject

| Field      | Type   | Character Limit | Description                        |
| :--------- | :----- | :-------------- | :--------------------------------- |
| patientKey | string | 20              | Unique identifier for the patient. |
| rxNumber   | string | 30              | Prescription number                |

# FillRequest event Type

\*\* FillRequest Response Object\*\*

| Field          | Type                                                                                                                   | Character Limit | Description                                                                   |
| :------------- | :--------------------------------------------------------------------------------------------------------------------- | :-------------- | :---------------------------------------------------------------------------- |
| eventId        | string                                                                                                                 | max             | Unique event identifier in HealthDyne system.                                 |
| eventDateUtc   | string                                                                                                                 | 27              | UTC timestamp of when the event occurred.                                     |
| eventType      | string                                                                                                                 | 50              | Type of event, e.g., "RXTRANSFER".                                            |
| status         | string                                                                                                                 | 20              | Current status of the event.                                                  |
| statusMessage  | string                                                                                                                 | max             | Descriptive message explaining the status.                                    |
| fillRequestKey | string                                                                                                                 | 255             | Unique identifier for the fill request  which is initially defined by client. |
| detail         | [FillRequestDetailObject](https://docs.healthdyne.com/v2.171/docs/mailbox-data-object-schemas#FillRequestDetailObject) |                 | Nested object containing extra details specific to the event type             |

#### FillRequestDetailObject

| Field            | Type                                                                                                           | Character Limit | Description                                                                              |
| :--------------- | :------------------------------------------------------------------------------------------------------------- | :-------------- | :--------------------------------------------------------------------------------------- |
| orderNumber      | string                                                                                                         | 100             | order number                                                                             |
| scriptKey        | string                                                                                                         | 255             | Unique identifier for the script being transferred which is initially defined by client. |
| fillNumber       | int                                                                                                            |                 | Shows how many fills have been fulfilled for this Rx                                     |
| remainingRefills | string                                                                                                         | 10              | Show how many fill remaing for the Rx                                                    |
| refillByDate     | string                                                                                                         |                 | Date recommended for refill                                                              |
| shipments        | \[[ShipmentObject](https://docs.healthdyne.com/v2.171/update/docs/mailbox-data-object-schemas#ShipmentObject)] |                 | shipment information                                                                     |

#### ShipmentObject

| Field          | Type                                                                                                          | Character Limit | Description                                        |
| :------------- | :------------------------------------------------------------------------------------------------------------ | :-------------- | :------------------------------------------------- |
| address        | \[[AddressObject](https://docs.healthdyne.com/v2.171/update/docs/mailbox-data-object-schemas#AddressObject) ] |                 | address information.                               |
| trackingNumber | string                                                                                                        | 50              | Package tracking number.                           |
| shipmentCode   | string                                                                                                        | 20              | Code representing the shipment type.               |
| trackingUrl    | string                                                                                                        | 10              | URL for tracking the shipment.                     |
| weight         | int                                                                                                           |                 | Weight of the shipment.                            |
| cost           | int                                                                                                           |                 | Shipping cost.                                     |
| dispensedQty   | string                                                                                                        | 20              | Quantity of medication dispensed.                  |
| daysSupply     | string                                                                                                        | 20              | Number of days the dispensed medication will last. |
| shipmentDate   | string                                                                                                        | 30              | The date the shipment was sent.                    |

#### AddresstObject

| Field    | Type   | Character Limit | Description            |
| :------- | :----- | :-------------- | :--------------------- |
| address1 | string | 255             | address 1 information. |
| address2 | string | 50              | address  information.  |
| city     | string | 40              | Shipped to city.       |
| state    | string | 2               | Shipped to state.      |
| zipcode  | string | 5               | Shipped to zip code.   |