---
title: Status Message Fields
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
# Order Status

[block:parameters]
{
  "data": {
    "h-0": "Field",
    "h-1": "Type",
    "h-2": "Character Limit",
    "h-3": "Required/Optional",
    "h-4": "Description",
    "0-0": "Batch ID",
    "0-1": "String",
    "0-2": "",
    "0-3": "Required",
    "0-4": "Unique Batch ID of the responses",
    "1-0": "Count",
    "1-1": "Integer",
    "1-2": "3",
    "1-3": "Required",
    "1-4": "The number of Status Results",
    "2-0": "Approximate Remaining  \nStatuses",
    "2-1": "Integer",
    "2-2": "9",
    "2-3": "Required",
    "2-4": "The approximate number of remaining statuses",
    "3-0": "Results",
    "3-1": "String",
    "3-2": "",
    "3-3": "Required",
    "3-4": "statuses"
  },
  "cols": 5,
  "rows": 4,
  "align": [
    "left",
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]

# Status Result

| Field        | Type   | Character Limit | Required/Optional | Description                                                            |
| :----------- | :----- | :-------------- | :---------------- | :--------------------------------------------------------------------- |
| Status       | String |                 | Required          | Status of the Prescription                                             |
| Prescription | String |                 | Required          | Prescription for the Status                                            |
| Patient      | String |                 | Required          | Patient for the Prescription                                           |
| Shipping     | String |                 | Optional          | The shipping information for the prescription if the status is Shipped |

# Status

| Field  | Type   | Character Limit | Required/Optional | Description                                                                                             |
| :----- | :----- | :-------------- | :---------------- | :------------------------------------------------------------------------------------------------------ |
| Type   | String | 50              | Required          | Acknowledged \| Canceled \| Rejected \| Dispensed \| RxVerified \| Pending Inventory \| Refill Reminder |
| Reason | String | 255             | Required          | Reason for Statuses                                                                                     |

# Status Reasons

[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Description",
    "0-0": "Acknowledged",
    "0-1": "Request has been received",
    "1-0": "Rejected",
    "1-1": "Prescription was not received for the order  \nThe requested drug did not match the prescription  \nNo inventory exists to fulfill the order  \n  \nSee [Top Reject Reasons](doc:top-reject-reasons)",
    "2-0": "Rx Verified",
    "2-1": "Prescription has been verified by the pharmacy",
    "3-0": "Canceled",
    "3-1": "Request received for order to be canceled",
    "4-0": "Dispensed",
    "4-1": "Order has been shipped",
    "5-0": "Refill Reminder",
    "5-1": "Reminder for submitting refill request"
  },
  "cols": 2,
  "rows": 6,
  "align": [
    "left",
    "left"
  ]
}
[/block]

# Prescription

| Field               | Type    | Character Limit | Required/Optional | Description                                                                  |
| :------------------ | :------ | :-------------- | :---------------- | :--------------------------------------------------------------------------- |
| Rx Number           | String  | 20              | Required          | RX number for the Prescription required if it is a refill or a status update |
| Drug Name           | String  | 60              | Required          | Name of the Medication                                                       |
| NDC                 | Integer | 9               | Required          | NDC for the Prescription                                                     |
| Refills Prescribed  | String  | 3               | Required          | Number of Refills Prescribed                                                 |
| Refills Remaining   | String  | 3               | Required          | Number of Refills Remaining                                                  |
| Refills Dispensed   | String  | 3               | Required          | Number of Refills Dispensed                                                  |
| Instruction         | String  | 147             | Required          | Instructions on Prescription storage and consumption.                        |
| Day Supply          | String  | 3               | Required          | Dispensed quantity divided by the number of Rx consumed in a day.            |
| Prescribed Quantity | String  | 3               | Required          | Quantity of Dispensed product.                                               |

# Patient

| Field     | Type   | Character Limit | Required/Optional | Description                                                                    |
| :-------- | :----- | :-------------- | :---------------- | :----------------------------------------------------------------------------- |
| Member ID | String | 18              | Optional          | Unique Patient Identifier that identifies patient of which an Rx is prescribed |
| Group ID  | String | 16              | Optional          | Contains Group Information                                                     |

# Shipping

| Field              | Type      | Character Limit | Required/Optional | Description                                                                    |
| :----------------- | :-------- | :-------------- | :---------------- | :----------------------------------------------------------------------------- |
| Shipping Code      | String    | 10              | Optional          | See [Shipping Methods Table](doc:status-message-fields#shipping-methods) below |
| Signature Required | Boolean   | 1               | Optional          | Does the package require a signature                                           |
| Saturday Delivery  | Boolean   | 1               | Optional          | Does the Patient want the package to be delivered on Saturday                  |
| Address            | Address   |                 | Optional          | Shipping Address                                                               |
| Tracking Number    | String    | 50              | Optional          | The tracking number of the package                                             |
| Shipping Cost      | Decimal   | 9,2             | Optional          | The cost for shipping the package                                              |
| Shipment Date      | Date Time |                 | Optional          | The date the package was shipped                                               |

# Shipping Methods

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
| UPS 3 DS | UPS 3 Day Select                          | Saturday delivery |
| UPS USG  | UPS-USPS Sure Post                        | Saturday delivery |

# Address

| Field | Type   | Character Limit | Required/Optional | Description                |
| :---- | :----- | :-------------- | :---------------- | :------------------------- |
| Line1 | String | 60              | Required          | Street Address             |
| Line2 | String | 60              | Optional          | Street Address             |
| Line3 | String | 40              | Optional          | Street Address             |
| City  | String | 50              | Required          | City                       |
| State | String | 2               | Required          | US State Abbreviation Code |
| Zip   | String | 5,9             | Required          | Format NNNNN, NNNNNNNNN    |