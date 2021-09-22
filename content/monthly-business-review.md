---
author: josaw1
description: This topic provides information about the monthly business review tool (preview version) in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 09/20/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Monthly business review tool (preview version)
---

# Monthly business review tool (preview version)

[!include [preview banner](includes/preview-banner.md)]

The Microsoft Dynamics 365 Fraud Protection monthly business review tool (preview) is provided as a preview service under the terms and conditions that are described in the [Microsoft Online Service Terms](https://go.microsoft.com/fwlink/?linkid=2172945). It lets merchants review long-term business metrics, compare and track fraud and rule performance month over month, and visualize long-term operational trends.

The monthly business review is an interactive report tool that is built on the Power BI platform. Merchants can use it to drive purchase protection for customers in their online business by applying various filters and reviewing business metrics by various segments.

The monthly business review report is updated with the latest transactional data every 24 hours. The time stamp on the report shows the update time in Coordinated Universal Time.

The monthly business review shows the following metrics by count or by amount:

- **Scale metrics** – The transaction volume, settled volume, and bank acceptance rate.
- **Decision metrics** – The rule rejected volume and rate, final rejected volume and rate, and manual review rejected volume.
- **Fraud metrics** – The fraud volume and rate by transaction date, and the fraud and rate that were received by the fifth of the next month.
- **Fraud metrics by received date** – The fraud volume and rate by received date.

## Appendix

### Hidden filter pane

The following filters are included in the filter pane on the right side of the page. The filter pane can be hidden as required.

- **3DS auth flag**
- **3DS transaction status**
- **Acquirer ID**
- **Assessment type** – You can filter by evaluate or protect type.
- **AVS verify**
- **Billing country/region**
- **BIN country/region**
- **Business segment**
- **Business type**
- **Currency**
- **Guest checkout flag**
- **Merchant final decision** – You can filter by purchase status decision that was previously provided.
- **Merchant first decision**
- **Merchant rule decision**
- **Merchant product category**
- **Order initiated channel**
- **Order transaction type**
- **Organization ID level 1**
- **Organization ID level 2**
- **Organization ID level 3**
- **Payer status**
- **Policy applied** – You can filter by rule/policy triggered transactions.
- **Recurring flag** – This flag indicates whether transactions are recurrent.
- **Settled flag**
- **Over zero-dollar flag** – This flag indicates whether the purchase isn't free.
- **Confirmed fraud type** – This filter includes chargeback, refund, merchant true reject, and purchase status.
- **Confirmed non-fraud type** – This filter includes bank approved and merchant approved.
- **Shipping country/region**
- **Shipping method**
- **User country/region**
- **User profile type**
