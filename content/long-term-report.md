---
author: josaw1
description: This topic details the Long term report for purchase protection in Microsoft Dynamics 365 Fraud Protection.
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

Dynamics 365 Fraud Protection provides a **Long term** report for purchase protection. You can use the report to review your key metrics and understand the performance of your fraud protection efforts for historical transactions over 6 months old.

Your top key performance indicators (KPIs) are summarized at the top of the report, providing a snapshot of  transactions labeled by you as fraudulent. You can use the charts on the page to drill down and fully investigate the metrics.

The purchase protection **Long term** report is updated with the latest transactional data every 24 hours. The time stamp on the report shows the time the report was last updated, in Coordinated Universal Time.

You can switch views on the report between **Count view** and **Amount view**. **Count view** shows volume and percentage by transaction count and **Amount view** shows volume and percentage in US dollars.

The machine learning (ML) model in Fraud Protection evaluates every transaction by using advanced adaptive artificial intelligence (AI) and then assigns a risk score. In general, the higher the risk score, the higher the perceived risk. The ML model uses a range of risk scores from 0 through 999.

## User filters

You can use the drop-down menus and sliders on the report to filter your view of the interactive charts. The following filter options are available.

- **PI type** – Includes payment instrument type such as **Card type**.

- **Product type** – Enables you to display based on product type.

- **IP country/region** – Filter on country or region, based on IP address.

- **Date range** – Show transaction data by date. You can select dates in the calendar, enter dates manually, or select date ranges.

- **Score range** – Use the text input box or the scroll bar to select desired score range, from 0 to 999, by increments of 10.

- **Non-fraud type** – Filter by non-fraud label. The non-fraud label may include *Bank approved*, *Merchant approved*, and other labels that you previously provided. 
> [!NOTE]
> Changing this value will impact the denominator for the calculation of fraud rate.

- **Fraud type** – Filter by fraud label. The fraud label may include *Chargebacks*, *Refunds*, *Merchant rejected*, and other labels that you previously provided.
> [!NOTE]
> Changing this value will impact fraud volume and the numerator for the calculation of fraud rate.

To clear specific filter selections, hover over the category name, and then select the **Clear selections** button (eraser icon). To reset all filters to the default options, select **Reset**.

## Key performance indicators

The **Long term** report provides the following key performance metrics.

- **Transaction volume** – Shows the total count or number of transactions that were sent for assessment.

- **Manual review rate** – Shows the percentage or purchases that was sent by rules for manual review, out of the total volume of purchases.

- **Rule rejected rate** – Shows the percentage of purchases that was rejected by rules, out of the total volume of purchases.

- **Bank acceptance rate** – Shows the percentage of transactions approved by the bank, out of all the transactions sent.

- **Chargeback received** – Shows the total volume of chargebacks received within the given date range.

- **Fraud volume** – Shows the total volume of transaction labeled as fraud in the **Fraud type** filter.

- **Fraud rate** – Shows the percentage of transactions labeled as fraud in the **Fraud type** filter, out of the total transactions labeled as fraud or non-fraud.

- **Average score** – Shows the average score for the total transactions.

## KPI charts

The KPI charts provide details about the following key performance metrics. You can change the date granularity for daily, weekly, or monthly views of your data.

- **Transaction volume** – Shows the total count or number of transactions that were sent for assessment.

- **Rule rejected rate** – Shows the percentage of purchases that was rejected by rules, out of the total volume of purchases.

- **Bank acceptance rate** – Shows the percentage of transactions approved by the bank, out of all the transactions sent.

- **Fraud rate** – Shows the percentage of transactions labeled as fraud in the **Fraud type** filter, out of the total transactions labeled as fraud or non-fraud.

- **Score distribution** – Shows the transaction volume distribution by risk score, in increments of 10. You can switch between **Chart** layout or **Table** layout.

