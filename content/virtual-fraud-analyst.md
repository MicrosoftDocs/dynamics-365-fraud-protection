---
author: v-davido
description: This topic explains how to use the virtual fraud analyst.
ms.author: v-davido
ms.service: fraud-protection
ms.date: 02/20/2020
ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin

title: Use the virtual fraud analyst

---

# Use the virtual fraud analyst

The virtual fraud analyst uses innovative artificial intelligence (AI) technology to provide a compelling historical view of your data, and to help you set up and adjust optimal [risk score thresholds](scorecard.md). This information can then be transformed into [rules](lists-rules.md) that help you decide, in real time, whether to accept or reject customer transactions.

The virtual fraud analyst helps you balance acceptable levels of lost revenue and customer support costs against chargebacks, fees, and refunds. Its configuration experience implements and tests your rules against historical customer data.

When you create your rules in the virtual fraud analyst, we recommend that you create them in the following order:

1. **Create your most fine-grained rules.**

    For example, build a custom list of products that are currently in a specific price range, and use that list to build your rule. Use filters on [standard ontology nodes and attributes](graph-explorer.md), and then select an appropriate [list](lists-rules.md) that contains the corresponding dataset. For example, a rule can be set to screen for high-priced products that are bought only by users who are in high-risk countries or regions. The virtual fraud analyst gives you more control and helps you stop more fraud in these subsets of your traffic.

2. **Create a "catch-all fraud" rule for all your traffic.**

    A catch-all rule meets your needs for all transactions, without being linked to a specific custom list. To create a catch-all rule for your traffic through the virtual fraud analyst, just skip step 1 of the instructions that follow, and move on to step 2, where you select a risk score.

## Virtual fraud analyst step-by-step instructions

### Step 1 (optional)

In step 1, you select the target data that your rule will apply to. This data consists of a combination of a node, attributes, and a list.

If you must first create a new list, select **Create new list** in the List management tool.

The following table defines the node and attribute combinations that you can use to build your lists. You can create up to three filters per rule, and you can create a total of 30 rules.

| Node | Attributes |
|---|---|
| User | CountryRegion |
| Device | DeviceType, IPCountryRegion |
| BillingAddress | CountryRegion |
| PaymentInstrument | Type |
| Product | Type, SKU, Category, Market |

When you've finished, select **Analyze**. Your settings are applied to data from the purchase application programming interface (API), and the interactive risk chart is generated.

### Step 2

In step 2, you use the **Transaction data** chart to examine the effect of fraud on your historical transaction data. You can filter your view by selecting a range of dates and a range of risk scores. In the chart, the x-axis represents the risk score, and the y-axis represents the number of transactions.

The machine learning model in Microsoft Dynamics 365 Fraud Protection evaluates every transaction by using advanced adaptive AI. It then assigns a risk score. The higher the risk score, the higher the perceived risk. The machine learning model uses a range of risk scores from 0 through 999. This approach resembles the approach that the fraud protection network uses.

Based on the risk score, from 0 through 999, the interactive chart shows the fraud impact on your revenue. The following categories are used: **Approved transactions**, **Confirmed fraud**, and **Rejected transactions**. (The **Confirmed fraud** category combines chargebacks and refunds.) You can hover over any point to see a detailed representation of the values.

On the right, in the **Risk impact** section, you can see the key metrics that are associated with the chart. Use the risk score slider to set your threshold, and then continue to refine the score in single-point increments after you create a rule in the next step.

| Metric | Definition |
|---|---|
| Fraud catch rate | The fraudulent transactions that have been blocked. Rejections are always above the risk score that you select. |
| Customer friction | The approved transactions that have been blocked. Approvals are equal to or less than the score that you select. |

When you select a risk score, a summary appears. This summary explicitly defines when transactions will be rejected.

### Step 3

After you've selected a risk score by using the risk score slider on the right, name your rule, set its status (active or inactive), and then select **Create**. Note that, because of caching, your new rule might take up to two minutes to become active.

## Balance fraud loss against opportunity loss

The goal of any world-class fraud protection system is to help companies maximize their bottom line. By using Fraud Protection, you can quickly find a risk threshold that helps protect against fraud but also minimizes the impact on your legitimate transactions.
