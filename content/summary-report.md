---
author: yvonnedeq
description: This article explains how to utilize the Summary report in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 04/10/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Summary report
ms.custom: bap-template
---

# Summary report

Fraud Protection provides a Summary report that's designed to show fraud KPI metrics. Use this report to find out the statistics of rule decision distributions, fraud rates, and available bank acceptance rates over time for reporting purposes. The following KPIs and time series metrics are included.

## KPIs
- **Transaction Volume** – The transaction volume, by count or amount, that was assessed by Fraud Protection.
- **Rule Approval Rate** – The percentage of assessed transactions by count or amount that was approved, based on the selected filters.
- **Manual Review Rate** – The percentage of assessed transactions by count or amount that was sent for review, based on the selected filters.
- **Rule Decision Rate** – The rule decision distribution, based on the selected filters.
- **Fraud Volume** – The confirmed fraudulent transactions by count or amount, based on the selected filters.
- **Fraud Rate** – The percentage of confirmed fraud volume out of the total confirmed fraud and non-fraud transactions, based on the selected filters.
- **Bank Acceptance Rate (When applies)** – The percentage of bank-approved transactions out of the total transactions that were sent to the bank, based on the selected filters.
- **Fraud chargeback rate** – The fraud chargeback rate by transaction date which is the percentage of fraud chargebacks out of the total volume that was settled by banks on the transaction date.

## Time series metrics
- **Transaction Volume** – The transaction volume, based on the selected filters.
- **Fraud Volume and Fraud Rate** – The fraudulent transaction volume and fraud rate, based on the selected filters.
- **Rule Decision Distribution** – The rule decision percentage, based on the selected filters. (The rule decisions include Approve, Reject, Review, and Challenge.)
- **Transaction Status** – The percentage distribution of the latest status of transactions, based on selected filters.
- **Rule Rejection Volume and Rate** – The volume of rejected transactions and the rejected rate.
- **Bank Acceptance Volume and Rate** – The volume of bank-approved transactions and the bank-approved rate.
- **Fraud chargeback volume and rate by transaction date** – The volume of fraud chargebacks and the percentage of fraud chargebacks out of the total volume that was settled by banks on the transaction date.
- **Fraud chargeback volume and rate by receive date** – The volume of fraud chargebacks based on the receive date, and the percentage of fraud chargebacks on the receive date out of the total fraud chargebacks on the receive date and total volume that was settled by banks on the same day.
