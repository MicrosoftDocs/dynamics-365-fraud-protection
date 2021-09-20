---
author: josaw1
description: This topic provides information about the evaluate experience in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 09/20/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Monthly business review (preview version)
---



# Monthly business review (preview version)

The Dynamics 365 Fraud Protection monthly business review (preview) tool is provided as a preview service under the terms and conditions described in the Microsoft Online Service Terms. The monthly business review allows merchants to review long term business metrics, compare and track fraud and rule performance month over month, and visualize long term operational trend.

The monthly business review is an interactive report tool built on the Microsoft Power BI platform. Merchants can use this tool to drive purchase protection in their online business for their customers by applying various filters and reviewing business metrics by various segments.

The monthly business review report refreshes every 24 hours with the latest transactional data. The time stamp in the report displays the UTC refresh time for the report.

The monthly business review shows the following metrics by count or by amount.

- **Scale metrics**: Displays transaction volume, settled volume, and bank acceptance rate.

- **Decision metrics**: Displays the rule rejected volume and rate, final rejected volume and rate, and manual review rejected volume.

- **Fraud metrics**: Displays fraud volume and rate by transaction date, and fraud and rate received by 5<sup>th</sup> of the next month.

- **Fraud metrics by received date**: Display fraud volume and rate by received date.

## Appendix

### Hidden filter pane

The following filters are included in the filter pane on the right side of the screen. The filter pane can be hidden, as needed.

- **3DS auth flag**.

- **3DS transaction status**.

- **Acquirer ID**.

- **Assessment type**: Merchants can filter by evaluate or protect type.

- **AVS verify**.

- **Billing country/region**.

- **BIN country/region**.

- **Business segment**.

- **Business type**.

- **Currency**.

- **Guest checkout flag**.

- **Merchant final decision**: Merchants can filter by the purchase status decision they provided.

- **Merchant first decision**.

- **Merchant rule decision**.

- **Merchant product category**.

- **Order initiated channel**.

- **Order transaction type**.

- **Organization ID level 1**.

- **Organization ID level 2**.

- **Organization ID level 3**.

- **Payer status**.

- **Policy applied**: Merchants can filter by rule/policy triggered transactions.

- **Recurring flag**: This indicates if transactions are recurrent or not.

- **Settled flag**.

- **Over zero-dollar flag**: This indicates if the purchase is not free.

- **Confirmed fraud type**: The confirmed fraud type includes chargeback, refund, merchant true reject, and purchase status

- **Confirmed non-fraud type**: The confirmed non-fraud type includes bank approved and merchant approved.

- **Shipping country/region**.

- **Shipping method**.

- **User country/region**.

- **User profile type**.
