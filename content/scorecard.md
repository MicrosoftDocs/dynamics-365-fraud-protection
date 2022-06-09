---
author: josaw1
description: This article explains how to review key metrics and understand the performance of fraud protection efforts in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 09/23/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Review key metrics with scorecard reports
---

# Review key metrics with scorecard reports

You can use the scorecard reports to review your key metrics and understand the month-by-month performance of your fraud protection efforts.

In the evaluate experience, your scorecard lets you evaluate the capabilities of Microsoft Dynamics 365 Fraud Protection. In the protect experience, your scorecard reflects the real-time performance of Fraud Protection as your system of record. After evaluating the data presented in the scorecard, you can use the knowledge that you gain to make well-informed risk management decisions for your business.

Your top-four key performance indicators (KPIs) are summarized across the top of the page to provide a snapshot of your performance. You can fully investigate these metrics in the charts.

## Customize your view

You can use the drop-down menus and sliders to filter your view of the interactive charts. The following options are available:

- **Measurement unit** - Toggle between dollar amount and count.
- **Aggregation level** – Show a daily, weekly, or monthly view of your data.
- **Merchant rule decision** – Show approval and/or rejection decisions that were the result of your settings in Fraud Protection.
- **Merchant final decision** – Show the latest status of the purchase.
- **MID classification** – Show all program merchant IDs (MIDs) and/or standard MIDs.
- **Transaction date** – Show transaction data by date. You can select dates in the calendar, enter them manually, or select ranges of dates.

To clear previous selections, hover over the category name, and then select the Clear selections icon (the eraser symbol). Note that one value must be selected for the **Aggregation level** and **Measurement unit** options.

## KPI charts

The scorecard plots the following metrics:

- **Transaction volume** – The total count of transactions that were sent for assessment.
- **Final approval rate** – The percentage of purchases that were approved out of the total volume.
- **Settled rate** – The percentage of bank approvals out of the total volume that was sent to banks.
- **Chargeback rate by receive date** – The percentage of chargebacks out of the total volume that was approved by banks on the chargeback receive date and the transaction date.


## Additional resources

[Scorecard reports for PSPs](scorecard-psp.md)

[!INCLUDE[footer-include](includes/footer-banner.md)]
