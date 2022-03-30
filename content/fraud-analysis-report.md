---
author: josaw1
description: This topic describes the fraud analysis report for purchase protection that is available in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 03/31/2022
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Fraud analysis report for purchase protection
---

# Fraud analysis report for purchase protection

Dynamics 365 Fraud Protection provides the ability to analyze transactions to determine whether a transaction is fraudulent, and to understand changing fraud patterns for your business. It helps you understand fraud volume by count and dollar amount, distribution, and trend. It also enables you to do analysis on fraud transactions by payment instrument, product, and IP country or region.

Your top key performance indicators (KPIs) are summarized at the top of the **Fraud analysis** page, providing a snapshot of  transactions labeled by you as fraudulent. You can use the charts on the page to drill down and fully investigate the metrics.

The **Fraud analysis** report is updated with the latest transactional data every 24 hours. The time stamp on the report shows the time the report was last updated, in Coordinated Universal Time.

You can switch views on the report between **Count view** and **Amount view**. **Count view** shows volume and percentage by transaction count and **Amount view** shows volume and percentage in US dollars.

The machine learning (ML) model in Fraud Protection evaluates every transaction by using advanced adaptive artificial intelligence (AI) and then assigns a risk score. In general, the higher the risk score, the higher the perceived risk. The ML model uses a range of risk scores from 0 through 999.

## User filters

You can use the drop-down menus and sliders on the report to filter your view of the interactive charts. The following filter options are available.

- **PI type** – This filter includes payment instrument type such as **Card type**.

- **Product type** – This filter enables you to display based on product type.

- **IP country/region** – You can filter on country or region, based on IP address.

- **Date range** – Use this filter to show transaction data by date. You can select dates in the calendar, enter dates manually, or select date ranges.

- **Score range** – Use the text input box or the scroll bar to select desired score range, from 0 to 999, by increments of 10.

- **Non-fraud type** – Use this option to filter by non-fraud label. The non-fraud label may include *Bank approved*, *Merchant approved*, and other labels that you previously provided. 
> [!NOTE]
> Changing this value will impact the denominator for the calculation of fraud rate.

- **Fraud type** – Use this option to filter by fraud label. The fraud label may include *Chargebacks*, *Refunds*, *Merchant rejected*, and other labels that you previously provided.
> [!NOTE]
> Changing this value will impact fraud volume and the numerator for the calculation of fraud rate.

To clear specific filter selections, hover over the category name, and then select the **Clear selections** button (eraser icon). To reset all filters to the default options, select **Reset**.

## Fraud summary scorecard

The **Fraud summary** scorecard provides the following fraud summary metrics.

- **Transaction volume** – This chart shows the total count or number of transactions that were sent for assessment.

- **Fraud volume** – This value represents the total volume of transaction labeled as fraud in the fraud type filter.

- **Fraud rate** – This chart shows the percentage of transactions labeled as fraud in the fraud type filter, among total transactions labeled as fraud or non-fraud.

## Fraud detail charts

The KPI charts provide details about the following key performance metrics. You can switch date granularity between daily, weekly, or monthly view of your data.

- **Fraud rate** – This chart shows the percentage of transactions labeled as fraud in fraud type filter, among total transactions labeled as fraud or non-fraud.

- **Fraud by transaction status** – This chart shows the volume of fraud by transaction status.

- **Fraud by payment instrument** – This report shows the fraud distribution by payment instrument (PI) type.

- **Fraud by product** – This report shows the fraud distribution by product type, category, and name.

- **Fraud by IP country/region** – This report shows the fraud distribution by IP country or region.
