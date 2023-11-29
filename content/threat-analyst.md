---
author: yvonnedeq
description: This article explains how to utilize the Threat report in Microsoft Dynamics 365 Fraud Protection.
ms.author: kfend
ms.date: 02/08/2023
ms.topic: conceptual
search.audienceType:
  - admin
title: Threat report
ms.custom: bap-template
---

# Threat report

Fraud Protection provides Threat report that is designed to show fraud insights into entities such as payment card type. You can use these reports to find distribution changes and identify anomalies on the entities. You can also use them to further optimize rules.

## Fraud views
Based on the filters you have selected, the following metrics are available for analysis.

- **Transaction Volume** – The amount of transactions that were assessed by Fraud Protection.
- **Fraud Volume** – The number of confirmed fraudulent transactions.
- **Fraud rate** – The percentage of confirmed fraud transactions.

### Time series view 
Based on the filters you have selected, the following metrics are available for analysis.

- **Transaction Volume** – The transaction volume that was assessed by Fraud Protection.
- **Fraud Rate by transaction date** – An aggregation of the fraud volume and fraud rate by the original transaction date.
- **Fraud Rate by fraud received date** – An aggregation of the fraud volume and fraud rate by the date when the fraud signal was received.
- **Fraud by transaction status(when applies)** – The transaction status distribution of confirmed fraudulent transactions. This information can provide insights into fraud reasons.
- **Fraudflag distribution from latest label or observation event(when applies)** – the percentage distribution of the fraudflag values from the latest label or observation event.  

### Entity distribution views
The available entities vary, depending on the capability. The following lists show the entities that are available for each capability.

#### Purchase Protection

- Merchant Business Segment
- Merchant Product Category
- PI Type – Payment instrument type
- PI Card Type – Payment instrument card type
- IP Country/State - country and state based on IP address

#### Account Protection
- Enabled JS –JavaScript enablement status
- Operating System Family
- Operating System
- Browser Family
- IP Country/State - Country and state based on IP address

#### Assessments
- After an assessment is created, you have the option to set up your own data filters/entities. More information on this can be found in the article of [Configure an existing assessment](assessment-configure-existing.md).

### Time series view
The following metrics are available in the **Time series** view:

- **Entity Distribution by transaction volume** – The value distribution of the assessed transactions on the selected entity.
- **Entity Distribution by fraud volume** – The value distribution of the fraud volume on the selected entity.

### Table view
The following metrics are available in the **Table** view.

- **Entity Distribution by transaction volume** – The assessed transaction volume and value distribution of the transactions on the selected entity during the specified date range.
- **Entity Distribution by fraud volume** – The confirmed fraud volume and value distribution of the fraud volume on the selected entity during the specified date range.

## Filters
In addition to the common filters, the following filters are available for you to further analyze your data. You can select different filters and check the metrics for your analysis.

- **Score** – Use the text box or the scroll bar to select the desired score range. The score is aggregated in increments of 10. for the digit in the ones place, the lower bound is rounded down to 0 (zero), and the upper bound is rounded up to 9. For example, if you select score from 35 through 64, the metrics and charts on the report show data that has a score range from 30 through 69.
- **Merchant rule decision** – The decisions that were made by Fraud Protection rules. The rule decisions include **Approve**, **Reject**, **Review**, and **Challenge**.
- **Merchant final decision** – The final decisions that were shared through the Fraud Protection status API.
- **Decision rule/clause** – The decision rule and clauses that were created through the Fraud Protection rule engine.
- **Score type** – The available Fraud Protection score types.
- **Transaction status(when applies)** – The latest status of transactions.
- **Latest event, status (when applies)** – the status of transactions from the latest label or observation event.  
- **Latest fraud event (When applies)** – the fraudflag value from the latest label or observation event.
