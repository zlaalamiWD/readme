---
title: Rx Transfer Overview
description: >-
  This recipe shows how to do a simple prescription transfer and fulfillment in
  3 steps:

  1. Create a Patient.

  2. Request the Prescription Transfer.

  3. Submit a Fill request.
hidden: false
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

MediaType mediaType = MediaType.parse("application/*+json");
RequestBody body = RequestBody.create(mediaType, "{\"sendingPharmacy\":{\"pharmacist\":{\"firstName\":\"John\",\"lastName\":\"Doe\"},\"contact\":{\"contactType\":\"Phone\",\"contactAddress\":\"6789012345\"},\"address\":{\"line1\":\"401 My Pharmacy Dr.\",\"city\":\"Lakeland\",\"state\":\"FL\",\"zipCode\":\"33810\"},\"pharmacyName\":\"MyPharmacy\",\"pharmacyNpi\":\"981000000999\",\"pharmacyNcpdp\":\"981000000999\",\"deaNumber\":\"981000000999\",\"phone\":\"1234567890\"},\"receivingPharmacy\":{\"pharmacist\":{\"firstName\":\"Phil\",\"lastName\":\"Doe\"},\"contact\":{\"contactType\":\"Phone\",\"contactAddress\":\"3456789012\"},\"address\":{\"line1\":\"500 Eagles Landing Dr.\",\"city\":\"Lakeland\",\"state\":\"FL\",\"zipCode\":\"33810\"},\"pharmacyName\":\"HEALTHDYNE\",\"pharmacyNpi\":\"1093974982\",\"pharmacyNcpdp\":\"1093974982\",\"deaNumber\":\"1093974982\",\"phone\":\"3456789012\"},\"prescription\":{\"prescriber\":{\"address\":{\"line1\":\"123 Doctor Lane\",\"city\":\"Lakeland\",\"state\":\"FL\",\"zipCode\":\"33810\"},\"firstName\":\"Doctor\",\"lastName\":\"Doe\",\"npi\":\"1093456789\",\"dea\":\"1093456789\",\"phoneNumber\":\"5556667777\"},\"rxNumber\":\"45678\",\"prescribedNdc\":\"56789010211\",\"prescribedDrugName\":\"Tylenol\",\"dispenseNdc\":\"56789010212\",\"dispenseDrugName\":\"Ibuprofen\",\"drugDosageForm\":\"TABS\",\"drugStrength\":\"500mg\",\"daysSupply\":90,\"quantityWritten\":180,\"quantityDispensedToDate\":90,\"firstFillDispensedQuantity\":90,\"remainingQuantity\":90,\"labelDirections\":\"TAKE 1 TABLET DAILY\",\"writtenDate\":\"2022-04-04\",\"expirationDate\":\"2022-06-04\",\"dawCode\":\"0\",\"lastFillDate\":\"2022-04-04\",\"firstFillDate\":\"2022-04-04\",\"fillsToDate\":1,\"refillsAuthorized\":1,\"refillsLeft\":1,\"refillsTransferred\":1,\"currentFillNumber\":2},\"scriptKey\":\"e156daa5-1905-42c5-9e2e-6e99ff082d95\",\"patientKey\":\"12389990\",\"transferFileType\":\"png\",\"transferFileUrl\":\"http:\\\\\\\\ScoobyDoobyDoo.com\"}");
Request request = new Request.Builder()
  .url("https://api.uat-healthdyne.com/v2/script")
  .post(body)
  .addHeader("accept", "application/json")
  .addHeader("HealthDyne-Subscription-Key", "abcdefghijklmnop")
  .addHeader("content-type", "application/*+json")
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

payload = "{\"sendingPharmacy\":{\"pharmacist\":{\"firstName\":\"John\",\"lastName\":\"Doe\"},\"contact\":{\"contactType\":\"Phone\",\"contactAddress\":\"6789012345\"},\"address\":{\"line1\":\"401 My Pharmacy Dr.\",\"city\":\"Lakeland\",\"state\":\"FL\",\"zipCode\":\"33810\"},\"pharmacyName\":\"MyPharmacy\",\"pharmacyNpi\":\"981000000999\",\"pharmacyNcpdp\":\"981000000999\",\"deaNumber\":\"981000000999\",\"phone\":\"1234567890\"},\"receivingPharmacy\":{\"pharmacist\":{\"firstName\":\"Phil\",\"lastName\":\"Doe\"},\"contact\":{\"contactType\":\"Phone\",\"contactAddress\":\"3456789012\"},\"address\":{\"line1\":\"500 Eagles Landing Dr.\",\"city\":\"Lakeland\",\"state\":\"FL\",\"zipCode\":\"33810\"},\"pharmacyName\":\"HEALTHDYNE\",\"pharmacyNpi\":\"1093974982\",\"pharmacyNcpdp\":\"1093974982\",\"deaNumber\":\"1093974982\",\"phone\":\"3456789012\"},\"prescription\":{\"prescriber\":{\"address\":{\"line1\":\"123 Doctor Lane\",\"city\":\"Lakeland\",\"state\":\"FL\",\"zipCode\":\"33810\"},\"firstName\":\"Doctor\",\"lastName\":\"Doe\",\"npi\":\"1093456789\",\"dea\":\"1093456789\",\"phoneNumber\":\"5556667777\"},\"rxNumber\":\"45678\",\"prescribedNdc\":\"56789010211\",\"prescribedDrugName\":\"Tylenol\",\"dispenseNdc\":\"56789010212\",\"dispenseDrugName\":\"Ibuprofen\",\"drugDosageForm\":\"TABS\",\"drugStrength\":\"500mg\",\"daysSupply\":90,\"quantityWritten\":180,\"quantityDispensedToDate\":90,\"firstFillDispensedQuantity\":90,\"remainingQuantity\":90,\"labelDirections\":\"TAKE 1 TABLET DAILY\",\"writtenDate\":\"2022-04-04\",\"expirationDate\":\"2022-06-04\",\"dawCode\":\"0\",\"lastFillDate\":\"2022-04-04\",\"firstFillDate\":\"2022-04-04\",\"fillsToDate\":1,\"refillsAuthorized\":1,\"refillsLeft\":1,\"refillsTransferred\":1,\"currentFillNumber\":2},\"scriptKey\":\"e156daa5-1905-42c5-9e2e-6e99ff082d95\",\"patientKey\":\"12389990\",\"transferFileType\":\"png\",\"transferFileUrl\":\"http:\\\\\\\\ScoobyDoobyDoo.com\"}"
headers = {
    "accept": "application/json",
    "HealthDyne-Subscription-Key": "abcdefghijklmnop",
    "content-type": "application/*+json"
}

response = requests.post(url, data=payload, headers=headers)

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
request.AddParameter("application/*+json", "{\"patient\":{\"address\":{\"addressType\":\"HOME\",\"line1\":\"100 Rivers Edge Dr.\",\"city\":\"Temple Terrace\",\"state\":\"FL\",\"zipCode\":\"02155\",\"countryCode\":\"US\",\"defaultAddress\":true},\"contact\":{\"contactType\":\"Phone\",\"contactAddress\":\"5712345678\"},\"allergies\":[\"Amoxicillin\"],\"externalMedications\":[{\"ndc\":\"00045049660\",\"startDate\":\"2022-03-02\",\"endDate\":\"2022-04-02\"}],\"patientKey\":\"12389990\",\"firstName\":\"JANE\",\"lastName\":\"DOE\",\"birthDate\":\"1956-03-02\",\"gender\":\"F\"}}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);


var client = new RestClient("https://api.uat-healthdyne.com/v2/script");
var request = new RestRequest(Method.POST);
request.AddHeader("accept", "application/json");
request.AddHeader("HealthDyne-Subscription-Key", "abcdefghijklmnop");
request.AddHeader("content-type", "application/*+json");
request.AddParameter("application/*+json", "{\"sendingPharmacy\":{\"pharmacist\":{\"firstName\":\"John\",\"lastName\":\"Doe\"},\"contact\":{\"contactType\":\"Phone\",\"contactAddress\":\"6789012345\"},\"address\":{\"line1\":\"401 My Pharmacy Dr.\",\"city\":\"Lakeland\",\"state\":\"FL\",\"zipCode\":\"33810\"},\"pharmacyName\":\"MyPharmacy\",\"pharmacyNpi\":\"981000000999\",\"pharmacyNcpdp\":\"981000000999\",\"deaNumber\":\"981000000999\",\"phone\":\"1234567890\"},\"receivingPharmacy\":{\"pharmacist\":{\"firstName\":\"Phil\",\"lastName\":\"Doe\"},\"contact\":{\"contactType\":\"Phone\",\"contactAddress\":\"3456789012\"},\"address\":{\"line1\":\"500 Eagles Landing Dr.\",\"city\":\"Lakeland\",\"state\":\"FL\",\"zipCode\":\"33810\"},\"pharmacyName\":\"HEALTHDYNE\",\"pharmacyNpi\":\"1093974982\",\"pharmacyNcpdp\":\"1093974982\",\"deaNumber\":\"1093974982\",\"phone\":\"3456789012\"},\"prescription\":{\"prescriber\":{\"address\":{\"line1\":\"123 Doctor Lane\",\"city\":\"Lakeland\",\"state\":\"FL\",\"zipCode\":\"33810\"},\"firstName\":\"Doctor\",\"lastName\":\"Doe\",\"npi\":\"1093456789\",\"dea\":\"1093456789\",\"phoneNumber\":\"5556667777\"},\"rxNumber\":\"45678\",\"prescribedNdc\":\"56789010211\",\"prescribedDrugName\":\"Tylenol\",\"dispenseNdc\":\"56789010212\",\"dispenseDrugName\":\"Ibuprofen\",\"drugDosageForm\":\"TABS\",\"drugStrength\":\"500mg\",\"daysSupply\":90,\"quantityWritten\":180,\"quantityDispensedToDate\":90,\"firstFillDispensedQuantity\":90,\"remainingQuantity\":90,\"labelDirections\":\"TAKE 1 TABLET DAILY\",\"writtenDate\":\"2022-04-04\",\"expirationDate\":\"2022-06-04\",\"dawCode\":\"0\",\"lastFillDate\":\"2022-04-04\",\"firstFillDate\":\"2022-04-04\",\"fillsToDate\":1,\"refillsAuthorized\":1,\"refillsLeft\":1,\"refillsTransferred\":1,\"currentFillNumber\":2},\"scriptKey\":\"e156daa5-1905-42c5-9e2e-6e99ff082d95\",\"patientKey\":\"12389990\",\"transferFileType\":\"png\",\"transferFileUrl\":\"http:\\\\\\\\ScoobyDoobyDoo.com\"}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);


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


const options = {
  method: 'POST',
  headers: {
    accept: 'application/json',
    'HealthDyne-Subscription-Key': 'abcdefghijklmnop',
    'content-type': 'application/*+json'
  },
  body: '{"sendingPharmacy":{"pharmacist":{"firstName":"John","lastName":"Doe"},"contact":{"contactType":"Phone","contactAddress":"6789012345"},"address":{"line1":"401 My Pharmacy Dr.","city":"Lakeland","state":"FL","zipCode":"33810"},"pharmacyName":"MyPharmacy","pharmacyNpi":"981000000999","pharmacyNcpdp":"981000000999","deaNumber":"981000000999","phone":"1234567890"},"receivingPharmacy":{"pharmacist":{"firstName":"Phil","lastName":"Doe"},"contact":{"contactType":"Phone","contactAddress":"3456789012"},"address":{"line1":"500 Eagles Landing Dr.","city":"Lakeland","state":"FL","zipCode":"33810"},"pharmacyName":"HEALTHDYNE","pharmacyNpi":"1093974982","pharmacyNcpdp":"1093974982","deaNumber":"1093974982","phone":"3456789012"},"prescription":{"prescriber":{"address":{"line1":"123 Doctor Lane","city":"Lakeland","state":"FL","zipCode":"33810"},"firstName":"Doctor","lastName":"Doe","npi":"1093456789","dea":"1093456789","phoneNumber":"5556667777"},"rxNumber":"45678","prescribedNdc":"56789010211","prescribedDrugName":"Tylenol","dispenseNdc":"56789010212","dispenseDrugName":"Ibuprofen","drugDosageForm":"TABS","drugStrength":"500mg","daysSupply":90,"quantityWritten":180,"quantityDispensedToDate":90,"firstFillDispensedQuantity":90,"remainingQuantity":90,"labelDirections":"TAKE 1 TABLET DAILY","writtenDate":"2022-04-04","expirationDate":"2022-06-04","dawCode":"0","lastFillDate":"2022-04-04","firstFillDate":"2022-04-04","fillsToDate":1,"refillsAuthorized":1,"refillsLeft":1,"refillsTransferred":1,"currentFillNumber":2},"scriptKey":"e156daa5-1905-42c5-9e2e-6e99ff082d95","patientKey":"12389990","transferFileType":"png","transferFileUrl":"http:\\\\ScoobyDoobyDoo.com"}'
};

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


//Script Response
{
  "scriptKey": "e156daa5-1905-42c5-9e2e-6e99ff082d95",
  "message": "The transfer was accepted.",
  "success": true
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

# Transfer Prescription

<!-- java@15-27 -->
<!-- python@16-29 -->
<!-- csharp@9-15 -->
<!-- javascript@16-29 -->

This step is required for transferring a prescription from another pharmacy. If the prescription was submitted via Surescripts directly to HealthDyne, see the eScript recipe. Please reference the Script API guide for details on status messages.

# Submit a Fill Request

<!-- java@30-42 -->
<!-- python@32-45 -->
<!-- csharp@18-24 -->
<!-- javascript@32-45 -->

Once you have received a "completed" status from HealthDyne for a prescription transfer Script request, you can use this API to begin the fulfillment process. Multiple scripts can be added to a single order using the "scriptKeys" array. Please reference the Fill API guide for details on status messages.