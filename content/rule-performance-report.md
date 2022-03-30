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
title: Rule performance report

---

# Rule performance report

Microsoft Dynamics 365 Fraud Protection provides a rule performance report designed to track the impact of fraud protection rules enabled by you. It helps merchants understand the transaction volume, distribution, and potential fraud trends by rules and clauses. It also lets them analyze decisions and performance by rule segments and compare the impact of observe rules and decision rules.

Your top key performance indicators (KPIs) are summarized at the top of the rule performance page to provide a snapshot of your rules. You can use the charts on the page to drill down and fully investigate the metrics.

The purchase protection rule performance report is updated with the latest transactional data every 24 hours. The time stamp on the report shows the update time in Coordinated Universal Time.

Users can switch views between count view and amount view. Count view shows volume and percentage by transaction count and amount view shows volume and percentage in US dollars.

The machine learning model in Fraud Protection evaluates every transaction by using advanced adaptive AI. It then assigns a risk score. The higher the risk score, the higher the perceived risk. The machine learning model uses a range of risk scores from 0 (zero) through 999.

**User filters in rule performance**

You can use the drop-down menus and sliders on the tool to filter your view of the interactive charts. The following filter options are available:

- **PI type** This filter includes payment instrument type such as card type.

- **Product type** – You can filter at product type.

- **IP country/region** – Country/region based on IP address.

- **Date range** – Use this filter to show transaction data by date. You can select dates in the calendar, enter dates manually, or select date ranges.

- **Score range:** use the input or scroll bar to select desired score range from 0 to 999, incremental of 10.

- **Non-fraud type** – You can filter by non-fraud label. The non-fraud label might include bank approved, merchant approved, and other labels previously provided by you. <u>Changing this will impact denominator for the calculation of fraud rate.</u>

- **Fraud type** – You can filter by fraud label. The fraud label might include chargebacks, refunds, merchant rejected, and other labels previously provided by you. <u>Changing this will impact fraud volume and numerator for the calculation of fraud rate.</u>

To clear specific filter selections, hover over the category name, and then select the **Clear selections** button (eraser symbol). To reset all filters to the default options, select **Reset**.

**Rule summary**

The rule performance provides the following rule summary metrics:

- **Transaction volume** – This chart shows the total count or number of transactions that were sent for assessment.

- **Manual review rate** – Out of the total volume of purchases, this chart shows the percentage that was sent by rules for manual review.

- **Rule rejected rate** – Out of the total volume of purchases, this chart shows the percentage that was rejected by rules.

- **Fraud rate** – Percentage of transaction labeled as fraud in fraud type filter, among total transactions labeled as fraud or non-fraud.

**Rule detail charts**

The KPI charts provide details about the following key performance metrics. Users can switch date granularity between daily, weekly, or monthly view of your data.

Decision rules

- **Decision rules**– This chart shows the transaction volume and distribution percentage by decision rule and clause. It also shows rule review rate, rule rejected rate and fraud rate. You can expand the rule entry to view clause transaction and distribution. Users can click any of the decision rule or clause to filter on these charts.

<!-- -->

- **Transaction volume –** This chart shows the total count or number of transactions that were sent for assessment.

<!-- -->

- **Rule rejected rate-** Out of the total volume of purchases, this chart shows the percentage that was rejected by decision rules.

Observe rules

- **Observe rules**– This chart shows the transaction volume and distribution percentage by observe rule and clause. It also shows rule review rate, rule rejected rate and fraud rate. You can expand the rule entry to view clause transaction and distribution. Users can click any of the observe rules or clauses to filter on these charts.

<!-- -->

- **Transaction volume –** This chart shows the total count or number of transactions that were sent for assessment.

<!-- -->

- **Rule rejected rate-** Out of the total volume of purchases, this chart shows the percentage that was rejected by decision rules.

Overlap

- **Overlap rules** – This table shows the percentage of overlap between the observe rule and the decision rule. The columns in this table represent the decision rule, and the rows represent the observe rule and clause. The value in each cell indicates the percentage of overlap between the observe rule and the decision rule. An empty cell indicates that there is no overlap. Users can click any of the observe rule or clause to filter on these charts.

<!-- -->

- **Transaction volume –** This chart shows the total count or number of transactions that were sent for assessment.

<!-- -->

- **Rule rejected rate-** Out of the total volume of purchases, this chart shows the percentage that was rejected by decision rules.
