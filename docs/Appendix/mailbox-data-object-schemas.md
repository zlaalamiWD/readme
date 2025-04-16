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

# RxTransfer event Type

#### Query Parameter

| Parameter    | Type | Character Limit | Required/Optional | Description                                                                                                                                            |
| :----------- | :--- | :-------------- | :---------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------- |
| messageCount | int  | 3               | Required          | used to define how many messages should be returned per batch. Maximum will be 100 messages. if no value passed, the default is 100 messages per batch |

**Response Object**

| Field         | Type                                                                                                                                                                 | Character Limit | Description                                                                             |
| :------------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------- | :-------------------------------------------------------------------------------------- |
| eventId       | string                                                                                                                                                               | max             | Unique event identifier in HealthDyne system.                                           |
| eventDateUtc  | string                                                                                                                                                               | 27              | UTC timestamp of when the event occurred.                                               |
| eventType     | string                                                                                                                                                               | 50              | Type of event, e.g., "RXTRANSFER".                                                      |
| status        | string                                                                                                                                                               | 20              | Current status of the event.                                                            |
| statusMessage | string                                                                                                                                                               | max             | Descriptive message explaining the status.                                              |
| scriptKey     | string                                                                                                                                                               | 255             | Unique identifier for the script being transferred which is initialy defined by client. |
| detail        | [https://docs.healthdyne.com/v2.171/docs/mailbox-data-object-schemas#detailObject](https://docs.healthdyne.com/v2.171/docs/mailbox-data-object-schemas#detailObject) |                 | Nested object containing extra details specific to the event type                       |

#### detailObject

| Field      | Type   | Character Limit | Required/Optional | Description                        |
| :--------- | :----- | :-------------- | :---------------- | :--------------------------------- |
| patientKey | string | 20              | Required          | Unique identifier for the patient. |
| rxNumber   | string | 30              | Required          | Prescription number                |