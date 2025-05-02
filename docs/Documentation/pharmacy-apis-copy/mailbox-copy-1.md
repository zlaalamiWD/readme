---
title: Mailbox
deprecated: false
hidden: true
metadata:
  robots: index
---
# RxFill Status Request

View the [MailBox](ref:post_v2-mailbox) API Reference for detailed request body information.

This endpoint should be used to obtain the status of Rxfill requests previously submitted. No request body is required.\
HealthDyne employs a mailbox style order status reporting methodology. Therefore, when an order has a status update, the status message is delivered to the partner’s mailbox. This status message remains in the mailbox until the status message is retrieved by the partner and receipt of the message is acknowledged.
A maximum of 100 status messages will be returned with a single request. Multiple requests may be necessary to receive all outstanding status messages. Please refer to the Status Codes returned to determine if all messages have been retrieved. Retrieving messages is a two‐step process.

1. Retrieve a batch of messages.
2. Acknowledge the batch using the batchId returned from #1 using a POST method.

Note: Status messages are not considered delivered or removed from the mailbox until an acknowledgment is sent using a POST request with the batchId as a query parameter.\
Until this acknowledgment is received, subsequent status fetch requests will return the same events with the same batchId. To avoid duplicate status data, do not submit another status request until the previous response has been acknowledged.

### Server

##### Only https connections are accepted.

| REQUEST TYPE | ENDPOINT                              |
| :----------- | :------------------------------------ |
| GET  (Test)  | partner.uat-healthdyne.com/v2/mailbox |
| GET  (Prod)  | partner.healthdyne.com/v2/mailbox     |

### Header

| Key                         | Value                  |
| :-------------------------- | :--------------------- |
| Accept                      | application/json       |
| HealthDyne-Subscription-Key | Provided by HealthDyne |

# GET Request

#### Sample GET Request

> `<   https://>`

This tells the API to only respond with 10 messages. The default message count is 100 messages. The Mailbox only allows 100 messages to be pulled at a time.

# GET Status Response

The below table lists the potential response codes that can be received in response to a GET request.

| Code | Description                            |
| :--- | :------------------------------------- |
| 200  | Status message(s) returned in response |
| 204  | No messages in queue                   |
| 400  | Bad Request                            |
| 500  | Internal Server Error                  |

#### Sample Status Response

```json
{
    
            }
        }
    ]
}
```

# Acknowledge Batch (POST Method)

The POST method acknowledges the batchID of messages from the queue.

##### Only https connections are accepted.

| REQUEST TYPE   | ENDPOINT                                                   |
| :------------- | :--------------------------------------------------------- |
| DELETE  (Test) | partner.uat-healthdyne.com/v2/mailbox/\{Batch id}/markread |
| DELETE(Prod)   | partner.healthdyne.com/v2/mailbox/\{Batch id}/markread     |

### Header

| Key                         | Value                  |
| :-------------------------- | :--------------------- |
| HealthDyne-Subscription-Key | Provided by HealthDyne |

# # POST Request

#### Sample POST Request

> `<https://partner.uat-healthdyne.com/v2/mailbox/\{Batch id}/markread>`

# Status Event Types:

# # Fill Request Status Events

## Submitted

HealthDyne will create the order after receiving a RxFill. Once the order has been successfully created, HealthDyne will generate a submitted order status message and queues the event up for the client to retrieve it.

#### sample "Submitted" event

```json
{
            "eventId": "5948314D-1152-4475-A29C-4B56FAF77437",
            "eventDateUtc": "2025-04-23T14:22:05.3118884",
            "eventType": "FILLREQUEST",
            "status": "Submitted",
            "statusMessage": null,
            "eventDetail": {
                "OrderId": "FR12004497",
                "OrderNumber": "23APR075202390"
            }
        }
```

## Rejected

If order creation errors/rejects; then Rejected event will be created. Possible reasons for system to reject order request include duplicate order number or Invalid NDC used.

#### Sample "Rejected" event

```json
{
            "eventId": "5948314D-1152-4475-A29C-4B56FAF77437",
            "eventDateUtc": "2025-04-23T14:22:05.3118884",
            "eventType": "FILLREQUEST",
            "status": "REJECTED",
            "statusMessage": "The order has been rejected",
            "eventDetail": {
				"OrderNumber": "84438058",
				"rejectReason": "Validation Failed: Invalid NDC: 12121212121"
			}	
}
```

## Canceled

When an order has been canceled by pharmacy, HealthDyne will send an update notifying of the canceled status along with reason for cancelation.

#### Sample "Canceled" event

```json
{
  
  
}
```

## Dispensed

Once the order has been shipped successfully by pharmacy, then send update will be sent to client.

#### Sample "Dispensed" event

```json
{
            "eventId": "5948314D-1152-4475-A29C-4B56FAF77437",
            "eventDateUtc": "2025-04-23T14:22:05.3118884",
            "eventType": "FILLREQUEST",
            "status": "DISPENSED",
            "statusMessage": "The order has been shipped",
            "eventDetail": {
				"OrderNumber": "84438058",
				"Packages": [
					{
						"ShipmentCode": "UPS GR",
						"TrackingNumber": "1Z765WF80339910758",
						"Weight": 4.9,
						"ShippingCost": 31.34,
						"ShipDateUtc": "2025-03-21T23:09:26.811Z",
						"ShippingAddress": {
							"Address1": "HOSPITAL MENONITA CAYEY ROAD #14",
							"Address2": "KM 72.2 RINCON WARD SECTOR LAS LOMAS",
							"City": "CAYEY",
							"State": "PR",
							"Zip": "00736"
						}
					}
				],
				"FulfillingPharmacy": "HEALTHDYNE-FL"
			}	
}
```

##