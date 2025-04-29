---
title: Fill Request Rejection Reason
deprecated: false
hidden: true
metadata:
  robots: index
---
| Reason                                                  | Mailbox description                                                                                                                                                                                               |
| :------------------------------------------------------ | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Invalid shipping code.                                  | The shipping code is not a valid code                                                                                                                                                                             |
| Invalid pharmacy.                                       | The OriginatingPharmacy does not contain the correct values.                                                                                                                                                      |
| Duplicate RXs found.                                    | The order contained more than one prescription with the same RX number.                                                                                                                                           |
| Failed Duplicate order check                            | There is another order with the same OrderNumber that is either waiting to be dispensed or has been shipped.                                                                                                      |
| Invalid NDC: ###########                                | The NDC is not a dispensable drug. The placeholder ########### will contain the submitted NDC.                                                                                                                    |
| Invalid NDC: ########### has Alternate NDC: XXXXXXXXXXX | The NDC is not a dispensable drug but the order can be resubmitted using an alternate NDC. The placeholder ########### will contain the submitted NDC and placeholder XXXXXXXXXXX will contain the alternate NDC. |