---
title: Check Status Events
description: |-
  Example of retrieving and acknowledging status events using the Mailbox API.
  1. Retrieve Messages
  2. Acknowledge Receipt
hidden: false
recipe:
  color: '#018FF4'
  icon: ''
---
```java Java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
  .url("https://api.uat-healthdyne.com/v2/mailbox")
  .get()
  .addHeader("accept", "application/json")
  .addHeader("HealthDyne-Subscription-Key", "abcdefghijklmnop")
  .build();

Response response = client.newCall(request).execute();




OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
  .url("https://api.uat-healthdyne.com/v2/mailbox?batchId=1000018")
  .post(null)
  .addHeader("accept", "application/json")
  .addHeader("HealthDyne-Subscription-Key", "abcdefghijklmnop")
  .build();

Response response = client.newCall(request).execute();
```

```python Python
import requests

url = "https://api.uat-healthdyne.com/v2/mailbox"

headers = {
    "accept": "application/json",
    "HealthDyne-Subscription-Key": "abcdefghijklmnop"
}

response = requests.get(url, headers=headers)

print(response.text)




import requests

url = "https://api.uat-healthdyne.com/v2/mailbox?batchId=1000018"

headers = {
    "accept": "application/json",
    "HealthDyne-Subscription-Key": "abcdefghijklmnop"
}

response = requests.post(url, headers=headers)

print(response.text)
```

```csharp C#
var client = new RestClient("https://api.uat-healthdyne.com/v2/mailbox");
var request = new RestRequest(Method.GET);
request.AddHeader("accept", "application/json");
request.AddHeader("HealthDyne-Subscription-Key", "abcdefghijklmnop");
IRestResponse response = client.Execute(request);




var client = new RestClient("https://api.uat-healthdyne.com/v2/mailbox?batchId=1000018");
var request = new RestRequest(Method.POST);
request.AddHeader("accept", "application/json");
request.AddHeader("HealthDyne-Subscription-Key", "abcdefghijklmnop");
IRestResponse response = client.Execute(request);
```

```javascript JavaScript
const options = {method: 'GET', headers: {accept: 'application/json'}};

fetch('https://api.uat-healthdyne.com/v2/mailbox', options)
  .then(response => response.json())
  .then(response => console.log(response))
  .catch(err => console.error(err));




const options = {
  method: 'POST',
  headers: {accept: 'application/json', 'HealthDyne-Subscription-Key': 'abcdefghijklmnop'}
};

fetch('https://api.uat-healthdyne.com/v2/mailbox?batchId=1000018', options)
  .then(response => response.json())
  .then(response => console.log(response))
  .catch(err => console.error(err));
```

```json Response Example
//GET Response
{
  "batchId": "1000018",
  "count": 2,
  "approximateRemainingCount": 0,
  "messageList": [
    {
      "messageId": "4e1ae5b3-3eed-4ed0-b709-67a9391cc866",
      "eventId": "1000003",
      "eventDateUtc": "2023-05-08T23:12:15.5421068Z",
      "eventType": "RXTRANSFER",
      "scriptKey": "1000001",
      "status": "Transferred",
      "statusMessage": "The Rx has been transferred successfully",
      "detail": {
        "patientKey": "1000002",
        "rxNumber": "RX12345"
      }
    },
    {
      "messageId": "582453ac-3844-4519-8fec-93c557ca12cb",
      "eventId": "1000005",
      "eventDateUtc": "2023-05-08T23:13:15.5421068Z",
      "eventType": "RXTRANSFER",
      "scriptKey": "1000004",
      "status": "Rejected",
      "statusMessage": "The file [http://somedomain.com/files/12548.png] could not be retrieved.",
      "detail": {
        "patientKey": "1000002",
        "rxNumber": null
      }
    }
  ]
}


//POST Response
{
    "batchId": "1000018",
    "status": "The messages were marked read.",
    "messageId": [
        "4e1ae5b3-3eed-4ed0-b709-67a9391cc866",
        "582453ac-3844-4519-8fec-93c557ca12cb"
    ]
}
```

# Retrieve Messages

<!-- java@1-10 -->
<!-- python@1-12 -->
<!-- csharp@1-5 -->
<!-- javascript@1-6 -->

HealthDyne's MailBox API utilizes a delivery method similar to the post office mailbox. Events such as status updates will be posted to the mailbox where clients can retrieve the events for ingestion into their internal systems. By default 25 messages will be returned when the MailBox API is called using the GET method. If you would like to retrieve more or less events per call you can specify the query parameter "messageCount" in order to adjust the number of events returned i.e. <https://api.uat-healthdyne.com/v2/mailbox?messageCount=15>. A maximum of 100 events can be returned in a single call. See the successful GET response in the window below.

# Acknowledge Receipt

<!-- java@15-24 -->
<!-- python@17-28 -->
<!-- csharp@10-14 -->
<!-- javascript@11-19 -->

In order to retrieve the next batch of events you must first acknowledge receipt of the current batch of events by POSTin back to the MailBox API with the batchId as a query parameter i.e. <https://api.uat-healthdyne.com/v2/mailbox?batchId=1000018>. See the successful POST response in the window below.