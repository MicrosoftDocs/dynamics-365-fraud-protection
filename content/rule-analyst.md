---
author: yvonnedeq
description: This article explains how to utilize the Rule analyst reports in Microsoft Dynamics 365 Fraud Protection.
ms.author: kfend
ms.date: 04/10/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Rule analyst reports
ms.custom: bap-template
---

# Rule analyst reports

Fraud Protection provides Rule analyst reports that are designed to track the impact of Fraud Protection rules that you've enabled. The reports help you understand the transaction volume, distribution, and potential fraud trends by rule and clause. You can also use them to analyze decisions and performance by rule segment, and to compare the impact of observe rules and decision rules.

## Decision rule analysis
You can use KPIs to filter and further analyze your decision rules. Based on the filters you have selected, the following metrics are available:

- **Transaction Volume** – The number of transactions that were assessed by the selected decision rules.
- **Rule Approval Rate** – The transactions that were assessed by the selected decision rules and approved, out of all transactions that were assessed by the decision rules. 
- **Manual Review Rate** – The transactions that were assessed by the selected decision rules and sent for review, out of all transactions that were assessed by the decision rules.
- **Rule Rejected Rate** – The transactions that were assessed by the selected decision rules and rejected, out of all transactions that were assessed by the selected decision rules.
- **Fraud Volume** – The confirmed fraudulent transactions that were assessed by selected decision rules.
- **Fraud Rate** – The percentage of fraud volume out of the total confirmed fraud and non-fraud transactions on the selected decision rules.
- **Bank Acceptance Rate (When applies)** – The percentage of bank-approved transactions out of the total transactions that were sent to the bank on the selected decision rules.

### Decision rule performance table view
Decision rules are the rules that have activated for real-time decisioning by using the Fraud Protection rule engine. The table view shows the following metrics on each decision rule and clause on selected filters:

- **Transaction Volume** – The number of transactions that were assessed by the decision rule.
- **Transaction Distribution** – The transaction percentage of the decision rule out of all decision rules.
- **Manual Review Rate** – The number of transactions that were assessed by the decision rule and sent for review, out of all transactions that were assessed by the decision rule.
- **Rule Rejected Rate** – The number of transactions that were assessed by the decision rule and rejected, out of all transactions that were assessed by the decision rule.
- **Fraud Volume** – The number of confirmed fraudulent transactions on the decision rule.
- **Non-Fraud Volume** – The number of confirmed non-fraudulent transactions on the decision rule.
- **Fraud Rate** – The percentage of confirmed fraudulent transactions out of the total confirmed fraud and non-fraud transactions on the decision rule.
- **Send to Bank Volume (When applies)** – The transactions that were assessed by the decision rule and sent to the bank.
- **Bank Acceptance Rate (When applies)** – The percentage of bank-approved transactions out of the total transactions that were sent to the bank on the decision rule.

### Decision rule performance time series view
Based on the filters you have selected, the following metrics are available for analysis.

- **Transaction Volume** – The transactions that were assessed by the decision rules.
- **Fraud Rate** – The percentage of confirmed fraudulent transactions out of the total confirmed fraud and non-fraud transactions on the decision rules.
- **Rule/Clause Distribution** – The distribution of the decision rules.
- **Score Distribution** – The distribution of Fraud Protection scores. When decision rule and clauses are selected in the filter, this chart shows the relations between decision rules and Fraud Protection scores.
- **Bank Decision Distribution** – The distribution of bank decisions. When decision rule and clauses are selected in the filter, this chart shows the relation between decision rules and bank decisions.

## Observe rule analysis
Fraud Protection's Observe rule analysis report shows the distribution percentage for the observe rule as it's overlapped by a decision rule. The report also shows the transaction status and confirmed fraud metrics by the observe rule and clause segments.

### Observe rule performance table view
Based on the filters you have selected, the following metrics are available for analysis.

- **Transaction Volume** – The transaction volume that was assessed by the observe rule.
- **Manual Review Rate** – The amount of transactions that were assessed by the decision rule and sent for review.
- **Rule Rejected Rate** – The amount of transactions that were assessed by the decision rule and rejected.
- **Fraud Volume** – The amount of confirmed fraudulent transactions on the observe rule.
- **Non-Fraud Volume** – The amount of confirmed non-fraudulent transactions on the observe rule.
- **Fraud Rate** – The percentage of fraud transactions out of the total confirmed fraud and non-fraud transactions on the observe rule.
- **Send to Bank Volume (When applies)** – The number of transactions that were assessed by the observe rule and sent to the bank.
- **Bank Acceptance Rate (When applies)** – The percentage of bank-approved transactions out of the total transactions that were sent to the bank on the observe rule.

### Overlap rule performance table view
This view shows the percentage of overlap between the observe rule and clause and the decision rule and clause. Columns represent the decision rule and clause, and rows represent the observe rule and clause.

- **Percentage** – The overlap percentage between the observe rule and clause and the decision rule and clause.

### Decision rule performance time series view
Based on the filters you have selected, the following metrics are available for analysis.

- **Transaction Volume** – The volume that was assessed by the observe rules.
- **Fraud Rate** – The percentage of fraud transactions out of the total confirmed transactions that were assessed on the observe rules.
- **Bank Decision Distribution** – The percentage of bank-decisioned transactions out of the total transactions that were sent to the bank on the observe rules.

## Filters
In addition to common filters, the following filters are available for you to further analyze your data. You can select different filters and check the metrics for your analysis

- **Score** – Use the text box or the scroll bar to select the desired score range. The score is aggregated in increments of 10. For the digit in the ones place, the lower bound is rounded down to 0 (zero), and the upper bound is rounded up to 9. For example, if you select a score from 35 through 64, the metrics and charts on the report show data that has a score range from 30 through 69.
- **Merchant Rule Decision** – The decisions that were made by Fraud Protection rules. The rule decisions include **Approve**, **Reject**, **Review**, and **Challenge**.
- **Merchant Final Decision** – The final decisions that were shared through the Fraud Protection status API.
- **Decision Rule/Clause** – The decision rule and clauses that were created through the Fraud Protection rule engine.
- **Transaction Status** – The latest status of transactions.
- **Score Type** – The available Fraud Protection score types.
