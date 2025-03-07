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

<HTMLBlock>{`
<table style="width: 100%; border-collapse: collapse;">
<thead>
<tr>
  <th style="border: 1px solid #ddd; padding: 8px;">Field</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Type</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Character Limit</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Required/Optional</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Description</th>
</tr>
</thead>
<tbody>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Batch ID</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Required</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Unique Batch ID of the responses</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Count</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Integer</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>3</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Required</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>The number of Status Results</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Approximate Remaining<br>Statuses</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Integer</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>9</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Required</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>The approximate number of remaining statuses</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Results</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Required</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>statuses</p>
</td>
</tr>
</tbody>
</table>
`}</HTMLBlock>

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

<HTMLBlock>{`
<table style="width: 100%; border-collapse: collapse;">
<thead>
<tr>
  <th style="border: 1px solid #ddd; padding: 8px;">Type</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Description</th>
</tr>
</thead>
<tbody>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Acknowledged</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Request has been received</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Rejected</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Prescription was not received for the order<br>The requested drug did not match the prescription<br>No inventory exists to fulfill the order  </p>
<p>See <a href="doc:top-reject-reasons">Top Reject Reasons</a></p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Rx Verified</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Prescription has been verified by the pharmacy</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Canceled</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Request received for order to be canceled</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Dispensed</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Order has been shipped</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Refill Reminder</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Reminder for submitting refill request</p>
</td>
</tr>
</tbody>
</table>
`}</HTMLBlock>

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