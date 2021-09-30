---
author: josaw1
description: This topic provides information about the fraud tracker tool (preview) in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 09/30/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Fraud tracker tool (preview)
---

# Fraud tracker tool (preview)

[!include [preview banner](includes/preview-banner.md)]

The Microsoft Dynamics 365 Fraud Protection fraud tracker tool (preview) is provided as a preview service under the terms and conditions that are described in the [Microsoft Online Service Terms](https://go.microsoft.com/fwlink/?linkid=2172945). It helps merchants understand fraud volume (by count and dollar amount), distribution, and trend, and lets them do analysis by payment instrument and product. It also helps them make informed operational decisions, such as adjusting the score threshold for a specific transaction segment.

The fraud tracker is an interactive report tool that is built on the Power BI platform. Merchants can use it to drive purchase protection for customers in their online business by applying various filters, changing the granularity of the dimension, and viewing an analysis of fraud volume and rate in various market segments.

The fraud tracker report is updated with the latest transactional data every 24 hours. The time stamp on the report shows the update time in Coordinated Universal Time.

The fraud tracker includes the following report tabs:

- **Fraud tracker** – This report shows an overview of fraud volume and rate across segments.
- **Fraud by received date** – This report shows the monthly and weekly distribution report for confirmed fraud.
- **PI analysis** – This report shows the confirmed fraud distribution by payment instrument (PI) type\*. (Fraud distribution is confirmed by the user or bank.)
- **Product analysis** – This report shows the confirmed fraud distribution by product type, category, and name.

\* If the **Confirmed fraud type** filter includes the **Merchant true reject** category, the merchant's final rejected transactions are included as fraudulent transactions.

## Fraud tracker

The **Fraud tracker** report provides a summary view of the fraud volume and fraud rate by payment instruments segment and product segment. It also shows the fraud volume and rate change over time and across an identified category. It lets you quickly identify any fraud patterns or trends in your online business.

The summary section shows the total transaction volume, fraud volume, label confirmed volume, and fraud rate of the date range that is selected for the transaction date.

There are four charts that show different dimensions of the fraud:

- **List of fraud volume and rate by PI segment** – This chart shows the confirmed fraud volume and fraud rate for transactions by PI type. By drilling down on a PI type, you can view a breakdown by credit card type. The shaded bar indicates the volume for each PI type, and the color shade for the fraud rate indicates the percentage of the fraud. High fraud rates are highlighted in red.
- **List of fraud volume and rate by product segment** – This chart shows the confirmed fraud volume and fraud rate for transactions by product type. By drilling down on a product type, you can view a breakdown by product category or drill down on a product name. The shaded bar indicates the volume for each product type, and the color shade for the fraud rate indicates the percentage of the fraud. High fraud rates are highlighted in red.
- **Fraud volume and rate by transaction period** – This chart shows the fraud volume and fraud rate for transactions by transaction time. You can change the aggregation level to daily, weekly, or monthly periods. The chart is a time-based distribution that shows the total confirmed fraud volume, percentage of confirmed fraud volume, and total label confirmed volume by transaction period. You can identify spikes in fraud volume or gradual changes in fraud rate that trend in a specific direction over time.
- **Fraud volume by identify category** – This chart shows the fraud volume and fraud rate for transactions by identify category (for example, **Chargeback**, **Purchases status reason**, or **Refund**). You can change the aggregation level to daily, weekly, or monthly periods. The chart is a time-based distribution where the total confirmed fraud volume is broken down by fraud identify category. You can identify the fraud category that has the largest volume or that has any change in the volume.

## Fraud by received date

The **Fraud by received date** report helps you analyze fraud by the received date. Therefore, you can act quickly on forecasted fraud increases.

The summary section shows the total transaction volume, fraud volume, label confirmed volume, and fraud rate for the date range that is selected for the fraud received date.

The **Fraud by received date** report has two levels: weekly and monthly. You can switch between the two levels by selecting the **Tab** key.

There are four charts that show different dimensions of the fraud:

- **List of fraud volume and rate by PI segment** – This chart shows the confirmed fraud volume and fraud rate for transactions by PI type. By drilling down on a PI type, you can view a breakdown by credit card type. The shaded bar indicates the volume for each PI type, and the color shade for the fraud rate indicates the percentage of the fraud. High fraud rates are highlighted in red.
- **List of fraud volume and rate by product segment** – This chart shows the confirmed fraud volume and fraud rate for transactions by product type. By drilling down on a product type, you can view a breakdown by product category or drill down on a product name. The shaded bar indicates the volume for each product type, and the color shade for the fraud rate indicates the percentage of the fraud. High fraud rates are highlighted in red.
- **Fraud volume and rate by fraud received week** – This chart shows the fraud volume and fraud rate for transactions by fraud received time. The chart is a time-based distribution that shows the total confirmed fraud volume and percentage of confirmed fraud volume out of the total label confirmed volume by fraud received time. You can change the fraud rate that is trending in a specific direction over time. This functionality is useful because **Fraud volume by received date** lets you compare fraud volumes and rates over time, without being affected by more recent fraud.
- **Fraud volume by weeks/months from transaction date and rate of 00-02 weeks/0 months from transaction date** – This chart shows the total confirmed fraud volume by number of weeks/months between the transaction date and the fraud received date. It also shows the percentage of the confirmed fraud volume out of the label confirmed volume during the past three weeks or during the same month. The chart is a time-based distribution that shows the fraud volume by age (time from the transaction date to the received date) and fraud rate of the smallest age group. When the report is at the weekly level, the age group is divided by 21 days (three weeks). When the report is at the monthly level, the age group is within the same month, within one month, within two months, and so on. The fraud age distribution is helpful if you want to compare different fraud age groups and identify any recent changes in small groups. An increased volume or fraud rate for the smallest age group indicates that more fraud will be received in the future. Therefore, you should adjust the score threshold accordingly.

## PI analysis

The **PI analysis** report shows the fraud volume, fraud rate, and fraud distribution by PI. It also provides time-based fraud distribution and fraud rate charts.

The summary section shows the total transaction volume, fraud volume, label confirmed volume, and fraud rate of the date range that is selected for the transaction date.

PI analysis has two levels: PI type and card type. You can switch between the levels by selecting the **Tab** key.

PI analysis consists of three parts:

- **Summary table** – This part shows the confirmed fraud volume, confirmed fraud rate, and percentage of confirmed fraud distribution for each segment (PI type or card type). The shaded bar indicates the volume for each segment, and the color shade for the fraud rate indicates the percentage of the fraud. High fraud rates are highlighted in red.
- **Fraud distribution percentage by segment and fraud volume** – This part shows the percentage of confirmed fraud distribution for each segment and the total confirmed fraud volume by transaction period. You can identify the product segment that has a large fraud distribution. Alternatively, you can identify changes in fraud distribution over time.
- **Fraud rate by segment** – This part shows the percentage of confirmed fraud volume versus the total label confirmed volume of each segment by transaction period. You can identify the PI segment that has a spike in the fraud rate. Alternatively, you can identify changes in the fraud rate for a PI segment over time.

## Product analysis

The **Product analysis** report shows the fraud volume, fraud rate, and fraud distribution by product. It also provides time-based fraud distribution and fraud rate charts.

The summary section shows the total transaction volume, fraud volume, label confirmed volume, and fraud rate of the date range that is selected for the transaction date.

Product analysis has three levels: product type, product category, and product name. You can switch between the levels by selecting the **Tab** key.

Product analysis consists of three parts:

- **Summary table** – This part shows the confirmed fraud volume, confirmed fraud rate, and percentage of confirmed fraud distribution for each segment (product type, product category, or product name). The shaded bar indicates the volume for each segment, and the color shade for the fraud rate indicates the percentage of the fraud. High fraud rates are highlighted in red.
- **Fraud distribution percentage by segment and fraud volume** – This part shows the percentage of confirmed fraud distribution for each segment and the total confirmed fraud volume by transaction period. You can identify the product segment that has a large fraud distribution. Alternatively, you can identify changes in fraud distribution over time.
- **Fraud rate by segment** – This part shows the percentage of confirmed fraud volume versus the total label confirmed volume of each segment by transaction period. You can identify the product segment that has a spike in the fraud rate. Alternatively, you can identify changes in the fraud rate for a PI segment over time.

<!-- I don't know what this applies to. \*Evaluated only on transactions with confirmed fraud and non-fraud statuses, as confirmed by user/merchant. -->

## Appendix

The following filters are included on the reports:

- **Billing country/region**
- **User country/region**
- **PI type, card type** – This filter includes a sub-filter for credit card and types of credit card.
- **Product type, category, name** – You can filter at different levels of the product filter tree.
- **Date range** – You can set the date range by adjusting the slider or using the date picker.
- **Label, fraud identifier** – You can filter by fraud label and non-fraud. The fraud label can include chargebacks, refunds, and other labels that were previously provided.
- **Measurement unit** – You can view the report by count or by amount.

### Hidden filter pane

The following filters are included in the filter pane on the right side of the page. The filter pane can be hidden as required.

- **Assessment type** – You can filter by evaluate or protect type.
- **Merchant final decision** – You can filter by the purchase status decision previously provided.
- **Bank decision** – You can filter by the bank decision provided.
- **Policy applied** – You can filter by rule/policy triggered transactions.
- **Recurring flag** – This flag indicates whether transactions are recurrent.
- **Over zero-dollar flag** – This flag indicates whether the purchase isn't free.
- **Confirmed fraud type** – This filter includes chargeback, refund, merchant true reject, and purchase status.
- **Confirmed non-fraud type** – This filter includes bank approved and merchant approved.
