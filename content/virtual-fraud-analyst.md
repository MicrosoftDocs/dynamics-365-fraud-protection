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

The virtual fraud analyst (VFA) uses innovative artificial intelligence (AI) technology to provide a compelling historical view of your data, and to help you set up and adjust optimal [risk score thresholds](scorecard.md). This information can then be transformed into [rules](lists-rules.md) that help you decide, in real time, whether to accept or reject customer transactions.

VFA enables you to balance acceptable levels of lost revenue and customer support costs against chargebacks, fees, and refunds. The configuration experience tests basic filters and risk score ranges against historical transactions.

There are two types of rules you can create in the **Rules** editor after exploring the impact of a given filter/risk score on your historical data in VFA:

1. **Fine-grained rules.**

    Creating fine-grained rules using VFA gives you more control and helps you stop more fraud in subsets of your transactions.
    For example, you can build a custom list of products that are currently in a specific price range and use that list to build your rule. First, use filters on [standard ontology nodes and attributes](graph-explorer.md), and then select an appropriate [list](lists-rules.md) that contains the corresponding dataset. Next, set up a rule to screen for high-priced products that are bought only by users who live in high-risk countries or regions.
    
2. **"Catch-all fraud" rules for all your traffic.**

    You can create a catch-all rule to meet your needs for all transactions without being linked to a specific custom list. To understand the impact of a catch-all rule on fraud protection, skip step 1 in the step-by-step instructions below and move directly to step 2, where you select a risk score. For more information on rules and lists, see the Rules and Lists Overview.

## Create rules in VFA

### Step 1 (optional): select what the rule applies to

In step 1, select the target data that your rule will apply to. This data consists of a combination of a node, attributes, and a list. If you must first create a new list, you can do so on the **Virtual fraud analyst** page. For more information on how to create a list, see step 2 below.

The following table defines the node and attribute combinations you can use to build your lists. 

| Node | Attributes |
|---|---|
| User | CountryRegion |
| Device | DeviceType, IPCountryRegion |
| BillingAddress | CountryRegion |
| PaymentInstrument | Type |
| Product | Type, SKU, Category, Market |

To create a filter for historical transaction data, do the following.

1. In the left navigation, click **Virtual fraud analyst**.
2. To create a new list:
     1. Click **Create a new list**.
     2. Add a name, description, node, and attribute.
     3. Enter your list entries, and then click **Create**.
3. In the left navigation, click **Virtual fraud analyst**.
4. Select a **Node**, **Attribute** and **List**.
5. To add another filter, click **Add another filter** and then repeat steps 2-4.
6. Click **Analyze**.

### Step 2: examine the effect of fraud

In step 2, use the **Transaction data** chart to examine the effect of fraud on your historical transaction data. You can filter your view by selecting a range of dates and a range of risk scores. 

To filter your view, do the following.

1. In the **Transaction date range** section, select a range of dates.
2. In the **Transaction Data** section, enter values to adjust the impact of the risk score range on your historical data.
3. In the **Risk Impact** section, use the risk score slider to set a risk score threshold between 0-999.

#### Understanding the Transaction data chart

In the chart on the left, the x-axis represents the risk score, and the y-axis represents the number of transactions.

The machine learning model in Microsoft Dynamics 365 Fraud Protection evaluates every transaction using advanced adaptive AI. It then assigns a risk score. The higher the risk score, the higher the perceived risk. The machine learning model uses a range of risk scores from 0 through 999. This approach resembles the approach that the fraud protection network uses.

Based on the risk score, from 0 through 999, the interactive chart shows the fraud impact on your revenue. The following categories are used: **Approved transactions**, **Confirmed fraud**, and **Rejected transactions**. (The **Confirmed fraud** category combines chargebacks and refunds.) You can hover over any point in the chart to see a detailed representation of the values.

#### The Risk Impact metrics

On the right, in the **Risk impact** section, you can see the key metrics that are associated with the chart. Use the risk score slider to set your threshold, and then continue to refine the score in single-point increments after you create a rule in the next step.

| Metric | Definition |
|---|---|
| Fraud catch rate | The fraudulent transactions that have been blocked. Rejections are always above the risk score that you select. |
| Customer friction | The approved transactions that have been blocked. Approvals are equal to or less than the score that you select. |

## Balance fraud loss against opportunity loss

The goal of any world-class fraud protection system is to help companies maximize their bottom line. By using Microsoft Dynamics  365 Fraud Protection (DFP), you can quickly find a risk threshold that helps protect your business against fraud and also minimizes the impact on your legitimate transactions.
