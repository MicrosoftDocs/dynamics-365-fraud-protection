---
author: yvonnedeq
description: This topic explains how to use the virtual fraud analyst.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 04/02/2020
ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin

title: Use the virtual fraud analyst

---

# Use the virtual fraud analyst

The virtual fraud analyst (VFA) uses innovative artificial intelligence (AI) technology to provide a compelling historical view of your data, and to help you set up and adjust optimal [risk score thresholds](scorecard.md). This information can then be transformed into [rules](rules.md) that help you decide, in real time, whether to accept or reject customer transactions.

VFA helps you balance acceptable levels of lost revenue and customer support costs against chargebacks, fees, and refunds.  The configuration experience tests basic filters and risk score ranges against historical transactions.

There are two types of rules you can create in the **Rules** editor after exploring the impact of a given filter/risk score on your historical data in VFA:

1. **Fine-grained rules.**

    Creating fine-grained rules using VFA gives you more control and helps you stop more fraud in subsets of your transactions.
    
    For example, you can build a custom list of products that are currently in a specific price range and use that list to build your rule. Use filters on [standard ontology nodes and attributes](graph-explorer.md), and then select an appropriate [list](lists.md) that contains the corresponding dataset. 
    
    Next, you can set up a rule to screen for high-priced products that are bought only by users who live in high-risk countries or regions.
    
2. **"Catch-all fraud" rules for all your traffic.**

    You can create a catch-all rule to meet your needs for all transactions without being linked to a specific custom list. To understand the impact of a catch-all rule on fraud protection, skip step 1 in the step-by-step instructions below and move directly to step 2, where you select a risk score. 
    For more information on rules and lists, see [Manage rules](rules.md) and [Manage lists](lists.md).

## Use rules in the Virtual fraud analyst 

### Step 1 (optional)

In step 1, you select the target data that your rule will apply to. This data consists of a combination of a node, attributes, and a list. If you must first create a new list, see [Upload a list](lists.md#upload-a-list).

The following table defines the node and attribute combinations you can use to build your lists. 

| Node | Attributes |
|---|---|
| User | CountryRegion |
| Device | DeviceType, IPCountryRegion |
| BillingAddress | CountryRegion |
| PaymentInstrument | Type |
| Product | Type, SKU, Category, Market |

**To create a filter for historical transaction data:**

1. [Create and upload a list](lists.md#upload-a-list).
1. In the left navigation, click **Virtual fraud analyst**.
1. Select a **node**, **attribute**, **list** and **column**.
1. To add another filter, click **Add another filter** and then repeat step 3.
1. Click **Analyze**.

### Step 2

In step 2, you use the **Transaction data** chart to examine the effect of fraud on your historical transaction data. You can filter your view by selecting a range of dates and a range of risk scores. 

**To filter your view:**

1. In the **Transaction date range** section, select a range of dates.
1. In the **Transaction Data** section, enter values to adjust the impact of the risk score range on your historical data.
1. In the **Risk Impact** section, use the risk score slider to set a risk score threshold between 0-999.

#### The Transaction data chart

In the chart on the left of the **Virtual fraud analyst** page, the x-axis represents the risk score, and the y-axis represents the number of transactions.

The machine learning model in Microsoft Dynamics 365 Fraud Protection evaluates every transaction using advanced adaptive AI. It then assigns a risk score. The higher the risk score, the higher the perceived risk. The machine learning model uses a range of risk scores from 0 through 999.

Based on the risk score, the interactive chart shows the fraud impact on your revenue. The following categories are used: **Approved transactions**, **Confirmed fraud**, and **Rejected transactions**. 

You can hover over any point in the chart to see a detailed representation of the values.

#### The Risk impact metrics

In the **Risk impact** section on the right of the **Virtual fraud analyst** page, you can view the key metrics are associated with the chart. Use the risk score slider to set your threshold, and then continue to refine the score in single-point increments after you create a rule in the next step.

| Metric | Definition |
|---|---|
| Fraud catch rate | The fraudulent transactions that have been blocked. Rejections are always above the risk score that you select. |
| Customer friction | The approved transactions that have been blocked. Approvals are equal to or less than the score that you select. |

## Balance fraud loss against opportunity loss

The goal of any world-class fraud protection system is to help companies maximize their bottom line. By using Fraud Protection, you can quickly find a risk threshold that helps protect your business against fraud and also minimizes the impact on your legitimate transactions.
