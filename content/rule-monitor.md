---
author: josaw1
description: This topic provides information about the rule monitor tool in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 09/20/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Rule monitor tool (preview version)
---


# Rule monitor tool (preview version)

The Dynamics 365 Fraud Protection rule monitor tool (preview) is provided as a preview service under the terms and conditions described in the Microsoft Online Service Terms. The rule monitor enables merchants to understand transaction volume, distribution, and fraud trend by rules and clauses, to analyze decision and performance by rule segments, and to compare the impact of observe rules with decision rules.

The rule monitor is an interactive report tool built on the Microsoft Power BI platform. Merchants can use this tool in their online business to drive purchase protection for their customers by applying various filters, changing the granularity of the dimension, and viewing an analysis of rules and clauses in various market segments.

The rule monitor report refreshes every 24 hours with the latest transactional data. The time stamp in the report displays the UTC refresh time for the report.

The rule monitor includes the following report tabs.

- **Rule analysis:** Displays transaction volume and distribution by rule and clause segments.

- **Decision and performance:** Displays the transaction status and confirmed fraud metrics by rule and clause segments.

- **Observe rule analysis:** Displays overlap between observe rule distribution and decision rule. It also displays transaction status and confirmed fraud metrics by observe rule and clause segments.

## Rule analysis

The rule analysis report provides transaction volume and distribution by rule and clause segments. It also provides transaction volume by rule or clause over time and across score bins. Rule analysis allows users to quickly identify any pattern or change in rule distribution.

With the decision rule dimension, you can choose to display your analysis by rule or by clause. In the date granularity field, you can choose daily, weekly, or monthly results.

There are four charts that provide transaction volume by rule/clause segment:

- **Transaction volume by rule segment (score bin):** Displays transaction volume by rule or clause for each score bin. You can compare rule or clause volume between low and high score bin.

- **Transaction volume by rule segment (time series):** Displays transaction volume by rule or clause over time. You can monitor the change in rule or clause volume over time.

- **Final rejected, bank declines, and fraud rates:** Displays the final rejected, bank declined, and fraud rates for each score bin.

- **Transaction volume and distribution by rule segment:** Displays transaction volume and distribution percentage by rule and clause. You can expand the rule entry to view clause transaction and distribution.

## Decision and performance

The decision and performance report shows the transaction status and confirmed fraud metrics by rule and clause segments.

The report has two tabs: charts and table. With the decision rule dimension, you can select whether to view the data by rule or by clause. In the date granularity field, users can choose daily, weekly, or monthly results.

There are five charts that provide different views of the rule decision and performance:

- **Distribution of transaction status** **by** **rule segment**: Displays transaction status, including bank declined, chargeback, and refund for each rule or segment. You can compare a certain percentage of a specific status for different rules and get insights on performance.

- **Transaction volume and final rejected rate:** Displays transaction volume and final rejected rate over time.

- **Transaction volume sent to bank and bank declined rate:** Displays transaction volume for sent to bank and bank declined rate over time.

- **Label confirmed volume and fraud rate:** Displays label confirmed volume and fraud rate over time.

- **Distribution of transactions by rule segment:** Displays the transaction distribution by rule or clause. The time-series provides the pattern or trend in distribution by rule or clause.

The table tab displays performance metrics, including transaction volume, merchant final rejected rate, sent to bank volume, bank declined rate, label confirmed volume, fraud rate, non-fraud volume, and fraud volume for decision rules. You can select the "**+**" icon on each rule to expand and view performance metrics for each clause.

## Observe rule analysis

The observe rule analysis report provides the distribution percentage for the observe rule as it's overlapped by a decision rule. It also displays transaction status and confirmed fraud metrics by observe rule and clause segments.

There are two tables and four charts that analyze observe rule performance and compare against decision rules:

- **Percentage of overlap between observe clause and decision clause for transactions:** Displays the percentage of overlap between the observe rule and clause and decision rule and clause. The columns in this report represent the decision rule and clause, and the rows represent the observe rule and clause. The value in each cell indicates the percentage of overlap between the observe rule and the decision rule. An empty cell indicates there is no overlap. You can select the "**–**" icon to collapse all the clauses for the observe rule and only display overlap percentage for the rule.

- **Performance metrics by observe rule:** Displays performance metrics including transaction volume, merchant final rejected rate, sent to bank volume, bank declined rate, label confirmed volume, fraud rate, non-fraud volume, and fraud volume for observe rules. You can select the "**+**" icon on each rule to expand and display performance metrics for each clause.

- **Transaction volume and final rejected rate:** Displays transaction volume and final rejected rate over time.

- **Transaction volume sent to bank and bank declined rate:** Displays transaction volume for sent to bank and bank declined rate over time.

- **Label confirmed volume and fraud rate:** Displays label confirmed volume and fraud rate over time.

- **Final rejected, bank declines, and fraud rates:** Displays the final rejected, bank declined, and fraud rates for each score bin.

## Appendix

The following filters are included in the reports.

- **Organization name**: Includes hierarchical structure filter.

- **PI type, card type**: Includes credit card and types of credit card as the sub-filter.

- **Product type, category, name**: Filter at different levels of the product filter tree.

- **Score bin:** Set the score bin range by adjusting the slider for the score bin picker.

- **Date range:** Set the date range by adjusting the slider or setting the date picker.

- **Decision rule, clause:** Includes decision rules and clauses as the sub-filter.

- **Observe rule, clause:** Includes observe rules and clauses as the sub-filter.

- **Bank decision:** Filter by the bank decision that was provided.

- **Label, fraud identifier:** Filter by fraud label and non-fraud. The fraud label may include chargebacks, refunds, and other labels provided.

- **Measurement unit:** Display the report by count or amount.

### Hidden filter pane

The following filters are included in the filter pane on the right side of the screen. The filter pane can be hidden if necessary.

- **3DS auth flag**.

- **3DS transaction status**.

- **Acquirer ID**.

- **Assessment type**: Filter by evaluate or protect type.

- **AVS verify**.

- **Billing country/region**.

- **BIN country/region**.

- **Business segment**.

- **Business type**.

- **Currency**.

- **Guest checkout flag**.

- **Merchant final decision**: Filter by the purchase status decision that was provided.

- **Merchant first decision**.

- **Merchant rule decision**.

- **Merchant product category**.

- **Order initiated channel**.

- **Order transaction type**.

- **Organization ID level 1**.

- **Organization ID level 2**.

- **Organization ID level 3**.

- **Payer status**.

- **Policy applied**: Filter by rule/policy triggered transactions.

- **Recurring flag**: Indicates whether transactions are recurrent.

- **Settled flag**.

- **Over zero-dollar flag**: Indicates if the purchase is not free.

- **Confirmed fraud type**: The confirmed fraud type includes chargeback, refund, merchant true reject, and purchase status.

- **Confirmed non-fraud type**: The confirmed non-fraud type includes bank approved and merchant approved.

- **Shipping country/region**.

- **Shipping method**.

- **User country/region**.

- **User profile type**.
