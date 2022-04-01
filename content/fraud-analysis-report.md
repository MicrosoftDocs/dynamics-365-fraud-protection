---
author: josaw1
description: This topic describes the Fraud Analysis report for purchase protection in Microsoft Dynamics 365 Fraud Protection.
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

Microsoft Dynamics 365 Fraud Protection lets you analyze transactions to determine whether a transaction is fraudulent and understand changing fraud patterns for your business. It helps you understand fraud volume by count and dollar amount, distribution, and trend. It also lets you analyze fraud transactions by payment instrument, product, and Internet Protocol (IP) country or region.

Your top key performance indicators (KPIs) are summarized at the top of the **Fraud analysis** page to provide a snapshot of transactions that you've labeled as fraudulent. You can use the charts on the page to drill down and fully investigate the metrics.

The **Fraud analysis** report is updated with the latest transactional data every 24 hours. The time stamp on the report shows the time when the report was last updated, in Coordinated Universal Time.

You can switch views on the report between **Count view** and **Amount view**. **Count view** shows volume and percentage by transaction count, and **Amount view** shows volume and percentage in US dollars.

The machine learning (ML) model in Fraud Protection evaluates every transaction by using advanced adaptive artificial intelligence (AI) and then assigns a risk score. In general, the higher the risk score, the higher the perceived risk. The ML model uses a range of risk scores from 0 through 999.

## User filters

You can use the drop-down menus and sliders on the report to filter your view of the interactive charts. The following filter options are available.

- **PI type** – Include the payment instrument type, such as **Card type**.
- **Product type** – Change the display based on the product type.
- **IP country/region** – Filter by country or region, based on IP address.
- **Date range** – Show transaction data by date. You can select dates in the calendar, manually enter dates, or select date ranges.
- **Score range** – Use the text box or the scroll bar to select the desired score range, from 0 through 999, in increments of 10.
- **Non-fraud type** – Filter by non-fraud label. The non-fraud labels might include *Bank approved*, *Merchant approved*, and other labels that you previously provided. 

    > [!NOTE]
    > Changes to this value will affect the denominator for the calculation of the fraud rate.

- **Fraud type** – Filter by fraud label. The fraud labels might include *Chargebacks*, *Refunds*, *Merchant rejected*, and other labels that you previously provided.

    > [!NOTE]
    > Changes to this value will affect the fraud volume and the numerator for the calculation of the fraud rate.

To clear specific filter selections, hover over the category name, and then select the **Clear selections** button (eraser symbol). To reset all filters to the default options, select **Reset**.

## Fraud summary scorecard

The **Fraud summary** scorecard provides the following fraud summary metrics:

- **Transaction volume** – The total count or number of transactions that were sent for assessment.
- **Fraud volume** – The total volume of transactions that were labeled as fraud in the **Fraud type** filter.
- **Fraud rate** – The percentage of transactions that were labeled as fraud in the **Fraud type** filter, out of the total transactions that were labeled as fraud or non-fraud.

## Fraud detail charts

The KPI charts provide details about the following key performance metrics. You can switch the date granularity for a daily, weekly, or monthly view of your data.

- **Fraud rate** – The percentage of transactions that were labeled as fraud in the **Fraud type** filter, out of the total transactions that were labeled as fraud or non-fraud.
- **Fraud by transaction status** – The volume of fraud by transaction status.
- **Fraud by payment instrument** – The fraud distribution by payment instrument type.
- **Fraud by product** – The fraud distribution by product type, category, and name.
- **Fraud by IP country/region** – The fraud distribution by country or region, based on IP address.

[!INCLUDE[footer-include](includes/footer-banner.md)]
