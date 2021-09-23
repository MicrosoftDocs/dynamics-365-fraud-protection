---
author: josaw1
description: This topic provides information about how payment service providers (PSPs) can use scorecard reports in Microsoft Dynamics 365 Fraud Protection to review key metrics and fraud protection performance.
ms.author: josaw
ms.date: 09/23/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Scorecard reports for PSPs (preview)
---

# Scorecard reports for PSPs (preview)

[!include [preview banner](includes/preview-banner.md)]

You can use the scorecard reports to review your key metrics and understand the performance of your fraud protection efforts. 

In the evaluate experience, your scorecard lets you evaluate the capabilities of Microsoft Dynamics 365 Fraud Protection. In the protect experience, your scorecard reflects the real-time performance of Fraud Protection as your system of record. After evaluating the data presented in the scorecard, you can use the knowledge that you gain to make well-informed risk management decisions for your business.

Your top-six key performance indicators (KPIs) are summarized across the top of the page to provide a snapshot of your performance. You can fully investigate these metrics in the charts. 

## Customize your view

You can use the drop-down menus and sliders to filter your view of the interactive charts. The following options are available: 

- Merchant rule decision – Show approval, review and/or rejection decisions that were the result of your settings in Fraud Protection. 

- Merchant final decision – Show the latest status of the purchase. 

- MID classification – Show all program merchant IDs (MIDs) and/or standard MIDs. 

- Date range – Show transaction data by date. You can select dates in the calendar, enter them manually, or select ranges of dates. 

- Date granularity – Show a daily, weekly, or monthly view of your data. 

To clear previous selections for filters, hover over the category name, and then select the Clear selections icon (the eraser symbol). Alternatively, click the “reset” button to reset all filters to default selections.  

## KPI charts

The scorecard plots the following metrics: 

- Transaction volume – The total count of transactions that were sent for assessment. 

- Rule approval rate – The percentage of purchases that were approved by rules out of the total volume. 

- Rule review rate – The percentage of purchases that were sent to manual review by rules out of the total volume. 

- Rule rejected rate – The percentage of purchases that were rejected by rules out of the total volume. 

- Chargeback rate by transaction date – The percentage of chargebacks out of the total volume that was approved by banks on the chargeback transaction date 

- Chargeback rate by receive date – The percentage of chargebacks out of the total volume that was approved by banks on the receive date. 

 

