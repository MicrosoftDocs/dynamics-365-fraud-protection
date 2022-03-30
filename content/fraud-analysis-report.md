---
author: josaw1
description: This topic explains how to configure user access to Microsoft Dynamics 365 Fraud Protection.
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

Microsoft Dynamics 365 Fraud Protection provides ability to analyze transactions to determine whether a transaction is fraudulent, and to understand changing fraud patterns for your business. It helps you understand fraud volume (by count and dollar amount), distribution, and trend, and lets them do analysis on fraud transactions by payment instrument, product, and IP country/region.

Your top key performance indicators (KPIs) are summarized at the top of the fraud analysis page to provide a snapshot of your transactions labeled by you as fraudulent. You can use the charts on the page to drill down and fully investigate the metrics.

The fraud analysis tool is updated with the latest transactional data every 24 hours. The time stamp on the report shows the update time in Coordinated Universal Time.

You can switch views between count view and amount view. Count view shows volume and percentage by transaction count and amount view shows volume and percentage in US dollars.

The machine learning model in Fraud Protection evaluates every transaction by using advanced adaptive AI and then assigns a risk score. Generally the higher the risk score, the higher the perceived risk. The machine learning model uses a range of risk scores from 0 (zero) through 999.

**User filters in fraud analysis**

You can use the drop-down menus and sliders on the tool to filter your view of the interactive charts. The following filter options are available:

- **PI type** This filter includes payment instrument type such as card type.

- **Product type** – You can filter at product type.

- **IP country/region** – Country/region based on IP address.

- **Date range** – Use this filter to show transaction data by date. You can select dates in the calendar, enter dates manually, or select date ranges.

- **Score range:** use the input or scroll bar to select desired score range from 0 to 999, incremental of 10.

- **Non-fraud type** – You can filter by non-fraud label. The non-fraud label might include bank approved, merchant approved, and other labels previously provided by you. <u>Changing this will impact denominator for the calculation of fraud rate.</u>

- **Fraud type** – You can filter by fraud label. The fraud label might include chargebacks, refunds, merchant rejected, and other labels previously provided by you. <u>Changing this will impact fraud volume and numerator for the calculation of fraud rate.</u>

To clear specific filter selections, hover over the category name, and then select the **Clear selections** button (eraser symbol). To reset all filters to the default options, select **Reset**.

**Fraud summary**

The scorecard provides the following fraud summary metrics:

- **Transaction volume** – This chart shows the total count or number of transactions that were sent for assessment.

- **Fraud volume** –total volume of transaction labeled as fraud in fraud type filter.

- **Fraud rate** – percentage of transaction labeled as fraud in fraud type filter, among total transactions labeled as fraud or non-fraud.

**Fraud detail charts**

The KPI charts provide details about the following key performance metrics. You can switch date granularity between daily, weekly, or monthly view of your data.

- **Fraud rate** – percentage of transaction labeled as fraud in fraud type filter, among total transactions labeled as fraud or non-fraud.

- **Fraud by transaction status** – Volume of fraud by transaction status.

- **Fraud by payment instrument** – This report shows the fraud distribution by payment instrument (PI) type.

- **Fraud by product** – This report shows the fraud distribution by product type, category, and name.

- **Fraud by IP country/region** – This report shows the fraud distribution by IP country/region.
