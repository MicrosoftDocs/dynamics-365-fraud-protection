---
author: josaw1
description: This article describes the Long term report for purchase protection in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 03/31/2022
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Long term report for purchase protection
---

# Long term report for purchase protection

Microsoft Dynamics 365 Fraud Protection provides a **Long term** report for purchase protection. You can use the report to review your key metrics and understand the performance of your fraud protection efforts for historical transactions over six months old.

Your top key performance indicators (KPIs) are summarized at the top of the **Long term** page to provide a snapshot of transactions that you've labeled as fraudulent. You can use the charts on the page to drill down and fully investigate the metrics.

The **Long term** report for purchase protection is updated with the latest transactional data every 24 hours. The time stamp on the report shows the time when the report was last updated, in Coordinated Universal Time.

You can switch views on the report between **Count view** and **Amount view**. **Count view** shows volume and percentage by transaction count, and **Amount view** shows volume and percentage in US dollars.

The machine learning (ML) model in Fraud Protection evaluates every transaction by using advanced adaptive artificial intelligence (AI) and then assigns a risk score. In general, the higher the risk score, the higher the perceived risk. The ML model uses a range of risk scores from 0 through 999.

## User filters

You can use the drop-down menus and sliders on the report to filter your view of the interactive charts. The following filter options are available:

- **PI type** – Include the payment instrument type, such as **Card type**.
- **Product type** – Change the display based on the product type.
- **IP country/region** – Filter by country or region, based on Internet Protocol (IP) address.
- **Date range** – Show transaction data by date. You can select dates in the calendar, manually enter dates, or select date ranges.
- **Score range** – Use the text box or the scroll bar to select the desired score range, from 0 through 999, in increments of 10.
- **Non-fraud type** – Filter by non-fraud label. The non-fraud labels might include *Bank approved*, *Merchant approved*, and other labels that you previously provided.

    > [!NOTE]
    > Changes to this value will affect the denominator for the calculation of the fraud rate.

- **Fraud type** – Filter by fraud label. The fraud labels might include *Chargebacks*, *Refunds*, *Merchant rejected*, and other labels that you previously provided.

    > [!NOTE]
    > Changes to this value will affect the fraud volume and the numerator for the calculation of the fraud rate.

To clear specific filter selections, hover over the category name, and then select the **Clear selections** button (eraser symbol). To reset all filters to the default options, select **Reset**.

## Key performance indicators

The **Long term** report provides the following key performance metrics:

- **Transaction volume** – The total count or number of transactions that were sent for assessment.
- **Manual review rate** – The percentage of purchases that were sent by rules for manual review, out of the total volume of purchases.
- **Rule rejected rate** – The percentage of purchases that were rejected by rules, out of the total volume of purchases.
- **Bank acceptance rate** – The percentage of transactions that were approved by the bank, out of all the transactions that were sent.
- **Chargeback received** – The total volume of chargebacks that were received during the given date range.
- **Fraud volume** – The total volume of transactions that were labeled as fraud in the **Fraud type** filter.
- **Fraud rate** – The percentage of transactions that were labeled as fraud in the **Fraud type** filter, out of the total transactions that were labeled as fraud or non-fraud.
- **Average score** – The average score for the total transactions.

## KPI charts

The KPI charts provide details about the following key performance metrics. You can change the date granularity for a daily, weekly, or monthly view of your data.

- **Transaction volume** – The total count or number of transactions that were sent for assessment.
- **Rule rejected rate** – The percentage of purchases that were rejected by rules, out of the total volume of purchases.
- **Bank acceptance rate** – The percentage of transactions that were approved by the bank, out of all the transactions that were sent.
- **Fraud rate** – The percentage of transactions that were labeled as fraud in the **Fraud type** filter, out of the total transactions that were labeled as fraud or non-fraud.
- **Score distribution** – The transaction volume distribution by risk score, in increments of 10. You can switch between a **Chart** layout and a **Table** layout.

[!INCLUDE[footer-include](includes/footer-banner.md)]
