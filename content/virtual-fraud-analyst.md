---
author: yvonnedeq
description: This article explains how the Virtual fraud analyst (VFA) in Microsoft Dynamics 365 Fraud Protection helps you set up and adjust risk score thresholds.
ms.author: josaw
ms.date: 02/02/2023
ms.topic: conceptual
search.audienceType:
  - admin

title: Virtual fraud analyst

---

# Virtual fraud analyst

The virtual fraud analyst (VFA) uses innovative artificial intelligence (AI) technology to provide a compelling historical view of your data, and to help you set up and adjust optimal [risk score thresholds](scorecard.md). This information can then be transformed into rules that help you decide, in real time, whether to accept or reject customer transactions.

VFA helps you balance acceptable levels of lost revenue and customer support costs against chargebacks, fees, and refunds. The configuration experience tests the risk score threshold, reject rate, fraud rate, and profit margin against historical transactions to estimate the risk impact on the detection rate, the net profit achieved, and other values.

The **Score rule optimizer** report is updated with the latest transactional data every 24 hours. The time stamp on the report shows the time when the report was last updated, in Coordinated Universal Time.

You can switch views on the report between **Count view** and **Amount view**. **Count view** shows volume and percentage by transaction count, and **Amount view** shows volume and percentage in US dollars.

The machine learning (ML) model in Microsoft Dynamics 365 Fraud Protection evaluates every transaction by using advanced adaptive AI and then assigns a risk score. In general, the higher the risk score, the higher the perceived risk. The ML model uses a range of risk scores from 0 through 999.

If your Fraud Protection instance has multiple environments, you can access the report in a specific environment by using the environment switcher. If the environment has child environments, the data on the report includes transactions and assessments for all the child environments.

## User filters

You can use the drop-down menus and sliders in VFA to filter your view of the interactive charts. The following filter options are available:

- **PI type** – Include payment instrument type, such as **Card type**.
- **Product type** – Change the display based on the product type.
- **IP country/region** – Filter by country or region, based on Internet Protocol (IP) address.
- **Date range** – Show transaction data by date. You can select dates in the calendar, manually enter dates, or select date ranges.
- **Non-fraud type** – Filter by non-fraud label. The non-fraud labels might include *Bank approved*, *Merchant approved*, and other labels that you previously provided.

    > [!NOTE]
    > Changes to this value will affect the denominator for the calculation of the fraud rate.

- **Fraud type** – Filter by fraud label. The fraud labels might include *Chargebacks*, *Refunds*, *Merchant rejected*, and other labels that you previously provided.

    > [!NOTE]
    > Changes to this value will affect the fraud volume and the numerator for the calculation of the fraud rate.

## Estimated risk impact

On the **estimated risk impact** report, you can adjust the criteria and view the estimated impact, based on key metrics. You can select the score cutoff, reject rate, fraud rate, or estimated profit margin as input.

- **Score cutoff** – The risk score can range from 0 through 999, and you can select the score cutoff in increments of 10.
- **Reject rate** – Select the target reject rate to calculate the corresponding score cutoff.
- **Fraud rate** – Select the target fraud rate to calculate the corresponding score cutoff.
- **Estimated profit margin** – Provide the estimated profit margin for the products to calculate the corresponding score cutoff and analyze the optimal net profit achieved.

The following key metrics for risk impact are available:

- **Detection rate** – The fraudulent transactions that were blocked.
- **Reject rate** – The percentage of volume where the merchant's final decision was rejected and a decision wasn't made by the bank, out of the total volume of transactions.
- **Fraud rate** – The percentage of fraud volume, out of the total settled volume.
- **Net profit achieved** – The percentage of total net profit achieved at the given score cutoff.

## Estimated net profit and net profit achieved percentage

In this chart, the x-axis represents the risk score, the blue bars represent net profit, and the black line represents the net profit percentage.

Based on the risk score, the interactive chart shows the impact of fraud on your revenue. The following categories are used in the chart; **Approved transactions**, **transactions labeled as fraud**, and **Rejected transactions**.

You can use the following filters:

- **Estimated profit margin** – Provide the estimated profit margin for the products.
- **Score range** – Use the text box or the scroll bar to select the desired score range.

You can hover over any area in the chart to show a detailed representation of the values.

## Balance fraud loss against opportunity loss

The goal of any world-class fraud protection system is to help companies maximize their bottom line. By using Fraud Protection, you can quickly find a risk threshold that helps protect your business against fraud and minimize the impact on your legitimate transactions.

### Create rules

After you explore the impact of a specific filter and risk score on your historical data in VFA, you can create rules in the Rules editor.

For more information about rules and lists, see [Manage rules](rules.md) and [Manage lists](lists.md).

[!INCLUDE[footer-include](includes/footer-banner.md)]
