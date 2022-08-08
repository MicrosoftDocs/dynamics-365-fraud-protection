---
author: josaw1
description: This article provides information about the score rule optimizer tool in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 09/20/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Score rule optimizer tool 
---

# Score rule optimizer tool

The Microsoft Dynamics 365 Fraud Protection score rule optimizer tool lets merchants analyze historical transaction data and perform operational tasks. It also helps them make informed operational decisions, such as setting the score threshold, rejecting risky transactions, estimating score threshold impact, analyzing fraud trends and performance, and conducting deep-dive analyses.

The score rule optimizer is an interactive report tool that is built on the Power BI platform. Merchants can use it to drive purchase protection for customers in their online business by applying various filters, changing the score threshold, and viewing an analysis of purchase activity in various market segments.

The score rule optimizer report is updated with the latest transactional data every 24 hours. The time stamp on the report shows the update time in Coordinated Universal Time.

The score rule optimizer includes the following report tabs:

- **Profit optimizer** – This report finds the score threshold that will maximize net profit.
- **Model performance** – This report shows the receiver operating characteristic (ROC) curve for the model and other related information at each score bin.
- **Operation analysis** – This report shows a summary of operations and key metrics over time and also by score bin.
- **Score distribution** – This report shows the cumulative volume percentage to help merchants understand the volume impact by score bin.
- **Threshold controller** – This report shows the change in volume above a given score bin over time.

## Profit optimizer

To use the **Profit optimizer** report to help maximize your net profit, you can configure the filter to the required market and select the date range where the fraud label is matured. If a fraud label isn't fully matured (for example, a chargeback), a higher-than-optimal score threshold will be returned.

To find the optimal balance between rejecting fraud and reducing false positives, an important input to estimate is the profit margin that takes the fraud loss into account. For example, if the profit margin of the product is 20 percent, the loss that is produced by one fraudulent transaction balances out the profit that is brought in by four legitimate transactions. Transactions will be rejected when the fraud rate reaches about 20 percent. Fraud loss might go beyond the cost of the product. Therefore, an additional chargeback fee from banks or operation cost might occur. The fraudulent transactions rate will further influence the bank authorization rate in the future.

When you select the profit margin on this tab, you should consider the following points:

- The rejection score bin threshold value is the recommended score bin threshold that will maximize net profit. To get the score threshold, you can multiply the score bin threshold value by ten.
- The profit optimizer shows the impact of using the recommended score threshold. It includes the following information:

    - **Percentage of transactions blocked at the rejection threshold**
    - **False positive rate at the rejection threshold** – The percentage of non-fraud volume at and above a score bin, out of the total non-fraud volume.
    - **Approved transaction fraud rate at the rejection threshold** – The percentage of the fraud volume in the score bin against the total fraud and non-fraud volume of the score bin.

- The score bin table shows the net profits for each score bin. It includes the following information:

    - **Net profits achieved** – The percentage of net profit at and under a score bin, out of the total possible non-fraud profit.
    - **Net profit** – The profit of non-fraudulent transaction minus the cost of goods for fraudulent transactions.
    - **The cost of goods lost due to fraudulent transactions**

- The profit optimizer chart shows the net profit for each score bin and the cumulative net profit.
- The profit optimizer shows the optimal net profit at the recommended score bin threshold. In other words, it shows the maximum cumulative profit for the score bin. The optimal net profit that is achieved is the percentage of optimal net profits out of the total possible non-fraud profit when the transactions above the recommended score threshold are rejected.

The profit optimizer is evaluated only on transactions that have known fraud status. Transactions that were rejected by risk rules or declined by the bank are usually excluded, except under the following conditions:

- Fraud labels are explicitly provided to Fraud Protection.
- If the **Fraud to include merchant rejected** filter is set to **True**, the final rejected transactions are included as fraudulent transactions.

## Model performance

The **Model performance** report shows the ROC curve, which is a plot chart of false positive rates versus the detection rate at various threshold settings. (The false positive rate is the percentage of legitimate transactions that were incorrectly rejected against all the legitimate transactions that were accepted. The detection rate is the percentage of all fraudulent transactions that were caught versus all fraudulent transactions.) The larger the area under the curve, the more efficiently the model performs.

Only transactions that have known fraud status are included on the **Model performance** report. Transactions that were rejected by the merchant or declined by the bank are excluded, except under the following conditions:

- Fraud labels are explicitly provided to Fraud Protection.
- If the **Fraud to include merchant rejected** filter is set to **True**, the final rejected transactions are included as fraudulent transactions.

You can configure the setting for the measurement unit by count or by amount. You can also filter the fraud and non-fraud labels, and select at least one type of fraud and non-fraud transaction to analyze the results.

The table shows metrics for each of the following score bins:

- **Rejected rate** – The percentage of volume at and above a score bin, out of the total transaction volume.
- **False positive rate** – The percentage of non-fraud volume at and above a score bin, out of the total non-fraud volume.
- **Detection rate** – The percentage of fraud volume at and above a score bin, out of the total fraud volume.
- **Approved transaction fraud rate** – The percentage of fraud volume under a score bin, out of the total fraud and non-fraud volume under that score bin.
- **Transactional false positive ratio (TFPr)** – The ratio of non-fraud volume for each fraud volume at and above a score bin.

## Operation analysis

The **Operation analysis** report shows a summary of the operation, and charts, tables, and the time series of key metrics for the business's fraud protection system.

Summary metrics show the following information:

- **Transaction volume** – The total transaction volume that was sent to Fraud Protection.
- **Rejected rate\*** – The percentage of volume where the merchant's final decision was rejected and a decision wasn't made by the bank, out of the transaction volume.
- **Volume of transactions on which the bank has made a decision**
- **Bank declined rate** – The percentage of volume that the bank declined, out of the bank decision volume.
- **Settled volume\*** – The bank approval volume and volume that is labeled as fraud.
- **Fraud rate\*** – The percentage of fraud volume out of the total settled volume.

\* If the **Fraud to include merchant rejected** filter is set to **True**, the report will include the merchant's final rejected transactions as fraudulent activity.

You can change views by selecting **Charts**, **Table**, or **Time series**. You can also choose to aggregate daily, weekly, or monthly.

- **Charts** – This view shows the key metrics plotted per score bin.
- **Table** – This view shows the metrics by score bin in tabular format.
- **Time series** – This view shows the key metrics plotted over time.

The following key metrics are included on the **Operation analysis** report:

- **Transaction volume and final rejected rate**
- **Transaction volume sent to bank bank declined rate** – Usually, the higher the score, the higher the bank declined rate.
- **Settled volume\* and fraud rate\*** – Usually, the higher the score, the higher the fraud rate.
- **Fraud volume by identify category** – The total fraud volume, segmented by identify category.
- **Decisions and fraud signal distribution** – The total volume of transactions that weren't settled by a decision and the total volume of settled transactions\* by fraud signal.

\* If the **Fraud to include merchant rejected** filter is set to **True**, the report will include the merchant's final rejected transactions as fraudulent activity.

## Score distribution

The accumulated score distribution plot shows the percentage of transactions at or above each score bin, out of the total transaction volume.

## Threshold controller

The **Threshold controller** report can be used to simulate a rejection experiment. You can adjust the threshold by setting the **Score bin threshold controller** slider. The plots show the percentage and volume of transactions under or above the threshold. The information that is provided can help you understand the impact of adjusting the score bin threshold.

The following metrics are plotted on the report:

- **Volume under threshold** – The volume under a selected score bin threshold.
- **Volume at and above threshold** – The volume at and above a selected score bin threshold.
- **Percentage at and above threshold** – The percentage of volume at and above a selected score bin threshold, out of the total transaction volume.

## Appendix

The following filters are included on the reports:

- **Billing country/region**
- **User country/region**
- **PI type, card type** – This filter includes credit card and types of credit card as the sub-filter.
- **Product type, category, name** – You can filter at different levels of the product filter tree.
- **Score bin** – You can set upper and lower score bin limits by adjusting the slider or setting the field.
- **Date range** – You can set the date range by adjusting the slider or setting the date picker.
- **Label, fraud identifier** – You can filter by fraud label and non-fraud. The fraud label might include chargebacks, refunds, and other labels previously provided.
- **Measurement unit** – You can show the report by count or by amount.

### Hidden filter pane

The following filters are included in the filter pane on the right side of the page. The filter pane can be hidden as required.

- **Score bin** – You can filter by each score bin.
- **Assessment type** – You can filter by evaluate or protect.
- **Merchant final decision** – You can filter by merchant's decision provided in purchase status.
- **Bank decision** – You can filter by bank decision provided.
- **Settled flag** – You can indicate settled or non-settled transactions.
- **Policy applied** – You can filter by rule/policy triggered transactions.
- **Label** – You can add fraud or non-fraud labels.
- **Fraud identifier** – The fraud identifier includes chargeback, refund, purchase status, and non-fraud transactions.
- **Recurring flag** – This flag indicates whether transactions are recurrent.
- **Over zero-dollar flag** – This flag indicates whether the purchase amount is 0 (zero).
- **Fraud to include merchant rejected** – If this filter is set to **True**, merchant rejected transactions are included in the fraud volume.
