---
author: josaw1
description: This topic describes how payment service providers (PSPs) can use scorecard reports in Microsoft Dynamics 365 Fraud Protection to review key metrics and understand the performance of their fraud protection efforts.
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

Microsoft Dynamics 365 Fraud Protection provides scorecard reports that are designed specifically for payment service providers (PSPs). You can use them to review your key metrics and understand the performance of your fraud protection efforts.

In the evaluate experience, the scorecard provides data that helps you evaluate capabilities in Fraud Protection. In the protect experience, it reflects the real-time performance of Fraud Protection. You can use the data to make well-informed risk management decisions for your business.

Your top-six key performance indicators (KPIs) are summarized across the top of the scorecard page to provide a snapshot of your fraud protection performance. You can use the charts on the page to drill down and fully investigate the metrics.

## Customize your view

You can use the drop-down menus and sliders on the scorecard to filter your view of the interactive charts. The following filter options are available:

- **Merchant rule decision** – Use this filter to show approval, review, and rejection decisions that are a result of settings that you configured in Fraud Protection.
- **Merchant final decision** – Use this filter to show the latest status of a purchase.
- **MID classification** – Use this filter to show all program merchant IDs (MIDs) and standard MIDs.
- **Date range** – Use this filter to show transaction data by date. You can select dates in the calendar, enter dates manually, or select date ranges.
- **Date granularity** – Use this filter to show a daily, weekly, or monthly view of your data.

To clear specific filter selections, hover over the category name, and then select the **Clear selections** button (eraser symbol). To reset all filters to the default options, select **Reset**.

## KPI charts

The scorecard provides details for the following key performance metrics:

- **Transaction volume** – This chart shows the total count of transactions that were sent for assessment.
- **Rule approval rate** – Out of the total volume of purchases, this chart shows the percentage that was approved by rules.
- **Rule review rate** – Out of the total volume of purchases, this chart shows the percentage that was sent by rules for manual review.
- **Rule rejected rate** – Out of the total volume of purchases, this chart shows the percentage that was rejected by rules.
- **Chargeback rate by transaction date** – Out of the total volume of chargebacks, this chart shows the percentage that was approved by banks on the chargeback transaction date.
- **Chargeback rate by receive date** – Out of the total volume of chargebacks, this chart shows the percentage that was approved by banks on the receive date.

## Additional resources

[Review key metrics with scorecard reports](scorecard.md)
