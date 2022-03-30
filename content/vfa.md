---
author: josaw1
description: This topic explains how to configure user access to Microsoft Dynamics 365 Fraud Protection.
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

The virtual fraud analyst (VFA) uses innovative artificial intelligence (AI) technology to provide a compelling historical view of your data, and to help you set up and adjust optimal [<u>risk score thresholds</u>](https://docs.microsoft.com/en-gb/dynamics365/fraud-protection/scorecard). This information can then be transformed into rules that help you decide, in real time, whether to accept or reject customer transactions.

VFA helps you balance acceptable levels of lost revenue and customer support costs against chargebacks, fees, and refunds. The configuration experience tests risk score threshold, reject rate, fraud rate and profit margin against historical transaction, to estimate risk impact on detection rate, net profit achieved and others.

The score rule optimizer report is updated with the latest transactional data every 24 hours. The time stamp on the report shows the update time in Coordinated Universal Time.

You can switch views between count view and amount view. Count view shows volume and percentage by transaction count, and amount view shows volume and percentage in US dollars.

The machine learning model in Fraud Protection evaluates every transaction by using advanced adaptive AI. It then assigns a risk score. The higher the risk score, the higher the perceived risk. The machine learning model uses a range of risk scores from 0 (zero) through 999.

**Use filters in VFA**

You can use the drop-down menus and sliders on the VFA to filter your view of the interactive charts. The following filter options are available:

**PI type** This filter includes payment instrument type such as card type.

**Product type** – You can filter at product type.

**IP country/region** – Country/region based on IP address.

**Date range** – Use this filter to show transaction data by date. You can select dates in the calendar, enter dates manually, or select date ranges.

**Non-fraud type** – You can filter by non-fraud label. The non-fraud label include bank approved, merchant approved, and other labels previously provided. <u>Changing this will impact denominator for the calculation of fraud rate.</u>

**Fraud type** – You can filter by fraud label. The fraud label include chargebacks, refunds, merchant rejected and other labels previously provided. <u>Changing this will impact fraud volume and numerator for the calculation of fraud rate.</u>

**Estimated risk impact**

In the **estimated risk impact**, you can adjust the criteria and view the estimated impact on key metrics. Select score cutoff, reject rate, fraud rate, or estimated profit margin as input.

Score cutoff: risk score can range from 0 to 999, and you can select score cutoff in increments of 10.

Reject rate: you can select target reject rate and VFA tool will calculate corresponding score cutoff.

Fraud rate: you can select target fraud rate and VFA tool will calculate corresponding score cutoff.

Estimated profit margin: user can provide estimated profit margin for the products and the VFA tool will calculate corresponding score cutoff and analyze optimal net profit achieved.

|                                       |     |
|---------------------------------------|-----|
| Key metrics for risk impact includes: |     |
|                                       |     |

- **Detection rate**- The fraudulent transactions that have been blocked

- **Reject rate\*** – The percentage of volume where the merchant's final decision was rejected and a decision wasn't made by the bank, out of the transaction volume.

- **Fraud rate\*** – The percentage of fraud volume out of the total settled volume.

- **Net profit achieved**- percentage of total net profit achieved at given score cutoff

**Estimated net profit and net profit achieved percentage**

In this chart, the x-axis represents the risk score, and the blue bars represent net profit, and the black line represents net profit percentage.

Based on the risk score, the interactive chart shows the impact of fraud on your revenue. The following categories are used: **Approved transactions**, **transactions labeled as fraud**, and **Rejected transactions**.

You can use the following filters on the tool:

**Estimated profit margin:** user can provide estimated profit margin for the products.

**Score range**: use the input or scroll bar to select desired score range.

You can hover over any point in the chart to see a detailed representation of the values.

**Balance fraud loss against opportunity loss**

The goal of any world-class fraud protection system is to help companies maximize their bottom line. By using Fraud Protection, you can quickly find a risk threshold that helps protect your business against fraud and also minimize the impact on your legitimate transactions.

Create rules in Fraud protection

You can create rules in the Rules editor after you explore the impact of a specific filter and risk score on your historical data in VFA.

For more information about rules and lists, see [<u>Manage rules</u>](https://docs.microsoft.com/en-gb/dynamics365/fraud-protection/rules) and [<u>Manage lists</u>](https://docs.microsoft.com/en-gb/dynamics365/fraud-protection/lists).
