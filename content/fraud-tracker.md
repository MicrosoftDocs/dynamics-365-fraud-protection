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

- **Fraud by received date**: Dislays the monthly and weekly distribution report for confirmed fraud.

- **PI analysis**: Displays confirmed fraud distribution by payment instrument (PI) type\*. (Fraud distribution is confirmed by the user or bank.)

- **Product analysis**: Displays confirmed fraud distribution by product type, category, and name.

## Fraud Tracker

Fraud tracker provides a summary view of the fraud volume and fraud rate by payment instruments segment and product segment. It also provides the fraud volume and rate change over time and across an identified category. It allows you to quickly identify any patterns or trends for fraud in your online business.

The summary section displays the total transaction volume, fraud volume, label confirmed volume, and the fraud rate of the date range selected for the transaction date.

There are four charts that show different dimensions of the fraud:

- **List of fraud volume and rate by PI segment:** Shows confirmed fraud volume and fraud rate for transactions by PI type. Users can further drill down a PI type to view a breakdown by credit card type. The shaded bar indicates the volume for each PI type, and the color shade for the fraud rate indicates the percentage of the fraud. High fraud rates are highlighted in red.

- **List of fraud volume and rate by product segment:** Shows confirmed fraud volume and fraud rate for transactions by product type. Users can further drill down a product type to view product category breakdown or to drill down by product name. The shaded bar indicates the volume for each product type, and the color shade for the fraud rate indicates the percentage of the fraud. High fraud rates are highlighted in red.

- **Fraud volume and rate by transaction period:** Shows the fraud volume and fraud rate for transactions by transaction time. Users can change the aggregation level to daily, weekly, or monthly periods. The chart is a time-based distribution showing the total confirmed fraud volume and percentage of confirmed fraud volume and the total label confirmed volume by a transaction period. Users can identify spikes of fraud volume or gradual change of fraud rate trending in a certain direction over time.

- **Fraud volume by identify category:** Shows the fraud volume and fraud rate for transactions by identify category, for example, "CHARGEBACK," "PURCHASES STATUS REASON," and "REFUND." Users can change the aggregation level to daily, weekly or monthly periods. The chart is a time-based distribution showing total confirmed fraud volume broken down by the fraud identify category. Users can identify the fraud category with the most volume or with any change in the volume.

\*If the "Confirmed fraud type" filter includes the "MERCHANT TRUE REJECT" category, the merchant's final rejected transactions are included as fraudulent transactions.

## Fraud by received date

The **Fraud by received date** report is a powerful tool that helps users analyze fraud by the received date so they can act quickly on forecasted fraud increase.

The summary section shows total transaction volume, fraud volume, label confirmed volume, and the fraud rate of the date range selected for the fraud received date.

The **Fraud by received date** report has two levels: weekly and monthly. Users can switch between the two levels by clicking the **Tab** key.

There are four charts that show different dimensions of the fraud:

- **List of fraud volume and rate by PI segment:** Shows confirmed fraud volume and fraud rate for transactions by PI type. Users can further drill down a PI type to view a breakdown by credit card type. The shaded bar indicates the volume for each PI type and the color shade for the fraud rate indicates the percentage of the fraud. High fraud rates are highlighted in red.

- **List of fraud volume and rate by product segment:** Shows confirmed fraud volume and fraud rate for transactions by product type. Users can further drill down a product type to view product category breakdown or even drill down to product name. The shaded bar indicates the volume for each product type, and the color shade for the fraud rate indicates the percentage of the fraud. High fraud rates are highlighted in red.

- **Fraud volume and rate by fraud received week:** Shows the fraud volume and fraud rate for transactions by fraud received time. The chart is a time-based distribution showing total confirmed fraud volume and percentage of confirmed fraud volume out of total label confirmed volume by fraud received time. Users can change the fraud rate trending in a certain direction over time. This is particularly useful because the **fraud volume by received date** allows users to compare fraud volumes and rates over time without being impacted by more recent fraud.

- **Fraud volume by weeks/months from transaction date and rate of 00-02 weeks/0 months from transaction date:** Shows the total confirmed fraud volume by number of weeks/months between transaction date and fraud received date. It also shows the percentage of confirmed fraud volume out of label confirmed in the past 3 weeks or in the same month. The chart is a time-based distribution showing fraud volume by age (time from transaction date to received date) and fraud rate of the smallest age group. The age group is divided by 21 days (3 weeks) when viewing at weekly level, and within the same month, within 1 month, 2 months, etc., when viewing at a monthly level. The fraud age distribution is helpful to compare different fraud age groups and identify any recent changes in small groups. An increased volume or fraud rate for the smallest age group indicates more fraud will be received in the future, and users should adjust the score threshold accordingly.

## PI analysis

The **PI analysis** report shows fraud volume, fraud rate and fraud distribution by PI, as well the time-based fraud distribution and fraud rate charts.

The summary section shows total transaction volume, fraud volume, label confirmed volume, and the fraud rate of the date range selected for the transaction date.

PI analysis has two levels: PI type and Card type. Users can switch between the two levels by clicking the **Tab** key.

PI analysis is composed of three parts:

- **Summary table:** Shows the confirmed fraud volume, confirmed fraud rate, and the percentage of confirmed fraud distribution for each segment (PI type or Card Type). The shaded bar indicates the volume for each segment, and the color shade for the fraud rate indicates the percentage of the fraud. High fraud rates are highlighted in red.

- **Fraud distribution percentage by segment and fraud volume:** Shows the percentage of confirmed fraud distribution for each segment and the total confirmed fraud volume by transaction period. Users can identify the product segment with a large fraud distribution or identify change in fraud distribution over time.

- **Fraud rate by segment:** Shows the percentage of confirmed fraud volume versus the total label confirmed volume of each segment by transaction period. Users can identify the PI segment with a fraud rate spike or identify changes in fraud rate for a PI segment over time.

## Product analysis

The Product analysis report shows fraud volume, fraud rate and fraud distribution by product, as well the time-based fraud distribution and fraud rate charts.

The summary section shows total transaction volume, fraud volume, label confirmed volume, and fraud rate of the date range selected for the transaction date.

Product analysis has three levels: product type, product category, and product name. Users can switch between the three levels by clicking the **Tab** key.

Product analysis is composed of three parts:

- **Summary table:** Shows the confirmed fraud volume, confirmed fraud rate, and percentage of confirmed fraud distribution for each segment (product type, product category, or product name). The shaded bar indicates the volume for each segment, and the color shade for the fraud rate indicates the percentage of the fraud. High fraud rates are highlighted in red.

- **Fraud distribution percentage by segment and fraud volume:** Shows the percentage of confirmed fraud distribution for each segment and the total confirmed fraud volume by transaction period. Users can identify the product segment with a large fraud distribution or identify changes in fraud distribution over time.

- **Fraud rate by segment:** Shows the percentage of confirmed fraud volume versus the total label confirmed volume of each segment by transaction period. User can identify the product segment with a fraud rate spike or identify changes in fraud rate for a PI segment over time.

\*Evaluated only on transactions with confirmed fraud and non-fraud statuses, as confirmed by user/merchant.

## Appendix

The following filters are included in reports.

-   Billing country/region.

-   User country/region.

-   PI type, card type. This includes credit card and types of credit card as the sub-filter.

-   Product type, category, name. Merchants can filter at different levels of the product filter tree.

-   Date range. Merchants can use the slider or date picker to set the date range.

-   Label, fraud identifier. Merchants can filter by fraud label and non-fraud. The fraud label may include chargebacks, refunds, and other labels provided by the merchant.

-   Measurement unit. Merchants can show the report by count or amount.

### Hidden filter pane

-   Assessment type. Merchants can filter by evaluate or protect type.

-   Merchant final decision: Merchants can filter by the purchase status decision they provided.

-   Bank decision. Merchants can filter by the bank decision they provided.

-   Policy applied. Merchants can filter by rule/policy triggered transactions.

-   Recurring flag. This indicates if transactions are recurrent or not.

-   Over zero-dollar flag. This indicates if the purchase is not free.

-   Confirmed fraud type. The confirmed fraud type includes chargeback, refund, merchant true reject, and purchase status

-   Confirmed non-fraud type. The confirmed non-fraud type includes bank approved and merchant approved.
