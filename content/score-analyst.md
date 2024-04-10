---
author: yvonnedeq
description: This article provides information about the Score analyst reports Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 04/10/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Score analyst reports
ms.custom: bap-template
---

# Score analyst reports

Fraud Protection provides Score analyst reports that use innovative artificial intelligence (AI) technology to analyze historical views of your data, and to help you set up and adjust optimal risk score thresholds. This information can then be transformed into rules that help you decide, in real time, whether to accept or reject customer transactions.

Advanced adaptive AI and other state-of-the-art AI technologies are used to generate a risk score on every transaction. The higher the risk score, the higher the perceived risk. The ML model uses a range of risk scores from 0 through 999. The score is aggregated in increments of 10. The lower bound is rounded down, and upper bound is rounded up. For example, if you select a score from 35 through 64, the metrics and charts on the report show data that has a score range from 30 through 69.

## KPIs
The following KPIs are included:

- **Transaction Volume** – The transaction volume at or above the score during the selected date range, by count or amount.
- **Rule Approval Rate** – The percentage of transactions at or above the score by count or amount that was approved by the decision rules.
- **Manual Review Rate** – The percentage of transactions at or above the score by count or amount that was sent for review by the decision rules.
- **Rule Rejected Rate** – The percentage of transactions at or above the score by count or amount that was rejected by the decision rules.
- **Fraud Volume** – The confirmed fraudulent transactions by count or amount.
- **Fraud Rate** – The percentage of confirmed fraud volume out of the total confirmed fraud and non-fraud transactions.
- **Bank Acceptance Rate (When applies)** – The percentage of bank-approved transactions out of the total transactions that were sent to the bank at or above the score.

## Distribution and performance report
Fraud control professionals can use the **Distribution and performance** report to analyze the relationship between Fraud Protection scores and other segments of the data, such as decisions, rule clauses, and transaction status.

### Score view
When you select the **Score** view, based on the filters you have selected, the following metrics are available:

- **Transaction volume by score** – The transaction volume in each score.
- **Fraud rate by score**

    - **Fraud volume** – The confirmed volume of fraudulent transactions in each score.
    - **Fraud rate** – The percentage of fraud volume out of the total confirmed fraud and non-fraud volume in each score.

- **Rule decision distribution by score** – The percentage of rule decisions in each score.
- **Rule Decision Rate** – The volume of transactions that were assessed by rules and the percentage of each type of rule decision in each score.
- **Transaction status by score** – The percentage of latest transaction statuses in each score.
- **Bank acceptance rate by score**

    - **Bank approved volume** – The bank-approved transactions in each score.
    - **Bank approved Rate** – The percentage of bank-approved transactions out of the total that were sent to the bank in each score.

### Time series view
When you select the Time series view, based on the filters you have selected, the following metrics are available.

- **Transaction Volume** – The transaction volume.
- **Fraud Rate**

    - **Fraud volume** – The transaction volume that's labeled as fraud.
    - **Fraud rate** – The percentage of fraud volume out of the total confirmed fraud and non-fraud transactions.

- **Rule Decision Distribution** – The rule decision percentage. (The rule decisions include **Approve**, **Reject**, **Review**, and **Challenge**.)
- **Transaction Status** – The percentage distribution of the latest status of transactions.
- **Rule Decision Rate** – The percentage distribution of rule decisions.
- **Bank Acceptance Volume and Rate** – The volume of bank-approved transactions, and the percentage of bank-approved transactions out of the total transactions that were sent to the bank.

### Table view
The statistical table view shows the following metrics for each score range, based on the selected filters:

- Transaction volume
- Reject rate
- Non-Fraud volume
- Fraud volume
- Fraud rate
- Send to bank volume
- Bank acceptance rate

## Operation analysis report
The **Operation analysis** report calculates statistics of score thresholds, based on the historical date. This information can help fraud control professionals understand the potential impact of the score threshold change and select score thresholds for their score rules.

- **Score distribution** – The percentage of volume at or above a score out of the total number of transactions. To further zoom in and out for your analysis, you can use the x-axis to adjust score ranges and the y-axis to adjust the percentage range.
- **Model Performance** – The receiver operating characteristic (ROC) curve, where the x-axis represents cumulative false positive rates and the y-axis represents cumulative true positive rates. You can adjust both the x-axis and the y-axis to further zoom in and out for your analysis.
- **Score Impact Analysis** – A statistical table view shows the following KPIs:

    - **Rejected Rate** – The percentage of rejected volume at or above a score, out of the total transaction volume.
    - **Detection Rate** – The percentage of fraud volume at or above a score, out of the total fraud volume.
    - **False Positive Rate** – The percentage of non-fraud volume at or above a score, out of the total non-fraud volume.
    - **Approved Fraud Rate** – The percentage of fraud volume under a score, out of the total fraud and non-fraud volumes under that score.
    - **Precision** – The percentage of fraud volume at or above a score, out of the total fraud and non-fraud volumes at or above a score.

- **Score Cutoff Simulation** – Given the input score cutoff, the following metrics are calculated:

    - Volume at or above the cutoff
    - Percentage at or above the cutoff
    - Fraud volume under the cutoff
    - Fraud rate under the cutoff
    - Time series chart of the volume under, at, or above the given score cutoff and the percentage at or above the cutoff
    - Time series chart of fraudulent transactions and fraud rate under the given cutoff

- **Profit Optimizer Simulation** – Given the estimated percentage of profit margin and score range (in increments of 10), the cumulative net profit and cumulative net profit achieved percentages are calculated.

    - **Net Profit** – The profit of non-fraud transactions minus the cost of goods of fraud transactions.
    - **Cumulative Net profits achieved percentage** – The percentage of net profit at or under a score bin out of the total possible non-fraud profit.
    - **Cumulative net profit** – The cumulative net profit from score 0 through 999.

## Filters
In addition to the common filters, the following filters are available for you to further analyze your data. You can select different filters and check the metrics for your analysis.

- **Score** – Use the text box or the scroll bar to select the desired score range. The score is aggregated in increments of 10. For the digit in the ones place, the lower bound is rounded down to 0 (zero), and the upper bound is rounded up to 9. For example, if you select a score from 35 through 64, the metrics and charts on the report show data that has a score range from 30 through 69.
- **Merchant Rule Decision** – The decisions that were made by Fraud Protection rules. The rule decisions include **Approve**, **Reject**, **Review**, and **Challenge**.
- **Merchant Final Decision** – The final decisions that were shared through the Fraud Protection status API.
- **Decision Rule/Clause** – The decision rule and clauses that were created through the Fraud Protection rule engine.
- **Transaction Status** – The latest status of transactions.

- **Score Type** – The available Fraud Protection score types.
