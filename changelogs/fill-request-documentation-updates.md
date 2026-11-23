---
title: Fill Request Documentation Updates
author: Amit Degadwala
hidden: true
published_at: '2026-11-23T04:19:35.651Z'
type: improved
---
## Fill Request Updates

The Fill Request guide now documents the two ways to submit one or more prescriptions for the same patient and explains how to check the order outcome after the API accepts the request. [Fill Request guide](doc:fill-request)

* Standard Fill Request: Send prescription keys with optional order-level insurance. [Standard POST API reference](ref:post_v2-fill)
* Per-prescription Fill Request: Supply insurance for individual prescriptions using existing plan numbers or inline details. PCN is optional for inline insurance on this route. Eligible OTC items can be included with the prescription order. [Per-prescription POST API reference](ref:post_v2-fill-fillrequest)

## Fill Request Status, Shipping, and Cancellation

* Get Fill Request: Look up events by `fillRequestKey`. The response groups events by status. When no matching record is found, the API returns HTTP 200 with problem details. [GET API reference](ref:get_v2-fill-fillrequest)
* Update shipping: Send the Fill Request key and shipping details while the order is still editable. The update applies to the whole order. [PUT API reference](ref:put_v2-fill)
* Cancel Fill Request: Specify prescription keys to cancel selected lines. Omit the keys or send an empty array to request cancellation of the whole order. [Cancel API reference](ref:post_v2-fill-cancel)

## Fill Request Schemas

The schema appendix now separates the standard and per-prescription submission fields. It includes the nested insurance and OTC item fields, the status response groups, and the shipping update and cancellation request bodies. [Fill Request Data Object (Schemas)](doc:fill-request-fields) · [Fill Request Fields (Updated Fields)](doc:fill-request-fields-copy)

## Mailbox Event Updates

The Mailbox guide now includes an `RxIssue` example for prescription-level issues. It also explains how to match Mailbox events to a Fill Request, identifies `RxCanceled` as the cancellation status, and links to the copay and payment events. [Mailbox guide](doc:mail-box#fill-request-status-events) · [Mailbox event schemas](doc:mailbox-data-object-schemas#fillrequest-event-type)