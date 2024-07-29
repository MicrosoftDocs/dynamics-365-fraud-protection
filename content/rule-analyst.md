---
author: yvonnedeq
description: This article explains how to use the Rule reports in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 07/29/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Rule reports
ms.custom: bap-template
---

# Rule reports

Dynamics 365 Fraud Protection provides Rule reports that are designed to track the impact of Fraud Protection rules that you enabled. The reports help you understand the transaction volume, distribution, and potential fraud trends by rule and clause. You can also use them to analyze decisions and performance by rule segment, and to compare the impact of observe rules and decision rules.

## Decision rule report
You can use KPIs to filter and further analyze your decision rules. Based on the filters you select, the following metrics are available:

- **Transaction volume** – The number of transactions that were assessed by the selected decision rules.
- **Rule approval rate** – The transactions that were assessed by the selected decision rules and approved, out of all transactions that were assessed by the decision rules. 
- **Manual review rate** – The transactions that were assessed by the selected decision rules and sent for review, out of all transactions that were assessed by the decision rules.
- **Rule rejected rate** – The transactions that were assessed by the selected decision rules and rejected, out of all transactions that were assessed by the selected decision rules.
- **Fraud volume** – The confirmed fraudulent transactions that were assessed by selected decision rules.
- **Fraud rate** – The percentage of fraud volume out of the total confirmed fraud and non-fraud transactions on the selected decision rules.
- **Bank acceptance rate (when applies)** – The percentage of bank-approved transactions out of the total transactions that were sent to the bank on the selected decision rules.

### Decision rule performance table view
Decision rules are the rules that are activated for real-time decisioning by using the Fraud Protection rule engine. The table view shows the following metrics on each decision rule and clause on selected filters:

- **Transaction volume** – The number of transactions that were assessed by the decision rule.
- **Transaction distribution** – The transaction percentage of the decision rule out of all decision rules.
- **Manual review rate** – The number of transactions that were assessed by the decision rule and sent for review, out of all transactions that were assessed by the decision rule.
- **Rule rejected rate** – The number of transactions that were assessed by the decision rule and rejected, out of all transactions that were assessed by the decision rule.
- **Fraud volume** – The number of confirmed fraudulent transactions on the decision rule.
- **Non-fraud volume** – The number of confirmed non-fraudulent transactions on the decision rule.
- **Fraud rate** – The percentage of confirmed fraudulent transactions out of the total confirmed fraud and non-fraud transactions on the decision rule.
- **Send to bank volume (when applies)** – The transactions that were assessed by the decision rule and sent to the bank.
- **Bank acceptance rate (when applies)** – The percentage of bank-approved transactions out of the total transactions that were sent to the bank on the decision rule.

### Decision rule performance time series view
Based on the filters you select, the following metrics are available for analysis.

- **Transaction volume** – The transactions that were assessed by the decision rules.
- **Fraud rate** – The percentage of confirmed fraudulent transactions out of the total confirmed fraud and non-fraud transactions on the decision rules.
- **Rule/clause Distribution** – The distribution of the decision rules.
- **Score Distribution** – The distribution of Fraud Protection scores. When decision rule and clauses are selected in the filter, this chart shows the relations between decision rules and Fraud Protection scores.
- **Bank decision distribution(when applies)** – The distribution of bank decisions. When decision rule and clauses are selected in the filter, this chart shows the relation between decision rules and bank decisions.

## Observe rule report
Fraud Protection's Observe rule analysis report shows the distribution percentage for the observe rule as it's overlapped by a decision rule. The report also shows the transaction status and confirmed fraud metrics by the observe rule and clause segments.

### Observe rule performance table view
Based on the filters you select, the following metrics are available for analysis.

- **Transaction volume** – The transaction volume that was assessed by the observe rule.
- **Manual review rate** – The amount of transactions that were assessed by the decision rule and sent for review.
- **Rule rejected rate** – The amount of transactions that were assessed by the decision rule and rejected.
- **Fraud volume** – The amount of confirmed fraudulent transactions on the observe rule.
- **Non-Fraud volume** – The amount of confirmed non-fraudulent transactions on the observe rule.
- **Fraud Rate** – The percentage of fraud transactions out of the total confirmed fraud and non-fraud transactions on the observe rule.
- **Send to bank volume (when applies)** – The number of transactions that were assessed by the observe rule and sent to the bank.
- **Bank acceptance rate (when applies)** – The percentage of bank-approved transactions out of the total transactions that were sent to the bank on the observe rule.

### Overlap rule performance table view
This view shows the percentage of overlap between the observe rule and clause and the decision rule and clause. Columns represent the decision rule and clause, and rows represent the observe rule and clause.

- **Percentage** – The overlap percentage between the observe rule and clause and the decision rule and clause.

### Decision rule performance time series view
Based on the filters you select, the following metrics are available for analysis.

- **Transaction volume** – The volume that was assessed by the observe rules.
- **Fraud rate** – The percentage of fraud transactions out of the total confirmed transactions that were assessed on the observe rules.
- **Bank decision distribution(when applies)** – The percentage of bank-decisioned transactions out of the total transactions that were sent to the bank on the observe rules.

## Filters
In addition to common filters, the following filters are available for you to further analyze your data. You can select different filters and check the metrics for your analysis

- **Score** – Use the text box or the scroll bar to select the desired score range. The score is aggregated in increments of 10. For the digit in the ones place, the lower bound is rounded down to 0 (zero), and the upper bound is rounded up to 9. For example, if you select a score from 35 through 64, the metrics and charts on the report show data that has a score range from 30 through 69.
- **Merchant rule decision** – The decisions made by Fraud Protection rules. The rule decisions include **Approve**, **Reject**, **Review**, and **Challenge**.
- **Merchant final decision** – The final decisions shared through the Fraud Protection status API.
- **Decision rule/clause** – The decision rule and clauses created through the Fraud Protection rule engine.
- **Score type** – The available Fraud Protection score types.
- **Transaction status (when applies)** – The latest status of transactions.
- **Latest event, status (when applies)** – The status of transactions from the latest label or observation event.  
- **Latest fraud event, fraud flag (when applies)** – The fraud flag value from the latest label or observation event.

