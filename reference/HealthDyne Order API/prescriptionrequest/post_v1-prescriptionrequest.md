---
title: /v1/prescriptionrequest
excerpt: ''
api:
  file: healthdyne-order-api.json
  operationId: post_v1-prescriptionrequest
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
See full field definitions in Appendix under [Prescription / Refill / Cancel Request Fields](doc:prescription-request)

## API Authentication and Authorization

HealthDyne secures access to its APIs via an API subscription key which is to be used for authentication and authorization. The API key must be submitted in the header of each API request. Please contact your HealthDyne account team to be assigned an API Key.

### Header

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Key
      </th>
      <th>
        Value
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        Accept
      </td>
      <td>
        application/json
      </td>
    </tr>
    <tr>
      <td>
        Content-Type
      </td>
      <td>
        application/json
      </td>
    </tr>
    <tr>
      <td>
        HealthDyne-Subscription-Key
      </td>
      <td>
        &lt;API KEY&gt; Provided by HealthDyne
      </td>
    </tr>
  </tbody>
</Table>