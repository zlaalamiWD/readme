---
title: eRx / Surescript Overview
description: >-
  This recipe shows a simple example for ordering fulfillment of a prescription
  in 3 easy steps:


  1. Create a Patient.

  2. eRx received via Surescripts

  3. Get prescription details

  4. Submit a Fill request.
hidden: true
recipe:
  color: '#018FF4'
  icon: ''
---
```java Java
OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/*+json");
RequestBody body = RequestBody.create(mediaType, "{\"patient\":{\"address\":{\"addressType\":\"HOME\",\"line1\":\"100 Rivers Edge Dr.\",\"city\":\"Temple Terrace\",\"state\":\"FL\",\"zipCode\":\"02155\",\"countryCode\":\"US\",\"defaultAddress\":true},\"contact\":{\"contactType\":\"Phone\",\"contactAddress\":\"5712345678\"},\"allergies\":[\"Amoxicillin\"],\"externalMedications\":[{\"ndc\":\"00045049660\",\"startDate\":\"2022-03-02\",\"endDate\":\"2022-04-02\"}],\"patientKey\":\"12389990\",\"firstName\":\"JANE\",\"lastName\":\"DOE\",\"birthDate\":\"1956-03-02\",\"gender\":\"F\"}}");
Request request = new Request.Builder()
  .url("https://api.uat-healthdyne.com/v2/patient")
  .post(body)
  .addHeader("HealthDyne-Subscription-Key", "abcdefghijklmnop")
  .addHeader("content-type", "application/*+json")
  .build();

Response response = client.newCall(request).execute();


OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
  .url("https://api.uat-healthdyne.com/v2/script")
  .get()
  .addHeader("accept", "application/json")
  .build();

Response response = client.newCall(request).execute();


OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/*+json");
RequestBody body = RequestBody.create(mediaType, "{\"scriptKeys\":[\"e156daa5-1905-42c5-9e2e-6e99ff082d95\"],\"shipping\":{\"address\":{\"line1\":\"500 Eagles Landin Dr\",\"city\":\"Lakeland\",\"state\":\"FL\",\"zipCode\":\"33810\",\"countryCode\":\"US\"},\"shippingCode\":\"UPS 1D\",\"saturdayDelivery\":true,\"signatureRequired\":true},\"fillRequestKey\":\"8a97815e-ef31-43ee-af87-662aaebaec32\"}");
Request request = new Request.Builder()
  .url("https://api.uat-healthdyne.com/v2/fill")
  .post(body)
  .addHeader("accept", "application/json")
  .addHeader("HealthDyne-Subscription-Key", "abcdefghijklmnop")
  .addHeader("content-type", "application/*+json")
  .build();

Response response = client.newCall(request).execute();
```

```python Python
import requests

url = "https://api.uat-healthdyne.com/v2/patient"

payload = "{\"patient\":{\"address\":{\"addressType\":\"HOME\",\"line1\":\"100 Rivers Edge Dr.\",\"city\":\"Temple Terrace\",\"state\":\"FL\",\"zipCode\":\"02155\",\"countryCode\":\"US\",\"defaultAddress\":true},\"contact\":{\"contactType\":\"Phone\",\"contactAddress\":\"5712345678\"},\"allergies\":[\"Amoxicillin\"],\"externalMedications\":[{\"ndc\":\"00045049660\",\"startDate\":\"2022-03-02\",\"endDate\":\"2022-04-02\"}],\"patientKey\":\"12389990\",\"firstName\":\"JANE\",\"lastName\":\"DOE\",\"birthDate\":\"1956-03-02\",\"gender\":\"F\"}}"
headers = {
    "HealthDyne-Subscription-Key": "abcdefghijklmnop",
    "content-type": "application/*+json"
}

response = requests.post(url, data=payload, headers=headers)

print(response.text)


import requests

url = "https://api.uat-healthdyne.com/v2/script"

headers = {"accept": "application/json"}

response = requests.get(url, headers=headers)

print(response.text)


import requests

url = "https://api.uat-healthdyne.com/v2/fill"

payload = "{\"scriptKeys\":[\"e156daa5-1905-42c5-9e2e-6e99ff082d95\"],\"shipping\":{\"address\":{\"line1\":\"500 Eagles Landin Dr\",\"city\":\"Lakeland\",\"state\":\"FL\",\"zipCode\":\"33810\",\"countryCode\":\"US\"},\"shippingCode\":\"UPS 1D\",\"saturdayDelivery\":true,\"signatureRequired\":true},\"fillRequestKey\":\"8a97815e-ef31-43ee-af87-662aaebaec32\"}"
headers = {
    "accept": "application/json",
    "HealthDyne-Subscription-Key": "abcdefghijklmnop",
    "content-type": "application/*+json"
}

response = requests.post(url, data=payload, headers=headers)

print(response.text)
```

```csharp C#
var client = new RestClient("https://api.uat-healthdyne.com/v2/patient");
var request = new RestRequest(Method.POST);
request.AddHeader("HealthDyne-Subscription-Key", "abcdefghijklmnop");
request.AddHeader("content-type", "application/*+json");
request.AddParameter("application/*+json", "{\"patient\":{\"address\":{\"line1\":\"100 Rivers Edge Dr.\",\"city\":\"Temple Terrace\",\"state\":\"FL\",\"zipCode\":\"02155\",\"countryCode\":\"US\",\"defaultAddress\":true},\"contact\":{\"contactType\":\"Phone\",\"contactAddress\":\"5712345678\"},\"allergies\":[\"Amoxicillin\"],\"externalMedications\":[{\"ndc\":\"00045049660\",\"startDate\":\"2022-03-02\",\"endDate\":\"2022-03-02\"}],\"patientKey\":\"12389990\",\"firstName\":\"JANE\",\"lastName\":\"DOE\",\"birthDate\":\"1956-03-02\",\"gender\":\"F\"}}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);


using RestSharp;
var options = new RestClientOptions("https://api.uat-healthdyne.com/v2/script");
var client = new RestClient(options);
var request = new RestRequest("");
request.AddHeader("accept", "application/json");
var response = await client.GetAsync(request);

Console.WriteLine("{0}", response.Content);



var client = new RestClient("https://api.uat-healthdyne.com/v2/fill");
var request = new RestRequest(Method.POST);
request.AddHeader("accept", "application/json");
request.AddHeader("HealthDyne-Subscription-Key", "abcdefghijklmnop");
request.AddHeader("content-type", "application/*+json");
request.AddParameter("application/*+json", "{\"scriptKeys\":[\"e156daa5-1905-42c5-9e2e-6e99ff082d95\"],\"shipping\":{\"address\":{\"line1\":\"500 Eagles Landin Dr\",\"city\":\"Lakeland\",\"state\":\"FL\",\"zipCode\":\"33810\",\"countryCode\":\"US\"},\"shippingCode\":\"UPS 1D\",\"saturdayDelivery\":true,\"signatureRequired\":true},\"fillRequestKey\":\"8a97815e-ef31-43ee-af87-662aaebaec32\"}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
```

```javascript JavaScript
const options = {
  method: 'POST',
  headers: {
    'HealthDyne-Subscription-Key': 'abcdefghijklmnop',
    'content-type': 'application/*+json'
  },
  body: '{"patient":{"address":{"addressType":"HOME","line1":"100 Rivers Edge Dr.","city":"Temple Terrace","state":"FL","zipCode":"02155","countryCode":"US","defaultAddress":true},"contact":{"contactType":"Phone","contactAddress":"5712345678"},"allergies":["Amoxicillin"],"externalMedications":[{"ndc":"00045049660","startDate":"2022-03-02","endDate":"2022-04-02"}],"patientKey":"12389990","firstName":"JANE","lastName":"DOE","birthDate":"1956-03-02","gender":"F"}}'
};

fetch('https://api.uat-healthdyne.com/v2/patient', options)
  .then(response => response.json())
  .then(response => console.log(response))
  .catch(err => console.error(err));


const options = {method: 'GET', headers: {accept: 'application/json'}};

fetch('https://api.uat-healthdyne.com/v2/script', options)
  .then(response => response.json())
  .then(response => console.log(response))
  .catch(err => console.error(err));


const options = {
  method: 'POST',
  headers: {
    accept: 'application/json',
    'HealthDyne-Subscription-Key': 'abcdefghijklmnop',
    'content-type': 'application/*+json'
  },
  body: '{"scriptKeys":["e156daa5-1905-42c5-9e2e-6e99ff082d95"],"shipping":{"address":{"line1":"500 Eagles Landin Dr","city":"Lakeland","state":"FL","zipCode":"33810","countryCode":"US"},"shippingCode":"UPS 1D","saturdayDelivery":true,"signatureRequired":true},"fillRequestKey":"8a97815e-ef31-43ee-af87-662aaebaec32"}'
};

fetch('https://api.uat-healthdyne.com/v2/fill', options)
  .then(response => response.json())
  .then(response => console.log(response))
  .catch(err => console.error(err));
```

```json Response Example
//Patient Response
{
  "patientKey": "12389990",
  "success": true,
  "message": "The patient was added."
}

//RxReceived
{
  "eventId": "1000003",
  "eventDateUtc": "2023-05-08T19:14:55.22818Z",
  "eventType": "RXStatus",
  "patientKey": "1000002",
  "scriptKey": "1000001",
  "status": "received", 
  "statusMessage": "A new prescription has been received",   
  "detail": {
    "Reason":null
  }
}


//Fill Response
{
  "fillRequestKey": "8a97815e-ef31-43ee-af87-662aaebaec32",
  "success": true,
  "message": "The fill request was accepted."
}
```

# Create Patient

<!-- java@1-12 -->
<!-- python@1-13 -->
<!-- csharp@1-6 -->
<!-- javascript@1-13 -->

This is the first step in utilizing the HealthDyne API catalogue and is required before any other actions can be taken. Use this endpoint to provide basic information about the person the prescription is written for.

# RxReceived



If a patient has already been created via the Patient API, HealthDyne will post a status event "RxReceived" notification to let you know the patient has available scripts waiting for fulfillment.

# Get Script

<!-- java@15-23 -->
<!-- python@16-24 -->
<!-- csharp@9-16 -->
<!-- javascript@16-21 -->

Call the Script API to retrieve relevant prescription information for the scriptKey provided in the RxReceived notification.

# Submit Fill Request

<!-- java@26-38 -->
<!-- python@27-40 -->
<!-- csharp@20-26 -->
<!-- javascript@24-37 -->

Once you have received a "eRxReceived" notification from HealthDyne for a prescription, you can use this API to begin the fulfillment process. Multiple scripts can be added to a single order using the "scriptKeys" array. Please reference the Fill API guide for details on status messages.