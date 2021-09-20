---
author: josaw1
description: This topic provides information about the score rule optimizer tool in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 09/20/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Score rule optimizer tool (preview)
---


# Score rule optimizer tool (preview)

The Dynamics 365 Fraud Protection score rule optimizer tool (preview) is provided to you as a preview service under terms and conditions described in the [Microsoft Online Service Terms](https://go.microsoft.com/fwlink/?linkid=2172945). The score rule optimizer is a tool that allows merchants to analyze historical transaction data, perform operational tasks, and make informed operational decisions such as setting the score threshold, rejecting risky transactions, estimating score threshold impact, analyzing fraud trends and performance, and conducting deep dive analyses.

The score rule optimizer is an interactive report tool built on the Microsoft Power BI platform. Merchants can use this tool to drive purchase protection for their customers in their online business by applying various filters, changing the score threshold, and viewing an analysis of purchase activity in various market segments.

The score rule optimizer report refreshes every 24 hours with the latest transactional data. The time stamp in the report displays the UTC refresh time for the report.

The score rule optimizer includes the following report tabs.

- **Profit optimizer**: Finds the score threshold that will maximize net profit.

- **Model performance**: Displays the receiver operating characteristic (ROC) curve for the model and other related information at each score bin.

- **Operation analysis**: Displays the summary of operations and key metrics over time as well as by score bin.

- **Score distribution**: Displays the cumulative volume percentage to help merchants understand the volume impact by score bin.

- **Threshold controller**: Displays the change of the volume above a given score bin over time.

## Profit optimizer

To use the profit optimizer to help maximize your net profit, you can configure the filter to the required market and select the date range where the fraud label is matured. If a fraud label is not fully matured (for example, a chargeback), a higher than optimal score threshold will be returned.

To find the optimal balance between rejecting fraud and reducing false positives, an important input to estimate is the profit margin with the consideration of the fraud loss. For example, if the profit margin of the product is 20%, the loss resulting from one fraudulent transaction balances out the profit brought in by four legitimate transactions. Transactions will be rejected when the fraud rate reaches about 20%. Fraud loss may go beyond the cost of the product, causing additional chargeback fee from banks or operation cost. The fraudulent transactions rate will further influence the bank authorization rate in the future.

When selecting the profit margin in this tab, the following items should be considered.

- The rejection score bin threshold value is the recommended score bin threshold that will maximize net profit. To get the score threshold, you can multiply the score bin threshold value by ten.

- The profit optimizer displays the impact of using the recommended score threshold, including:

  - Percentage of transactions blocked at the rejection threshold.

  - False positive rate at the rejection threshold. Displays the percentage of non-fraud volume at and above a score bin out of total non-fraud volume.

  - Approved transaction fraud rate at the rejection threshold. Displays the percentage of the fraud volume in the score bin against the total fraud and non-fraud volume of the score bin.

- The score bin table displays the net profits for each score bin, including:

  - Net profits achieved. The percentage of net profit at and under a score bin out of the total possible non-fraud profit.

  - Net profit. The profit of non-fraudulent transaction minus the cost of goods for fraudulent transactions.

  - The cost of goods lost due to fraudulent transactions.

- The profit optimizer chart displays the net profit for each score bin and the cumulative net profit.

- The profit optimizer displays the optimal net profit at the recommended score bin threshold. In other words, it displays the maximum cumulative profit for the score bin. The optimal net profit achieved is the percentage of optimal net profits out of total possible non-fraud profit by rejecting the transactions above the recommended score threshold.

The profit optimizer is evaluated only on transactions with known fraud status. Transactions rejected by risk rules or declined by the bank are usually not included, except under the following conditions:

- Fraud labels are explicitly provided to Fraud Protection.

- If the **Fraud to include merchant rejected** filter is set to **True**, the final rejected transactions are included as fraudulent transactions.

## Model performance

The model performance tab displays the ROC curve, which is a plot graph of false positive rates (the percentage of legitimate transactions wrongly rejected against all the legitimate transactions accepted) versus the detection rate (the percentage of all fraudulent transactions caught versus all fraudulent transactions) at various threshold settings. The bigger the area under the curve, the more efficiently the model performs.

The only transactions included on the model performance page are those with known fraud status. Transactions rejected by the merchant or declined by the bank are not included, except under the following conditions:

- Fraud labels are explicitly provided to Fraud Protection.

- If the **Fraud to include merchant rejected** filter is set to **True**, the final rejected transactions are included as fraudulent transactions.

You can configure the setting for the measurement unit by count or by amount. You can also filter the fraud and non-fraud labels and select at least one type of fraud and non-fraud transaction to analyze the results.

The table displays metrics for each of the following score bins:

- Rejected rate. Percentage of volume at and above a score bin out of the total transaction volume.

- False positive rate. Percentage of non-fraud volume at and above a score bin out of the total non-fraud volume.

- Detection rate. Percentage of fraud volume at and above a score bin out of the total fraud volume.

- Approved transaction fraud rate. Percentage of fraud volume under a score bin out of the total fraud and non-fraud volume under that score bin.

- TFPr (transactional false positive ratio). The ratio of non-fraud volume for each fraud volume at and above a score bin.

## Operation analysis

The operation analysis report displays a summary of the operation, and charts, tables, and the time series of key metrics for the business' fraud protection system.

Summary metrics display the following information:

- Transaction volume. Total transaction volume sent to Fraud Protection.

- Rejected rate*. Percentage of volume that the merchant's final decision is rejected, and a decision is not made by the bank out of the transaction volume.

- Volume of transactions on which the bank has made a decision.

- Bank declined rate. Percentage of volume that bank declined out of bank decisioned volume.

- Settled volume. Bank approval volume and volume labeled as fraud.\*

- Fraud rate. Percentage of fraud volume out of total settled volume.\*

\* If the **Fraud to include merchant rejected** filter is set to **True**, the merchant's final rejected transactions will be included in the report as fraudulent activity.

You can change views by selecting **Charts**, **Table**, or **Time series**. You can also choose to aggregate daily, weekly, or monthly.

- **Charts**: Displays key metrics plotted per score bin.

- **Table**: Displays the metrics by score bin in tabular format.

- **Time series**: Displays the key metrics plotted over time.

The following key metrics are included in the operation analysis report:

- Transaction volume and final rejected rate.

- Transaction volume sent to bank bank declined rate. Usually, the higher the score, the higher the bank declined rate.

- Settled volume\* and fraud rate\*. Usually, the higher the score, the higher the fraud rate.

- Fraud volume by identify category. Total fraud volume segmented by identify category.

-  Decisions and fraud signal distribution. Total volume of transactions not settled by decision and the total volume of settled transactions\* by fraud signal.

\* If the **Fraud to include merchant rejected** filter is set to **True**, the merchant's final rejected transactions will be included in the report as fraudulent activity.

## Score distribution

The accumulated score distribution plot illustrates the percentage of transactions at or above each score bin out of the total transaction volume.

## Threshold controller

The threshold controller tool can be used to simulate a rejection experiment. You can adjust the threshold by setting the **Score bin threshold controller** slider. The plots display the percentage and volume of transactions under or above the threshold. The information provided is helpful to understand the impact of adjusting the score bin threshold.

The following metrics are plotted in the report:

- Volume under threshold. Volume under a selected score bin threshold.

- Volume at and above threshold*. Volume at and above a selected score bin threshold.

- Percentage at and above threshold. Percentage of volume at and above a selected score bin threshold out of total transaction volume.

## Appendix

The following filters are included in the reports.

- **Billing country/region**.

- **User country/region**.

- **PI type, card type**: This filter includes credit card and types of credit card as the sub-filter.

- **Product type, category, name**: You can filter at different levels of the product filter tree.

- **Score bin**: You can use the slider or input box to set upper and lower score bin limits.

- **Date range**: You can use the slider or date picker to set the date range.

- **Label, fraud identifier**: You can filter by fraud label and non-fraud. The fraud label may include chargebacks, refunds, and other labels previously provided.

- **Measurement unit**: You can display the report by count or amount.

### Hidden filter pane

The following filters are included in the filter pane on the right side of the screen. The filter pane can be hidden if necessary.

- **Score bin**: You can filter by each score bin.

- **Assessment type**: You can filter by evaluate or protect.

- **Merchant final decision**: Filter by merchant's decision provided in purchase status.

- **Bank decision**: You can filter by bank decision provided.

- **Settled flag**: You can indicate settled or non-settled transactions.

- **Policy applied**: You can filter by rule/policy triggered transactions.

- **Label**: You can add fraud or non-fraud labels.

- **Fraud identifier**: The fraud identifier includes chargeback, refund, purchase status, and non-fraud transactions.

- **Recurring flag**: Indicates whether transactions are recurrent.

- **Over zero-dollar flag**: Indicates if the purchase amount is zero.

- **Fraud to include merchant rejected**: If set to **True**, merchant rejected transactions are included in the fraud volume.
