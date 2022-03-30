---
author: josaw1
description: This topic describes the Rule performance report for purchase protection in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 03/31/2022
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Rule performance report for purchase protection

---

# Rule performance report for purchase protection

Dynamics 365 Fraud Protection provides a **Rule performance** report that is designed to track the impact of Fraud Protection rules that you have enabled. The report can help you understand the transaction volume, distribution, and potential fraud trends by rules and clauses. It also enables you to analyze decisions and performance by rule segments and compare the impact of observe rules and decision rules.

Your top key performance indicators (KPIs) are summarized at the top of the **Rule performance** page, providing a snapshot of your rules. You can use the charts on the page to drill down and fully investigate the metrics.

The **Rule performance** report for purchase protection is updated with the latest transactional data every 24 hours. The time stamp on the report shows the time the report was last updated, in Coordinated Universal Time.

You can switch views on the report between **Count view** and **Amount view**. **Count view** shows volume and percentage by transaction count and **Amount view** shows volume and percentage in US dollars.

The machine learning (ML) model in Fraud Protection evaluates every transaction by using advanced adaptive artificial intelligence (AI) and then assigns a risk score. In general, the higher the risk score, the higher the perceived risk. The ML model uses a range of risk scores from 0 through 999.

## User filters

You can use the drop-down menus and sliders on the report to filter your view of the interactive charts. The following filter options are available.

- **PI type** – This filter includes payment instrument type such as **Card type**.

- **Product type** – This filter enables you to display based on product type.

- **IP country/region** – You can filter on country or region, based on IP address.

- **Date range** – Use this filter to show transaction data by date. You can select dates in the calendar, enter dates manually, or select date ranges.

- **Score range** – Use the text input box or the scroll bar to select desired score range, from 0 to 999, by increments of 10.

- **Non-fraud type** – Use this option to filter by non-fraud label. The non-fraud label may include *Bank approved*, *Merchant approved*, and other labels that you previously provided. 
> [!NOTE]
> Changing this value will impact the denominator for the calculation of fraud rate.

- **Fraud type** – Use this option to filter by fraud label. The fraud label may include *Chargebacks*, *Refunds*, *Merchant rejected*, and other labels that you previously provided.
> [!NOTE]
> Changing this value will impact fraud volume and the numerator for the calculation of fraud rate.

To clear specific filter selections, hover over the category name, and then select the **Clear selections** button (eraser icon). To reset all filters to the default options, select **Reset**.

## Rule summary metrics

The **Rule performance** report provides the following rule summary metrics.

- **Transaction volume** – This chart shows the total count or number of transactions that were sent for assessment.

- **Manual review rate** – This chart shows the percentage of purchases that was sent by rules for manual review, out of the total volume of purchases.

- **Rule rejected rate** – This chart shows the percentage of purchases that was rejected by rules, out of the total volume of purchases.

- **Fraud rate** – This shows the percentage of transactions labeled as fraud in the fraud type filter, among total transactions labeled as fraud or non-fraud.

## Rule detail charts

The KPI charts provide details about the following key performance metrics. You can switch date granularity between daily, weekly, or monthly view of your data.

### Decision rules

- **Decision rules** – This chart shows the transaction volume and distribution percentage by decision rule and clause. It also shows rule review rate, rule rejected rate, and fraud rate. You can expand the rule entry to view clause transaction and distribution. You can select any of the decision rules or clauses to filter on.

- **Transaction volume** – This chart shows the total count or number of transactions that were sent for assessment.

- **Rule rejected rate** - This chart shows the percentage of purchases that were rejected by decision rules, out of the total volume of purchases.

### Observe rules

- **Observe rules** – This chart shows the transaction volume and distribution percentage by observe rule and clause. It also shows rule review rate, rule rejected rate, and fraud rate. You can expand the rule entry to view clause transaction and distribution. You can select any of the observe rules or clauses to filter on.

- **Transaction volume** – This chart shows the total count or number of transactions that were sent for assessment.

- **Rule rejected rate** – This chart shows the percentage of purchases that was rejected by decision rules, out of the total volume of purchases.

### Overlap

- **Overlap rules** – This table shows the percentage of overlap between observe rules and decision rules. The columns represent the decision rules, and the rows represent the observe rules and clauses. The value in each cell represents the percentage of overlap between the observe rule and the decision rule. An empty cell indicates that there is no overlap. You can select any of the observe rules or clauses to filter on.

- **Transaction volume** – This chart shows the total count or number of transactions that were sent for assessment.

- **Rule rejected rate** - This chart shows the percentage of purchases that was rejected by decision rules, out of the total volume of purchases.
