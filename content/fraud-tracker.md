---
author: josaw1
description: This topic provides information about the fraud tracker tool in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 09/20/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Fraud tracker tool (preview version)
---


# Fraud tracker tool (preview version)

The Dynamics 365 Fraud Protection fraud tracker tool (preview) is provided as a preview service under the terms and conditions described in the [Microsoft Online Service Terms](https://go.microsoft.com/fwlink/?linkid=2172945). The fraud tracker helps merchants with: understanding fraud volume (by count and dollar amount), distribution, and trend; analyzing by payment instrument and product; and making informed operational decisions such as adjusting the score threshold for a certain transaction segment.

The fraud tracker is an interactive report tool built on the Microsoft Power BI platform. Merchants can use this tool to drive purchase protection for their customers in their online business by applying various filters, changing the granularity of the dimension, and viewing an analysis of fraud volume and rate in various market segments.

The fraud tracker report refreshes every 24 hours with the latest transactional data. The time stamp in the report displays the UTC refresh time for the report.

The fraud tracker includes the following report tabs.

- **Fraud tracker**: Provides an overview of the fraud volume and rate across segments.

- **Fraud by received date**: Displays the monthly and weekly distribution report for confirmed fraud.

- **PI analysis**: Displays confirmed fraud distribution by payment instrument (PI) type\*. (Fraud distribution is confirmed by the user or bank.)

- **Product analysis**: Displays confirmed fraud distribution by product type, category, and name.

\*If the **Confirmed fraud type** filter includes the **Merchant true reject** category, the merchant's final rejected transactions are included as fraudulent transactions.

## Fraud Tracker

Fraud tracker provides a summary view of the fraud volume and fraud rate by payment instruments segment and product segment. It also provides the fraud volume and rate change over time and across an identified category. It allows you to quickly identify any fraud patterns or trends in your online business.

The summary section displays the total transaction volume, fraud volume, label confirmed volume, and the fraud rate of the date range selected for the transaction date.

There are four charts that show different dimensions of the fraud.

- **List of fraud volume and rate by PI segment:** Displays confirmed fraud volume and fraud rate for transactions by PI type. You can drill down on a PI type to view a breakdown by credit card type. The shaded bar indicates the volume for each PI type, and the color shade for the fraud rate indicates the percentage of the fraud. High fraud rates are highlighted in red.

- **List of fraud volume and rate by product segment:** Displays confirmed fraud volume and fraud rate for transactions by product type. You can drill down on a product type to view breakdown by product category or to drill down by product name. The shaded bar indicates the volume for each product type, and the color shade for the fraud rate indicates the percentage of the fraud. High fraud rates are highlighted in red.

- **Fraud volume and rate by transaction period:** Displays the fraud volume and fraud rate for transactions by transaction time. You can change the aggregation level to daily, weekly, or monthly periods. The chart is a time-based distribution that displays the total confirmed fraud volume and percentage of confirmed fraud volume and the total label confirmed volume by a transaction period. Users can identify spikes in fraud volume or gradual change of fraud rate trending in a certain direction over time.

- **Fraud volume by identify category:** Displays the fraud volume and fraud rate for transactions by identify category (for example, **Chargeback**, **Purchases status reason**, and **Refund**). You can change the aggregation level to daily, weekly, or monthly periods. The chart is a time-based distribution that displays total confirmed fraud volume broken down by the fraud identify category. You can identify the fraud category with the most volume or with any change in the volume.


## Fraud by received date

The fraud by received date report helps you analyze fraud by the received date, so you can act quickly on forecasted fraud increase.

The summary section shows total transaction volume, fraud volume, label confirmed volume, and the fraud rate for the date range selected for the fraud received date.

The fraud by received date report has two levels, weekly and monthly. You can switch between the two levels by pressing the **Tab** key.

There are four charts that show different dimensions of the fraud:

- **List of fraud volume and rate by PI segment:** Displays confirmed fraud volume and fraud rate for transactions by PI type. You can drill down on a PI type to display a breakdown by credit card type. The shaded bar indicates the volume for each PI type and the color shade for the fraud rate indicates the percentage of the fraud. High fraud rates are highlighted in red.

- **List of fraud volume and rate by product segment:** Displays confirmed fraud volume and fraud rate for transactions by product type. You can drill down on a product type to display breakdown by product category or drill down on product name. The shaded bar indicates the volume for each product type, and the color shade for the fraud rate indicates the percentage of the fraud. High fraud rates are highlighted in red.

- **Fraud volume and rate by fraud received week:** Displays the fraud volume and fraud rate for transactions by fraud received time. The chart is a time-based distribution that displays total confirmed fraud volume and percentage of confirmed fraud volume out of total label confirmed volume by fraud received time. You can change the fraud rate trending in a certain direction over time. This is useful because **Fraud volume by received date** allows you to compare fraud volumes and rates over time without being impacted by more recent fraud.

- **Fraud volume by weeks/months from transaction date and rate of 00-02 weeks/0 months from transaction date:** Displays the total confirmed fraud volume by number of weeks/months between transaction date and fraud received date. It also displays the percentage of confirmed fraud volume out of label confirmed in the past 3 weeks or in the same month. The chart is a time-based distribution that displays fraud volume by age (time from transaction date to received date) and fraud rate of the smallest age group. The age group is divided by 21 days (3 weeks) when displaying at weekly level, and within the same month, within 1 month, 2 months, etc., when displaying at a monthly level. The fraud age distribution is helpful if you want to compare different fraud age groups and identify any recent changes in small groups. An increased volume or fraud rate for the smallest age group indicates more fraud will be received in the future, and you should adjust the score threshold accordingly.

## PI analysis

The PI analysis report displays fraud volume, fraud rate, and fraud distribution by PI, and the time-based fraud distribution and fraud rate charts.

The summary section displays total transaction volume, fraud volume, label confirmed volume, and the fraud rate of the date range selected for the transaction date.

PI analysis has two levels, PI type and card type. You can switch between the levels by pressing the **Tab** key.

PI analysis is composed of three parts:

- **Summary table:** Displays the confirmed fraud volume, confirmed fraud rate, and the percentage of confirmed fraud distribution for each segment (PI type or card type). The shaded bar indicates the volume for each segment, and the color shade for the fraud rate indicates the percentage of the fraud. High fraud rates are highlighted in red.

- **Fraud distribution percentage by segment and fraud volume:** Displays the percentage of confirmed fraud distribution for each segment and the total confirmed fraud volume by transaction period. You can identify the product segment with a large fraud distribution or identify change in fraud distribution over time.

- **Fraud rate by segment:** Displays the percentage of confirmed fraud volume versus the total label confirmed volume of each segment by transaction period. You can identify the PI segment with a fraud rate spike or identify changes in fraud rate for a PI segment over time.

## Product analysis

The product analysis report shows fraud volume, fraud rate, and fraud distribution by product, and the time-based fraud distribution and fraud rate charts.

The summary section displays total transaction volume, fraud volume, label confirmed volume, and fraud rate of the date range selected for the transaction date.

Product analysis has three levels; product type, product category, and product name. You can switch between the levels by pressing the **Tab** key.

Product analysis consists of three parts:

- **Summary table:** Displays the confirmed fraud volume, confirmed fraud rate, and percentage of confirmed fraud distribution for each segment (product type, product category, or product name). The shaded bar indicates the volume for each segment, and the color shade for the fraud rate indicates the percentage of the fraud. High fraud rates are highlighted in red.

- **Fraud distribution percentage by segment and fraud volume:** Displays the percentage of confirmed fraud distribution for each segment and the total confirmed fraud volume by transaction period. You can identify the product segment with a large fraud distribution or identify changes in fraud distribution over time.

- **Fraud rate by segment:** Displays the percentage of confirmed fraud volume versus the total label confirmed volume of each segment by transaction period. You can identify the product segment with a fraud rate spike or identify changes in fraud rate for a PI segment over time.

<!-- I don't know what this applies to. \*Evaluated only on transactions with confirmed fraud and non-fraud statuses, as confirmed by user/merchant. -->

## Appendix

The following filters are included in reports.

- **Billing country/region**.

- **User country/region**.

- **PI type, card type**: Includes sub-filter for credit card and types of credit card.

- **Product type, category, name**: Filter at different levels of the product filter tree.

- **Date range**: Adjust the slider or date picker to set the date range.

- **Label, fraud identifier**: Filter by fraud label and non-fraud. The fraud label may include chargebacks, refunds, and other labels previously provided.

- **Measurement unit**: Display the report by count or amount.

### Hidden filter pane

The following filters are included in the filter pane on the right side of the screen. The filter pane can be hidden if necessary.

- **Assessment type**: Filter by evaluate or protect type.

- **Merchant final decision**: Filter by the purchase status decision previously provided.

- **Bank decision**: Filter by the bank decision provided.

- **Policy applied**:  Filter by rule/policy triggered transactions.

- **Recurring flag**: Indicates whether transactions are recurrent.

- **Over zero-dollar flag**: Indicates if the purchase is not free.

- **Confirmed fraud type**: Includes chargeback, refund, merchant true reject, and purchase status.

- **Confirmed non-fraud type**: Includes bank approved and merchant approved.
