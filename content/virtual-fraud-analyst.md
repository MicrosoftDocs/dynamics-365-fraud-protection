---
author: jackwi111
description: This topic explains how to use the virtual fraud analyst.
ms.author: v-jowigh
ms.service: fraud-protection
ms.date: 09/04/2019

ms.topic: conceptual
title: Use the virtual fraud analyst
---

# Use the virtual fraud analyst

The virtual fraud analyst uses innovative artificial intelligence (AI) technology to provide a compelling historical view of your data, and to help you set up and adjust optimal [risk score thresholds](scorecard.md). This information can then be transformed into [model operating points](lists-model-operating-points.md) to help you decide, in real time, whether to accept or reject customer transactions.

The virtual fraud analyst helps you balance acceptable levels of lost revenue and customer support costs against chargebacks, fees, and refunds. Its configuration experience implements and tests your model operating points against historical customer data.

When you create your model operating points in the virtual fraud analyst, we recommend that you complete them in the following order:

1. **Create your most fine-grained model operating points.**

For example, build a custom list of products that are currently in a specific price range, and use that list to build your model operating point. Use filters on [standard ontology nodes and attributes](graph-explorer.md), and then select an appropriate [list](lists-model-operating-points.md) that contains the corresponding dataset. For example, a model operating point can be set to screen for high-priced products that are bought only by users who are in high-risk countries or regions. The virtual fraud analyst gives you more control and helps you stop more fraud in these subsets of your traffic.

2. **Create a "catch-all fraud" model operating point for all your traffic.**

You can create a catch-all rule for your traffic that suits your needs for all transactions, without tying it to a specific custom list. To do so through the virtual fraud analyst, simply skip step 1 in the instructions below and proceed to selecting a risk score.

## Virtual fraud analyst step by step

### Step 1 (optional)
In Step 1, select the target data (a combination of a node, attributes, and a list) your model operating point will apply to. If you need to create a new list first, select **Create new list** to do so in the **List management** tool.

The following table defines the node and attribute combinations that you can use to build your lists. You can create up to three filters per model operating point, and you can create a total of 30 model operating points.

| Node | Attributes 
|---|---|
| User | Country |
| Device | DeviceType, IPCountry |
| Billing | Country |
| PaymentInstrument | Type |
| Product | Type, SKU, Category, Market |

When you've finished, select **Analyze**. This applies your settings to data from the purchase API and generates the interactive risk chart.

### Step 2
In Step 2, use the **Transaction data** graph to examine the effect of fraud upon your historical transaction data. You can choose a date range and a risk score range to filter your view. In the chart, the x-axis represents the risk score, and the y-axis represents the number of transactions.

The machine learning model in Dynamics 365 Fraud Protection evaluates every transaction by using advanced adaptive AI. It then assigns a risk score. The higher the risk score, the higher the perceived risk. The machine learning model uses a risk score range from 0 through 1000. This approach resembles the approach that the fraud protection network uses. Microsoft, in turn, converts this risk score to a more manageable -1 through 99 range to simplify decision making and reporting.

Occasionally, a transaction has an unscored risk score. An unscored risk score indicates that the model hasn't yet scored the transaction. The virtual fraud analyst generates unscored risk scores to indicate that you should create model operating points for the unscored transactions if the volume of your traffic is high enough.

Based on the risk score, from -1 through 99, the interactive chart shows the fraud impact on your revenue. The following categories are used: **Approved transations**, **Confirmed fraud** (which combines both chargebacks and refunds), and **Rejected transactions**. Hover over any point to see a detailed representation of the values.

To the right, in **Risk impact**, you can see the key metrics that are associated with the chart. Use its risk score slider to set your threshold.

| Metric | Definition |
|---|---|
| Fraud catch rate | The fraudulent transactions that have been blocked. Rejections are always above the risk score that you select. |
| Customer friction | The approved transactions that have been blocked. Approvals are equal to or less than the score that you select. |

When you choose a risk score, a summary appears that explicitly defines when transactions will be rejected.

### Step 3
After selecting the risk score with the slider on the right, name your model operating point and set its status (active or inactive), then select **Create**. Note that due to caching, your new rule may take up to two minutes to become active.

## Recommendations

The machine learning models in the fraud protection network help find emerging fraud patterns and risky attributes across all participating merchants. The virtual fraud analyst can use these findings to recommend ways that merchants who use Dynamics 365 Fraud Protection can improve the configuration of their model operating points. The virtual fraud analyst also makes recommendations about other attributes and information that can be added to the knowledge graph. This information might include chargeback data, margins, and the cost of goods sold (COGS). By augmenting existing data, you can maximize the impact of the product.

Note that before model operating points are configured, either manually or by using guidance from the virtual fraud analyst, the default decision returned on purchase transactions is to accept the transaction. This is not a recommendation, only a baseline intended to simplify your process when configuring new rule conditions. Once you have created model operating points, the decisions returned by Dynamics 365 Fraud Protection will reflect your chosen settings.

## Balance fraud loss against opportunity loss

The goal of any world-class fraud protection system is to enable companies to maximize their bottom line. By using Dynamics 365 Fraud Protection, you can quickly find a risk threshold that helps protect against fraud but also minimizes the impact on your legitimate transactions.
