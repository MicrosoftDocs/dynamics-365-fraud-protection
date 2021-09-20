---
author: josaw1
description: This topic provides information about the evaluate experience in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 09/20/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Score Rule Optimizer (Preview version)
---


# Score Rule Optimizer (Preview version)

The Fraud Protection score rule optimizer (Preview) tool is provided to you as a Preview service under terms and conditions described in the [Microsoft Online Service Terms](https://go.microsoft.com/fwlink/?linkid=2172945). The score rule optimizer is a tool that allows merchants to analyze historical transaction data, perform operational tasks, and make informed operational decisions such as setting the score threshold, rejecting risky transactions, estimating score threshold impact, analyzing fraud trends and performance, and conducting deep dive analysis.

The score rule optimizer is an interactive report tool built on the Microsoft Power BI platform. Merchants can use this tool to drive purchase protection for their customers in their online business by applying various filters, changing the score threshold, and viewing an analysis of purchase activity in various market segments.

The score rule optimizer report refreshes every 24 hours with the latest transactional data. The time stamp in the report displays the UTC refresh time for the report.

The score rule optimizer is composed of the following report tabs:

- **Profit optimizer**, which helps merchants find the score threshold that will maximize their net profit.

- **Model performance**, which shows the ROC curve for the model and other related information at each score bin.

- **Operation analysis**, which shows a summary of operations and key metrics over time as well as by score bin.

- **Score distribution**, which shows the cumulative volume percentage to help merchants understand the volume impact by score bin.

- **Threshold controller**, which shows the change of the volume above a given score bin over time.

## Profit optimizer

To use the profit optimizer and maximize their net profit, merchants can configure the filter to the required market and select the date range where the fraud label is matured. Note that if a fraud label (for example, *chargeback*) is not fully matured, a higher than optimal score threshold will be returned.

To find the optimal balance between rejecting fraud and reducing false positives, one important input to estimate is the profit margin with the consideration of the fraud loss. For example, if the profit margin of the product is 20%, the loss resulting from one fraudulent transaction balances out the profit brought in by four legitimate transactions. Transactions will start being rejected when the fraud rate reaches about 20%. Fraud loss may go beyond the cost of the product, causing additional chargeback fee from banks or operation cost. The fraudulent transactions rate will further influence the bank authorization rate in the future.

When selecting the profit margin in this tab, the following items should be considered.

-   The Rejection score bin threshold value is the recommended score bin threshold that will maximize net profit. To get the score threshold, merchants can multiply the score bin threshold value by ten.

-   The Profit optimizer shows the impact of using the recommended score threshold. This includes:

<!-- -->

-   The percentage of transactions blocked at the rejection threshold.

-   The false positive rate at the rejection threshold. This is the percentage of non-fraud volume at and above a score bin out of total non-fraud volume

-   The approved transaction fraud rate at the rejection threshold. This is the percentage of the fraud volume in the score bin against the total fraud and non-fraud volume of the score bin.

<!-- -->

-   The score bin table shows the net profits for each score bin. This includes:

<!-- -->

-   The net profits achieved. This is the percentage of net profit at and under a score bin out of the total possible non-fraud profit.

-   The net profit. This is the profit of non-fraudulent transaction minus the cost of goods for fraudulent transactions.

-   The cost of goods lost due to fraudulent transactions.

<!-- -->

-   The profit optimizer chart shows the net profit for each score bin and the cumulative net profit.

-   The profit optimizer shows the optimal net profit at the recommended score bin threshold, that is, the maximum cumulative profit for the score bin. The optimal net profit achieved is the percentage of optimal net profits out of total possible non-fraud profit by rejecting the transactions above the recommended score threshold.

Note that the optimizer is evaluated only on transactions with a known fraud status. Transactions rejected by risk rules or declined by the bank are usually not included except under these conditions:

-   Fraud labels are explicitly provided by the merchant.

-   If the Fraud to include merchant rejected filter is set to True, the merchant's final rejected transactions are included as fraudulent transactions.

## Model performance

The Model performance tab shows the ROC (receiver operating characteristic) curve, which is a plot graph of false positive rates (the percentage of legitimate transactions wrongly rejected against all the legitimate transactions accepted) *vs*. the detection rate (the percentage of all fraudulent transactions caught vs. all fraudulent transactions) at various threshold settings. The bigger the area under the curve, the more efficiently the model performs.

Note that only transactions with a known fraud/non-fraud status are included on this page. This means that all transactions rejected by the merchant or declined by the bank are generally excluded unless an explicit fraud or non-fraud label was sent to Fraud Protection. If a merchant wants to include merchant rejected transactions as fraud in the evaluation, they can set the option in the **Filters** tab on the right pane.

Merchants can configure the setting for the measurement unit by count or by amount. They can also filter the fraud and non-fraud labels and select at least one type of fraud and non-fraud transaction to analyze the results.

The table shows metrics for each of the following score bins:

-   Rejected rate. This is the percentage of volume at and above a score bin out of the total transaction volume.

-   False positive rate. This is the percentage of non-fraud volume at and above a score bin out of the total non-fraud volume.

-   Detection rate. This is the percentage of fraud volume at and above a score bin out of the total fraud volume.

-   Approved transaction fraud rate. This is the percentage of fraud volume under a score bin out of the total fraud and non-fraud volume under that score bin.

-   TFPr (transactional false positive ratio). This is the ratio of non-fraud volume for each fraud volume at and above a score bin.

## Operation analysis

The operation analysis report shows a summary of the operation as well as charts, tables, and the time series of key metrics for the business's fraud protection system.

Summary metrics show the following information:

-   Transaction volume. This is the total transaction volume sent to Fraud Protection.

-   Rejected rate. This is the percentage of volume that the merchant's final decision is rejected, and a decision is not made by the bank out of the transaction volume.

-   Volume of transactions on which the bank has made a decision.

-   Bank declined rate. This is the percentage of volume that bank declined out of bank decisioned volume.

-   Settled volume. This is the bank approval volume and volume labeled as fraud. \*\*

-   Fraud rate. This is the percentage of fraud volume out of total settled volume. \*\*

\*\* If the**Fraud to include merchant rejected** filter is set to *True*, the merchant's final rejected transactions will be included in the report as fraudulent activity.

Merchants can change views by selecting **Charts**, **Table** or **Time series**. They can also choose to aggregate daily, weekly, or monthly.

- **Charts** show key metrics plotted per score bin.

- **Table** shows the metrics by score bin in tabular format.

- **Time series** show the key metrics plotted over time.

The following key metrics are included in the operation analysis report:

-   Transaction volume and final rejected rate.

-   Transaction volume sent to the bank and the bank declined rate. Note that, usually, the higher the score, the higher the bank declined rate.

-   Settled volume\*\* and fraud rate\*\*. This is usually the higher the score, the higher the fraud rate.

-   Fraud volume by identify category. This is the total fraud volume segmented by identify category.

-   Decisions and fraud signal distribution. This is the total volume of transactions not settled by decision and the total volume of settled transactions\*\* by fraud signal.

## Score distribution

The accumulated score distribution plot illustrates the percentage of transactions at or above each score bin out of the total transaction volume.

## Threshold controller

The threshold controller tool is used to simulate a rejection experiment. Adjust the threshold by adjusting **Score bin threshold controller** slider. The plots show the percentage and volume of transactions under or above the threshold. This information is helpful to understand the impact of adjusting the score bin threshold.

The following metrics are plotted in the report:

-   Volume under threshold. This is the volume under a selected score bin threshold.

-   Volume at and above threshold. This is the volume at and above a selected score bin threshold.

-   Percentage at and above threshold. This is the percentage of volume at and above a selected score bin threshold out of total transaction volume.

## Appendix

The following filters are included in reports.

-   Billing country/region.

-   User country/region.

-   PI type, card type. This includes credit card and types of credit card as the sub-filter.

-   Product type, category, name. Merchants can filter at different levels of the product filter tree.

-   Score bin. Merchants can use the slider or input box to set upper and lower score bin limits.

-   Date range. Merchants can use the slider or date picker to set the date range.

-   Label, fraud identifier. Merchants can filter by fraud label and non-fraud. The fraud label may include chargebacks, refunds, and other labels provided by the merchant.

-   Measurement unit. Merchants can show the report by count or amount.

### Hidden filter pane

-   Score bin. Merchants can filter by each score bin.

-   Assessment type. Merchants can filter by evaluate or protect.

-   Merchant final decision: filter by merchant's decision provided in purchase status

-   Bank decision. Merchants can filter by bank decision provided.

-   Settled flag. Merchants can indicate settled or non-settled transactions.

-   Policy applied. Merchants can filter by rule/policy triggered transactions.

-   Label. Merchants can add fraud or non-fraud labels.

-   Fraud identifier. The fraud identifier includes chargeback, refund, purchaseStatus, and non-fraud transactions.

-   Recurring flag. This indicates if transactions are recurrent or not.

-   Over zero-dollar flag. This indicates if the purchase amount is zero.

-   Fraud to include merchant rejected. If set to True, then merchant rejected transactions are included in the fraud volume.
