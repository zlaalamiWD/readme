---
title: Pharmacy APIs
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
HealthDyne's Pharmacy APIs allow developers to integrate our fulfillment capabilities into their organization's healthcare applications.

Get started by adding reviewing the [Patient](doc:patient-request), [Script](doc:script-rxtransfer-request), and [Fill](doc:fill-request) request documentation. Visit the [API Reference](ref:patient) or check the [Recipes](https://docs.healthdyne.com/v2.0/recipes) page for example requests.

# Rx / Fulfillment Workflows

## eRx / Surescripts

1. Create / update patient record using Patient API [Patient API Guide](doc:patient-request)
2. RxReceived notification in Mailbox API [Mailbox API Guide](doc:mail-box)
3. Query Script API using scriptKey to retrieve prescription details [Script API Guide](https://docs.healthdyne.com/v2.17/docs/script-rxtransfer-request)
4. Generate fill request using Fill API [Fill API Guide](https://docs.healthdyne.com/v2.17/docs/fill-request)
5. Retrieve status updates via Mailbox API [Mailbox API Guide](https://docs.healthdyne.com/v2.17/docs/mail-box)

See the [eRx / Surescript Workflow Recipe](https://docs.healthdyne.com/v2.17/recipes/escript-surescript-overview) for an example workflow.

## Rx Transfer

1. Create / update patient record using Patient API [Patient API Guide](docs:patient-request)
2. Submit Rx Transfer via Script API [Script API Guide](https://docs.healthdyne.com/v2.17/docs/script-rxtransfer-request)
3. Generate fill request using Fill API once RxTransferred notification is received [Fill API Guide](https://docs.healthdyne.com/v2.17/docs/fill-request)
4. Retrieve status updates via Mailbox API [Mailbox API Guide](https://docs.healthdyne.com/v2.17/docs/mail-box)

See the [Rx Transfer Workflow Recipe](https://docs.healthdyne.com/v2.17/recipes/prescription-transfer-overview) for an example workflow.
