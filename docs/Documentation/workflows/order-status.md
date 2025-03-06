---
title: Order Status
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
# Status Request

View the [Order Status](ref:get_v1-prescriptionrequest-orderstatus) API Reference for detailed request body information.

This endpoint should be used to obtain the status of ALL prescription and/or refill requests previously submitted which had an unretrieved status update. No request body is required.\
HealthDyne employs a mailbox style order status reporting methodology. Therefore, when an order has a status update, the status message is delivered to the partner’s mailbox. This status message remains in the mailbox until the status message is retrieved by the partner and receipt of the message is acknowledged.\
A maximum of 25 status messages will be returned with a single request. Multiple requests may be necessary to receive all outstanding status messages. Please refer to the Status Codes returned to determine if all messages have been retrieved.\
Note, the status messages are not considered delivered and removed from the mailbox until the receipt of the message is acknowledged using the StatusReceived endpoint. Hence, another status request should not be submitted until the previous status response is acknowledged.\
The description below provides a management overview of the request message which only contains a header. Detailed descriptions of the entities contained within the request can be found in the Appendix section of this document as well as the API Reference.

The Order Status API will create the following order status messages to support the standard workflow:

1. Acknowledged – sent at Prescription API event
2. Rejected – sent based off event from Rx receipt journey including rejection reasons
3. Canceled – sent when a Client or Pharmacy is requested
4. Shipped – sent at prescription level when an order is shipped
5. Refill Reminder – sent at 85% utilization with number of refills remaining
6. RefillAcknowledged- sent at Refill API event

Order Status messages will be configurable so the Client can send an Order Status request and HealthDyne can send an Order Status message to Clients.

### Server

| Request Type | Endpoint                                                                                                                                                  | Query String                   |
| :----------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------- |
| Get (Test)   | [https://partner.UAT-WellDyne.com/v1/prescriptionrequest/orderstatus/limit\*](https://partner.UAT-WellDyne.com/v1/prescriptionrequest/orderstatus/limit*) | \*Optional. Default 5. Max 25. |
| Get (Test)   | [https://partner.UAT-WellDyne.com/v1/prescriptionrequest/orderstatus/limit\*](https://partner.UAT-WellDyne.com/v1/prescriptionrequest/orderstatus/limit*) | \*Optional. Default 5. Max 25. |

### Header

| Key                         | Value                  |
| :-------------------------- | :--------------------- |
| Accept                      | application/json       |
| Content-Type                | application/json       |
| HealthDyne-Subscription-Key | Provided by HealthDyne |

# Status Response

The description below provides a management overview of the response message returned after transmission of a refill request message. Detailed descriptions of the entities contained within the response can be found in the Appendix section of this document as well as the API Reference.

| Code | Description                                                               |
| :--- | :------------------------------------------------------------------------ |
| 200  | All messages delivered                                                    |
| 204  | No messages                                                               |
| 206  | Max 25 messages delivered - submit another request for remaining messages |
| 400  | Bad Request – typically header is missing key                             |
| 401  | Unauthorized                                                              |
| 500  | Internal Server Error                                                     |

### Body

| Key          | Description                                         |
| :----------- | :-------------------------------------------------- |
| RequestId    | HealthDyne Guide used to uniquely identify message  |
| MessageCount | Number of messages contained within the MessageList |
| MessagesList | Array of status messages                            |

#### Sample Status Response

```json
{
  "BatchID": "9dd52b79-0fec-4434-90f3-e5623d0d596e",
  "count": 3,
  "approximateRemainingStatuses": 3,
  "results": [
    {
      "Status": {
        "StatusType": "Acknowledged",
        "Reason": "Acknowledged"
      },
      "Prescription": {
		  "RX": 12345,
		  "NDC": "687947329",
		  "NDCName": "Drug Name",
		  "RefillsPrescribed": 10,
		  "RefillsDispensed": 0,
		  "RefillsRemaining": 10
	  },
      "Patient": {
        "MemberID": "HC768654981",
        "GroupID": "7653732",
        "FirstName": "John",
		"LastName": "Doe",
        "DateOfBirth": "01/01/1970",
		"Address" : {
			"AddressType": "HOME",
			"Address1": "123 Main Street",
			"City": "Tampa",
			"State": "FL",
			"Zip": 33763
		}
		"Contact": {
			"ContactType": "Phone",
			"ContactAddress": "8138889999"
		},
		"Allergies": [
			{"Allergy": "NSAIDS"},
			{"Allergy": "PENICILLINS"}
		]
		"ExternalMedications": NULL	
	  },
	  "Shipping": NULL
	},
    {
      "Status": {
        "StatusType": "Rejected",
        "Reason": "Physician did not authorize the medication"
      },
      "Prescription": {
		  "RX": NULL,
		  "NDC": "687947329",
		  "NDCName": "Drug Name",
		  "RefillsPrescribed": 0,
		  "RefillsDispensed": 0,
		  "RefillsRemaining": 0
	  },
      "Patient": {
        "MemberID": "HC768654981",
        "GroupID": "7653732",
        "FirstName": "John",
		"LastName": "Doe",
        "DateOfBirth": "01/01/1970",
		"Address" : {
			"AddressType": "HOME",
			"Address1": "123 Main Street",
			"City": "Tampa",
			"State": "FL",
			"Zip": 33763
		}
		"Contact": {
			"ContactType": "Phone",
			"ContactAddress": "8138889999"
		},
		"Allergies": [
			{"Allergy": "NO KNOWN DRUG ALLERGY"}
		]
		"ExternalMedications": NULL	
	  },
	  "Shipping": NULL
	},
	    {
      "Status": {
        "StatusType": "Shipped",
        "Reason": "Shipped"
      },
      "Prescription": {
		  "RX": 3265814,
		  "NDC": "687947329",
		  "NDCName": "Drug Name",
		  "RefillsPrescribed": 0,
		  "RefillsDispensed": 0,
		  "RefillsRemaining": 0
	  },
      "Patient": {
        "MemberID": "HC768654981",
        "GroupID": "7653732",
        "FirstName": "John",
		"LastName": "Doe",
        "DateOfBirth": "01/01/1970",
		"Address" : {
			"AddressType": "HOME",
			"Address1": "123 Main Street",
			"City": "Tampa",
			"State": "FL",
			"Zip": 33763
		}
		"Contact": {
			"ContactType": "Phone",
			"ContactAddress": "8138889999"
		},
		"Allergies": [
			{"Allergy": "NO KNOWN DRUG ALLERGY"}
		]
		"ExternalMedications": NULL	
	  },
	  "Shipping": {
  		"Address" : {
			"AddressType": "HOME",
			"Address1": "123 Main Street",
			"City": "Tampa",
			"State": "FL",
			"Zip": 33763
		},
		"ShipmentCode": "UPS GR",
		"SaturdayDelivery": "FALSE",
		"SignatureRequired": "FALSE",
		"TRACKINGNUMBER": "1Z765WF81303299692",
		"ShippingCost": 5.50,
		"ShipmentWeight": 1.25,
		"DateShipped": 2022-02-23 23:27:18.227
	  }
	}

}
```

# Refill Reminder Status

#### Sample Refill Reminder Status

```json
{
    "batchId": "425906ed-30ea-4b03-9bd5-0b87b9b4ee04",
    "count": 1,
    "approximateRemainingCount": 0,
    "messageList": [
        {
            "requestId": "22DEC202207281415",
            "status": "Refill Reminder",
            "reason": "Refill Reminder",
            "shipment": null,
            "memberId": "AC000002890",
            "rxNumber": "10497561",
            "fillNumber": 1,
            "eventDate": "2022-12-22T17:31:52.256569+00:00"        }
    ]
}
```
