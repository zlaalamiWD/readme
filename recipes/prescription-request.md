---
title: Prescription Request
description: Simple example of submitting a single prescription request.
hidden: true
recipe:
  color: '#018FF4'
  icon: ''
---
```java Java
OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/*+json");
RequestBody body = RequestBody.create(mediaType, "{\"patient\":{\"address\":{\"addressType\":\"Home\",\"line1\":\"123 Main Street\",\"city\":\"123 Main Street\",\"state\":\"CO\",\"zipCode\":\"800016\",\"defaultAddress\":true},\"contact\":{\"contactType\":\"Phone\",\"contactAddress\":\"7201234567\"},\"allergies\":[\"Amoxicillin\"],\"externalMedications\":[{\"ndc\":\"00045049660\",\"notes\":\"TYLENOL      TAB 325MG\",\"startDate\":\"2021-01-03\",\"endDate\":\"2022-01-12\"}],\"patientId\":\"23426523423\",\"firstName\":\"First\",\"lastName\":\"Last\",\"birthDate\":\"1960-01-01\",\"gender\":\"M\"},\"prescription\":{\"ndc\":\"13533070501\",\"drugName\":\"PROLASTIN-C INJ 1000MG\",\"quantity\":30},\"shipping\":{\"address\":{\"addressType\":\"Home\",\"line1\":\"123 Main Street\",\"city\":\"Centennial\",\"state\":\"CO\",\"zipCode\":\"800016\",\"defaultAddress\":true},\"shippingCode\":\"POS 1C\",\"saturdayDelivery\":false,\"signatureRequired\":false},\"requestId\":\"RID0244\",\"lineOfBusiness\":\"LOB\"}");
Request request = new Request.Builder()
  .url("https://api.uat-healthdyne.com/v1/prescriptionrequest")
  .post(body)
  .addHeader("accept", "application/json")
  .addHeader("HealthDyne-Subscription-Key", "abcdefghijklmnop")
  .addHeader("content-type", "application/*+json")
  .build();

Response response = client.newCall(request).execute();
```

```python Python
url = "https://api.uat-healthdyne.com/v1/prescriptionrequest"

payload = "{\"patient\":{\"address\":{\"addressType\":\"Home\",\"line1\":\"123 Main Street\",\"city\":\"123 Main Street\",\"state\":\"CO\",\"zipCode\":\"800016\",\"defaultAddress\":true},\"contact\":{\"contactType\":\"Phone\",\"contactAddress\":\"7201234567\"},\"allergies\":[\"Amoxicillin\"],\"externalMedications\":[{\"ndc\":\"00045049660\",\"notes\":\"TYLENOL      TAB 325MG\",\"startDate\":\"2021-01-03\",\"endDate\":\"2022-01-12\"}],\"patientId\":\"23426523423\",\"firstName\":\"First\",\"lastName\":\"Last\",\"birthDate\":\"1960-01-01\",\"gender\":\"M\"},\"prescription\":{\"ndc\":\"13533070501\",\"drugName\":\"PROLASTIN-C INJ 1000MG\",\"quantity\":30},\"shipping\":{\"address\":{\"addressType\":\"Home\",\"line1\":\"123 Main Street\",\"city\":\"Centennial\",\"state\":\"CO\",\"zipCode\":\"800016\",\"defaultAddress\":true},\"shippingCode\":\"POS 1C\",\"saturdayDelivery\":false,\"signatureRequired\":false},\"requestId\":\"RID0244\",\"lineOfBusiness\":\"LOB\"}"
headers = {
    "accept": "application/json",
    "HealthDyne-Subscription-Key": "abcdefghijklmnop",
    "content-type": "application/*+json"
}

response = requests.post(url, data=payload, headers=headers)

print(response.text)
```

```csharp C#
var client = new RestClient("https://api.uat-healthdyne.com/v1/prescriptionrequest");
var request = new RestRequest(Method.POST);
request.AddHeader("accept", "application/json");
request.AddHeader("HealthDyne-Subscription-Key", "abcdefghijklmnop");
request.AddHeader("content-type", "application/*+json");
request.AddParameter("application/*+json", "{\"patient\":{\"address\":{\"addressType\":\"Home\",\"line1\":\"123 Main Street\",\"city\":\"123 Main Street\",\"state\":\"CO\",\"zipCode\":\"800016\",\"defaultAddress\":true},\"contact\":{\"contactType\":\"Phone\",\"contactAddress\":\"7201234567\"},\"allergies\":[\"Amoxicillin\"],\"externalMedications\":[{\"ndc\":\"00045049660\",\"notes\":\"TYLENOL      TAB 325MG\",\"startDate\":\"2021-01-03\",\"endDate\":\"2022-01-12\"}],\"patientId\":\"23426523423\",\"firstName\":\"First\",\"lastName\":\"Last\",\"birthDate\":\"1960-01-01\",\"gender\":\"M\"},\"prescription\":{\"ndc\":\"13533070501\",\"drugName\":\"PROLASTIN-C INJ 1000MG\",\"quantity\":30},\"shipping\":{\"address\":{\"addressType\":\"Home\",\"line1\":\"123 Main Street\",\"city\":\"Centennial\",\"state\":\"CO\",\"zipCode\":\"800016\",\"defaultAddress\":true},\"shippingCode\":\"POS 1C\",\"saturdayDelivery\":false,\"signatureRequired\":false},\"requestId\":\"RID0244\",\"lineOfBusiness\":\"LOB\"}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
```

```json Response Example
{
    "prescriptionRequest": {
      "requestId": "RID0244",
      "lineOfBusiness": "LOB",
      "patient": {
        "patientId": "23426523423",
        "memberId": null,
        "firstName": "First",
        "lastName": "Last",
        "birthDate": "1960-01-01T00:00:00",
        "address": {
          "addressType": "Home",
          "addressName": null,
          "line1": "123 Main Street",
          "line2": null,
          "line3": null,
          "city": "123 Main Street",
          "state": "CO",
          "zipCode": "80016",
          "defaultAddress": true,
          "contact": null
        },
        "insurance": null,
        "contact": {
          "contactType": "Phone",
          "contactAddress": "7201234567"
        },
        "gender": "M",
        "stateId": null,
        "allergies": [
          "PENICILLINS"
        ],
        "externalMedications": [
          {
            "ndc": "00045049660",
            "notes": "TYLENOL      TAB 325MG",
            "startDate": "2021-01-03T00:00:00",
            "endDate": "2022-01-12T00:00:00"
          }
        ]
      },
      "prescription": {
        "rxNumber": null,
        "drugName": "PROLASTIN-C INJ 1000MG",
        "ndc": "13533070501",
        "providerNpi": null,
        "pharmacyNpi": null,
        "quantity": 30
      },
      "shipping": {
        "address": {
          "addressType": "Home",
          "addressName": null,
          "line1": "123 Main Street",
          "line2": null,
          "line3": null,
          "city": "Centennial",
          "state": "CO",
          "zipCode": "80016",
          "defaultAddress": true,
          "contact": null
        },
        "shippingCode": "POS 1C",
        "saturdayDelivery": false,
        "signatureRequired": false,
        "bulkShipment": false
      }
    },
    "receivedUtc": "2023-05-05T18:21:54.6766103Z",
    "success": true,
    "errors": null
  }
```

# Submit Prescription Request

<!-- java@1-13 -->
<!-- python@1-12 -->
<!-- csharp@1-7 -->

Submit a prescription request to add a patient and start fulfillment on a prescription that has already been sent to HealthDyne via eRx / Surescripts. Please see the Order Status API guide for status information.