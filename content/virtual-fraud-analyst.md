---
author: jackwi111
description: This topic explains how to use the virtual fraud analyst.
ms.author: v-jowigh
ms.service: crm-online
ms.date: 04/22/2019

ms.topic: conceptual
title: Use the virtual fraud analyst
---

# Use the virtual fraud analyst

The virtual fraud analyst uses innovative artificial intelligence (AI) technology to provide a compelling historical view of your data, and to help you set up and adjust optimal [risk score thresholds](scorecard.md). This information can then be transformed into [model operating points](lists-model-operating-points.md) to help you decide, in real time, whether to accept or reject customer transactions.

The virtual fraud analyst helps you balance acceptable levels of lost revenue and customer support costs against chargebacks, fees, and refunds. Its configuration experience implements and tests your model operating points against historical customer data.

When you create your prioritizations in the virtual fraud analyst, we recommend that you complete the steps in the following order:

1. **Create your most fine-grained model operating points.**

    For example, build a custom list of products that are currently in a specific price range, and use that list to build your model operating point. Use filters on [standard ontology nodes and attributes](graph-explorer.md), and then select an appropriate [list](lists-model-operating-points.md) that contains the corresponding dataset. For example, a model operating point can be set to screen for high-priced products that are bought only by users who are in high-risk countries or regions. The virtual fraud analyst gives you more control and helps you stop more fraud in these subsets of your traffic.

2. **Create a "catch-all fraud" model operating point for all your traffic.**

    Create custom lists, and add entries to them to suit your specific needs for all transactions. After these lists are created, you can use them by creating model operating points either manually or through the virtual fraud analyst. Because you've already built model operating points for high-risk locales and traffic, you can have more flexibility to analyze fraud here.

In Step 1 of the Virtual Fraud Analyst, you select the target data (a combination of a node, attributes, and a list) to apply to your model operating point.

The following table defines the node and attribute combinations that you can use to build your lists. You can create up to three filters per model operating point, and you can create a total of 30 model operating points.

| Node | Attributes |
|---|---|
| User | Country |
| Device | DeviceType, IPCountry |
| Billing | Country |
| PaymentInstrument | Type |
| Product | Type, SKU, Category, Market |

When you've finished, select **Analyze**. Your interactive risk chart appears.

In Step 2 of the Virtual Fraud Analyst, you select a date range for past transaction data and explore how different risk scores affect metrics for the fraud catch rate and customer friction. Select the line for a risk score in the bar chart, and examine the effect on your historical transaction data. Two sliders let you further refine your analysis when creating a model operating point. In the **Transaction data** pane, use the slider to adjust the risk range that is shown in the chart. In the **Risk impact** pane, use the slider to select a risk score between -1 and 99. In the **Transaction data** pane, use the dropdown for three view options:

- Graph view – Percentage of transactions
- Graph view – Total value of transactions
- Table view

In the chart, the x-axis represents the risk score. Depending on the view that you select, the y-axis represents either the percentage or number of transactions.

The machine learning model in Dynamics 365 Fraud Protection evaluates every transaction by using advanced adaptive AI. It then assigns a risk score. The higher the risk score, the higher the perceived risk. The machine learning model uses a risk score range from 0 through 1000. This approach resembles the approach that the fraud protection network uses. Microsoft, in turn, converts this risk score to a more manageable -1 through 99 range to simplify decision making and reporting.

Occasionally, a transaction has an unscored risk score. An unscored risk score indicates that the model hasn't yet scored the transaction. The virtual fraud analyst generates unscored risk scores to indicate that you should create model operating points for the unscored transactions if the volume of your traffic is high enough.

Based on the risk score, from -1 through 99, the interactive chart shows the fraud impact on your revenue. The following categories are used:

- **Approved transactions** – Transactions in this category are shown in light blue.
- **Confirmed fraud** – This category combines both chargebacks and refunds. Transactions in this category are shown in dark blue.
- **Rejected transactions** – Transactions in this category are shown in red.

Hover over any model operating point to see the representation of the values.

At the same time, the **risk impact** pane shows the key metrics that are associated with the chart.

| Metric | Definition |
|---|---|
| Fraud catch rate | The fraudulent transactions that have been blocked. Rejections are always above the risk score that you select. |
| Customer friction | The number of good (non-fraudulent) transactions that have been blocked. Approvals are equal to or less than the score that you select. |

After you've selected a risk score, a **Model Operating Point Summary** appears that explicitly defines when transactions will be rejected.

In Step 3 of the Virtual Fraud Analyst, you name, select a status, and create your model operating point that is based on the risk score you previously selected.

## Recommendations

The machine learning models in the fraud protection network help find emerging fraud patterns and risky attributes across all participating merchants. The virtual fraud analyst can use these findings to recommendations ways that merchants who use Dynamics 365 Fraud Protection can improve the configuration of their model operating points. The virtual fraud analyst also makes recommendations about other attributes and information that can be added to the knowledge graph. This information might include chargeback data, margins, and the cost of goods sold (COGS). By augmenting existing data, you can maximize the impact of the product.

## Balance fraud loss against opportunity loss

The goal of any world-class fraud protection system is to enable companies to maximize their bottom line. By using Dynamics 365 Fraud Protection, you can quickly find a risk threshold that helps protect against fraud but also minimizes the impact on your legitimate transactions.
