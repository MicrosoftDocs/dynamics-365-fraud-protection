---
author: josaw1
description: This article provides information about the rule monitor tool in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 09/20/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Rule monitor tool (preview)
---

# Rule monitor tool (preview)

The Microsoft Dynamics 365 Fraud Protection rule monitor tool (preview) is provided as a preview service under the terms and conditions that are described in the [Microsoft Online Service Terms](https://go.microsoft.com/fwlink/?linkid=2172945). It helps merchants understand the transaction volume, distribution, and fraud trend by rules and clauses. It also lets them analyze decisions and performance by rule segments, and compare the impact of observe rules and decision rules.

The rule monitor is an interactive report tool that is built on the Power BI platform. Merchants can use it to drive purchase protection for customers in their online business by applying various filters, changing the granularity of the dimension, and viewing an analysis of rules and clauses in various market segments.

The rule monitor report is updated with the latest transactional data every 24 hours. The time stamp on the report shows the update time in Coordinated Universal Time.

The rule monitor includes the following report tabs:

- **Rule analysis** – This report shows transaction volume and distribution by rule and clause segments.
- **Decision and performance** – This report shows the transaction status and confirmed fraud metrics by rule and clause segments.
- **Observe rule analysis** – This report shows the overlap between observe rule distribution and a decision rule. It also shows transaction status and confirmed fraud metrics by observe rule and clause segments.

## Rule analysis

The **Rule analysis** report shows transaction volume and distribution by rule and clause segments. It also shows transaction volume by rule or clause over time and across score bins. Rule analysis helps users quickly identify any pattern or change in rule distribution.

The decision rule dimension lets you select whether your analysis is shown by rule or by clause. In the date granularity field, you can select daily, weekly, or monthly results.

There are four charts that show transaction volume by rule or clause segment:

- **Transaction volume by rule segment (score bin)** – This chart shows the transaction volume by rule or clause for each score bin. You can compare rule or clause volume between low and high score bins.
- **Transaction volume by rule segment (time series)** – This chart shows the transaction volume by rule or clause over time. You can monitor the change in rule or clause volume over time.
- **Final rejected, bank declines, and fraud rates** – This chart shows the final rejected, bank declined, and fraud rates for each score bin.
- **Transaction volume and distribution by rule segment** – This chart shows the transaction volume and distribution percentage by rule and clause. You can expand the rule entry to view clause transaction and distribution.

## Decision and performance

The **Decision and performance** report shows the transaction status and confirmed fraud metrics by rule and clause segments.

The report has two tabs: one for charts and one for a table. The decision rule dimension lets you select whether the data is shown by rule or by clause. In the date granularity field, you can select daily, weekly, or monthly results.

The chart tab includes five charts that provide different views of rule decision and performance:

- **Distribution of transaction status by rule segment** – This chart shows the transaction status for each rule or segment. The statuses include bank declined, chargeback, and refund. You can compare a specific percentage of a specific status for different rules to gain insights into performance.
- **Transaction volume and final rejected rate** – This chart shows the transaction volume and final rejected rate over time.
- **Transaction volume sent to bank and bank declined rate** – This chart shows the transaction volume for sent to bank and bank declined rate over time.
- **Label confirmed volume and fraud rate** – This chart shows the label confirmed volume and fraud rate over time.
- **Distribution of transactions by rule segment** – This chart shows the transaction distribution by rule or clause. The time series provides the pattern or trend in the distribution by rule or clause.

The table tab shows performance metrics for decision rules. The metrics include transaction volume, merchant final rejected rate, sent to bank volume, bank declined rate, label confirmed volume, fraud rate, non-fraud volume, and fraud volume. You can select the plus sign (**+**) on each rule to expand it and view performance metrics for each clause.

## Observe rule analysis

The **Observe rule analysis** report shows the distribution percentage for the observe rule as it's overlapped by a decision rule. It also shows the transaction status and confirmed fraud metrics by observe rule and clause segments.

There are two tables and four charts that analyze observe rule performance and compare it against decision rules:

- **Percentage of overlap between observe clause and decision clause for transactions** – This table shows the percentage of overlap between the observe rule and clause and the decision rule and clause. The columns in this table represent the decision rule and clause, and the rows represent the observe rule and clause. The value in each cell indicates the percentage of overlap between the observe rule and the decision rule. An empty cell indicates that there is no overlap. You can select the minus sign (**–**) to collapse all the clauses for the observe rule and show only the overlap percentage for the rule.
- **Performance metrics by observe rule** – This table shows performance metrics for observe rules. The metrics include transaction volume, merchant final rejected rate, sent to bank volume, bank declined rate, label confirmed volume, fraud rate, non-fraud volume, and fraud volume. You can select the plus sign (**+**) on each rule to expand it and show performance metrics for each clause.
- **Transaction volume and final rejected rate** – This chart shows the transaction volume and final rejected rate over time.
- **Transaction volume sent to bank and bank declined rate** – This chart shows the transaction volume for sent to bank and bank declined rate over time.
- **Label confirmed volume and fraud rate** – This chart shows the label confirmed volume and fraud rate over time.
- **Final rejected, bank declines, and fraud rates** – This chart shows the final rejected, bank declined, and fraud rates for each score bin.

## Appendix

The following filters are included on the reports:

- **Organization name** – This filter includes a hierarchical structure filter.
- **PI type, card type** – This filter includes credit card and types of credit card as the sub-filter.
- **Product type, category, name** – You can filter at different levels of the product filter tree.
- **Score bin** – You can set the score bin range by adjusting the slider for the score bin picker.
- **Date range** – You can set the date range by adjusting the slider or setting the date picker.
- **Decision rule, clause** – This filter includes decision rules and clauses as the sub-filter.
- **Observe rule, clause** – This filter includes observe rules and clauses as the sub-filter.
- **Bank decision** – You can filter by the bank decision that was provided.
- **Label, fraud identifier** – You can filter by fraud label and non-fraud. The fraud label might include chargebacks, refunds, and other labels that were provided.
- **Measurement unit** – You can view the report by count or by amount.

### Hidden filter pane

The following filters are included in the filter pane on the right side of the page. The filter pane can be hidden as required.

- **3DS auth flag**
- **3DS transaction status**
- **Acquirer ID**
- **Assessment type** – You can filter by evaluate or protect type.
- **AVS verify**
- **Billing country/region**
- **BIN country/region**
- **Business segment**
- **Business type**
- **Currency**
- **Guest checkout flag**
- **Merchant final decision** – You can filter by the purchase status decision that was provided.
- **Merchant first decision**
- **Merchant rule decision**
- **Merchant product category**
- **Order initiated channel**
- **Order transaction type**
- **Organization ID level 1**
- **Organization ID level 2**
- **Organization ID level 3**
- **Payer status**
- **Policy applied** – You can filter by rule/policy triggered transactions.
- **Recurring flag** – This flag indicates whether transactions are recurrent.
- **Settled flag**
- **Over zero-dollar flag** – This flag indicates whether the purchase isn't free.
- **Confirmed fraud type** – The confirmed fraud type includes chargeback, refund, merchant true reject, and purchase status.
- **Confirmed non-fraud type** – The confirmed non-fraud type includes bank approved and merchant approved.
- **Shipping country/region**
- **Shipping method**
- **User country/region**
- **User profile type**
