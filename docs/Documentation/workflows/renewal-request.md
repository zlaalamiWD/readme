---
title: Renewal Request
deprecated: false
hidden: false
metadata:
  robots: index
---
# Renewal Request:

See [Renewal](ref:post_v2-renewal) API reference for request message fields.

This API lets the client initiate an outreach a request to the Physician for a new prescription on behalf of the patient. The API validates that the client has received a Proactive Renewal mail box event and requests that the client get approval from the patient for us to outreach to their physician.

# Submit Renewal Request

API field validation information in Appendix [Renewal Request Fields](https://docs.healthdyne.com/docs/renewal-request-fields#renewal-request-data-object)

Client must send a Renewal request with following details:

1. fillRequestKey: Unique key used to track each Renewal Request.
2. scriptKeys: an array of scriptKey(s) sent in Script API and in a "Transferred" status.

#### Server

##### Only HTTPS connections are accepted.

| METHOD TYPE | ENDPOINT                                      |
| :---------- | :-------------------------------------------- |
| POST (Test) | api.uat-healthdyne.com/v2/fill/renewalrequest |
| POST (Prod) | api.healthdyne.com/v2/fill/renewalrequest     |

#### Header

| Key                         | Value                  |
| :-------------------------- | :--------------------- |
| Accept                      | application/json       |
| Content-Type                | application/json       |
| HealthDyne-Subscription-Key | Provided by HealthDyne |

#### Sample Submit Renewal Request

`POST https://api.uat-healthdyne.com/v2/fill/renewalrequest`

#### Sample Submit Renewal Request Body

```json
{
  "fillRequestKey": "RenewalRequest01",
  "scriptKeys": [
    {
      "scriptKey": "ScRenewalEnd12",
      "patientInsurance": {
        "planNumber": "59253",
        "secondaryPlanNumber": "59254",
        "tertiaryPlanNumber": "59255"
      }
    },
    {
      "scriptKey": "ScRenewalEnd13",
      "patientInsurance": {
        "planNumber": "59254",
        "secondaryPlanNumber": "59255",
        "tertiaryPlanNumber": "59253"
      }
    }
  ],
  "shipping": {
    "address": {
      "line1": "500 Eagles Landin Dr",
      "line2": null,
      "line3": null,
      "city": "Lakeland",
      "state": "FL",
      "zipCode": "33810",
      "countryCode": "US"
    }
  }
}
```

Click here to see [Submit Renewal Request Data Object](https://docs.healthdyne.com/docs/renewal-request-fields#request-object)

#### Sample Submit Fill Response

```json
{
    "fillRequestKey": "RenewalRequest01",
    "message": "The renewal request was accepted"
}
```

Click here to see [Submit Renewal Response Data Object](https://docs.healthdyne.com/docs/renewal-request-fields#response-object-1)

# Renewal Request Status Mailbox Events

Please see the [Renewal Request](doc:mail-box#renewal-request-status-events) status events under the [Mailbox](doc:mail-box) API guide for a detailed list of status events.

# Renewed Status

HealthDyne will create the order after receiving a Renewal Request by sending create order command in the downstream pharmacy management system. Once the order has been successfully created, HealthDyne will generate a ‘renewed’ order status message and queues the event up for the client to retrieve it. See [Renewal Request Submitted Status Event](doc:mail-box#renewed).