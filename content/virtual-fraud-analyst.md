---
author: yvonnedeq
description: This topic explains how the Virtual fraud analyst (VFA) in Microsoft Dynamics 365 Fraud Protection helps you set up and adjust risk score thresholds.
ms.author: josaw
ms.date: 03/31/2022
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin

title: Virtual fraud analyst

---

# Virtual fraud analyst

The virtual fraud analyst (VFA) uses innovative artificial intelligence (AI) technology to provide a compelling historical view of your data, and to help you set up and adjust optimal [risk score thresholds](scorecard.md). This information can then be transformed into rules that help you decide, in real time, whether to accept or reject customer transactions.

VFA helps you balance acceptable levels of lost revenue and customer support costs against chargebacks, fees, and refunds. The configuration experience tests risk score threshold, reject rate, fraud rate and profit margin against historical transactions, to estimate risk impact on detection rate, net profit achieved, and other values.

The **Score rule optimizer** report is updated with the latest transactional data every 24 hours. The time stamp on the report shows the time the report was last updated, in Coordinated Universal Time.

You can switch views on the report between **Count view** and **Amount view**. **Count view** shows volume and percentage by transaction count and **Amount view** shows volume and percentage in US dollars.

The machine learning (ML) model in Fraud Protection evaluates every transaction by using advanced adaptive artificial intelligence (AI) and then assigns a risk score. In general, the higher the risk score, the higher the perceived risk. The ML model uses a range of risk scores from 0 through 999.

## User filters

You can use the drop-down menus and sliders in the VFA to filter your view of the interactive charts. The following filter options are available.

- **PI type** – Includes payment instrument type such as **Card type**.

- **Product type** – Enables you to display based on product type.

- **IP country/region** – Filters on country or region, based on IP address.

- **Date range** – Shows transaction data by date. You can select dates in the calendar, enter dates manually, or select date ranges.

- **Non-fraud type** – Filters by non-fraud label. The non-fraud label may include *Bank approved*, *Merchant approved*, and other labels that you previously provided. 
> [!NOTE]
> Changing this value will impact the denominator for the calculation of fraud rate.

- **Fraud type** – Filters by fraud label. The fraud label may include *Chargebacks*, *Refunds*, *Merchant rejected*, and other labels that you previously provided.
> [!NOTE]
> Changing this value will impact fraud volume and the numerator for the calculation of fraud rate.

## Estimated risk impact

In the **estimated risk impact** report, you can adjust the criteria and view the estimated impact based on key metrics. You can select score cutoff, reject rate, fraud rate, or estimated profit margin as input.

- **Score cutoff** – The risk score can range from 0 to 999, and you can select the score cutoff in increments of 10.

- **Reject rate** – Select the target reject rate to calculate the corresponding score cutoff.

- **Fraud rate** –  Select the target fraud rate to calculate the corresponding score cutoff.

- **Estimated profit margin** – Provide the estimated profit margin for the products to calculate the corresponding score cutoff and analyze the optimal net profit achieved.

Key metrics for risk impact include the following.

- **Detection rate** – Shows the fraudulent transactions that were blocked.

- **Reject rate** – Shows the percentage of volume where the merchant's final decision was rejected and a decision was not made by the bank, out of the total volume of transactions.

- **Fraud rate** – Shows the percentage of fraud volume, out of the total settled volume.

- **Net profit achieved** - Shows the percentage of total net profit achieved at the given score cutoff.

## Estimated net profit and net profit achieved percentage

In this chart, the x-axis represents the risk score, the blue bars represent net profit, and the black line represents net profit percentage.

Based on the risk score, the interactive chart shows the impact of fraud on your revenue. The following categories are used in the chart; **Approved transactions**, **transactions labeled as fraud**, and **Rejected transactions**.

You can use the following filters.

- **Estimated profit margin** - Provides the estimated profit margin for the products.

- **Score range** - Use the text input box or the scroll bar to select the desired score range.

You can hover over any area in the chart to display a detailed representation of the values.

## Balance fraud loss against opportunity loss

The goal of any world class fraud protection system is to help companies maximize their bottom line. By using Fraud Protection, you can quickly find a risk threshold that helps protect your business against fraud and also minimize the impact on your legitimate transactions.

### Create rules

You can create rules in the **Rules editor** after you explore the impact of a specific filter and risk score on your historical data in VFA.

For more information about rules and lists, see [Manage rules](rules.md) and [Manage lists](lists.md).

[!INCLUDE[footer-include](includes/footer-banner.md)]
