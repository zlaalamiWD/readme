---
title: Mailbox
deprecated: false
hidden: true
metadata:
  robots: index
---
# RxFill Status Request

View the [MailBox](ref:post_v2-mailbox) API Reference for detailed request body information.

Fill Request status messages are stored in a queue for each partner. Retrieving messages is a two‐step process.

1. Retrieve a batch of messages.
2. Delete the batch using the RequestId returned from #1. After retrieving the batch of status messages, the delete method must be called within 30 seconds, otherwise the messages in the batch will be placed back on the queue.

To deplete the queue, continue the steps above until a status code of 204 is returned. The queue should be checked at regularly scheduled intervals.

Note, the status messages are not considered delivered and removed from the mailbox until the receipt of the message is acknowledged by using a DELETE method with the batchId as a query parameter. Hence, another status request should not be submitted until the previous status response is acknowledged.

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

# Acknowled Batch (POST Method)

The POST method deletes the batch of messages from the queue. The delete must occur within 30 seconds of queue retrieval, otherwise messages will be placed back on the queue.

##### Only https connections are accepted.

| REQUEST TYPE   | ENDPOINT                                                     |
| :------------- | :----------------------------------------------------------- |
| DELETE  (Test) | partner.uat-healthdyne.com/v1/fillstatus/queue/\{request id} |
| DELETE(Prod)   | partner.healthdyne.com/v1/fillstatus/queue/\{request id}     |

### Header

| Key                         | Value                  |
| :-------------------------- | :--------------------- |
| HealthDyne-Subscription-Key | Provided by HealthDyne |

# # POST Request

#### Sample POST Request

> `<https://partner.uat-healthdyne.com/v2/mailbox?batchId=6be689c3-3306-4a75-b0d3-a769be788c99>`

#### Sample DELETE Response

```json
{ 
    
    ] 
}
```

# Status Event Types:

# # Fill Request Status Events

## Acknowledged

HealthDyne will create the order after receiving a RxFill. Once the order has been successfully created, HealthDyne will generate an Acknowledged’ order status message and queues the event up for the client to retrieve it.

#### sample "Submitted" event

```json
{
  
  }
}
```

## Rejected

If order creation errors/rejects; then Rejected event will be created. Possible reasons for system to reject order request include existing open orders for same order number or Invalid NDC used.

#### Sample "Rejected" event

```json
{
  
  
}
```

## Canceled

When an order has been canceled by pharmacy, HealthDyne will send an update notifying of the canceled status along with reason for cancelation.

#### Sample "Canceled" event

```json
{
  "
  
}
```

## Dispensed

Once the order has been shipped successfully by pharmacy, then send update will be sent to client.

#### Sample "Dispensed" event

```json
{

  
  }
}

```

##