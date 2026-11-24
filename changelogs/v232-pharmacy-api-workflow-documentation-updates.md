---
title: v2.32 Pharmacy API Workflow Documentation Updates
author: Amit Degadwala
hidden: true
published_at: '2026-11-24T05:44:59.025Z'
---
**Internal review only**

The v2.32 Pharmacy API guides now explain what each workflow is for, how a client application hands off to HealthDyne, and what staff or patients can see at each step. Each guide includes a workflow diagram and expandable examples.

## Patient and Payment Card Updates

- The Patient guide explains when to look up, create, or update a patient and how to use the patient key to open prescriptions, coverage, and payment cards. [Patient guide](doc:patient-request#patient-onboarding-and-profile-workflow)
- The Payment Cards guide shows the hosted card form, the return to the client app, how to confirm a saved card, and how the card sequence is used in a Fill Request. The card schema links now point to v2.32. [Payment Cards guide](doc:payment-card-apis#how-a-patient-saves-and-uses-a-payment-card)

## Insurance and Fill Request Updates

- The Insurance guide shows how staff list, add, update, and deactivate patient plans and select coverage for an individual prescription. [Insurance guide](doc:insurance#how-insurance-on-the-patient-profile-is-used)
- The Fill Request guide shows the checkout-to-shipment workflow. It explains order-level versus per-prescription coverage, optional PCN for detailed inline insurance on the per-prescription route, eligible OTC items, saved cards, shipping updates, and cancellation. [Fill Request guide](doc:fill-request#how-a-fill-moves-from-checkout-to-shipment)

## Prescription Transfer Updates

- The Script guide shows prescription lookup and inbound and outbound transfer workflows. It explains queued acceptance and when to check the pharmacy outcome. The linked schema adds the inline document format and validation rules for environments where inline processing is available. [Script guide](doc:script-rxtransfer-request#prescription-lookup-and-transfer-workflow) · [Attachment schema](doc:script-rxtransfer-fields#inline-transfer-attachment)

## Mailbox Updates

- The Mailbox guide explains how applications retrieve, process, and acknowledge batches, then update prescription and order timelines. The linked schema records the optional message count of 1 to 300, default of 300, and optional discontinued-reason fields. [Mailbox guide](doc:mail-box#how-pharmacy-events-reach-your-application) · [Mailbox schemas](doc:mailbox-data-object-schemas)
- The GET Mailbox API reference now shows the same optional count and response codes as the workflow guide. [GET Mailbox API reference](ref:get_v2-mailbox)