---
author: jackwi111
description: Use the virtual fraud analyst
ms.author: v-jowigh
ms.date: 02/25/2019
ms.service:
 - d365-fraud-protection
ms.topic: conceptual
title: Use the virtual fraud analyst
---


# Use the virtual fraud analyst

Using innovative AI technology, the virtual fraud analyst provides a compelling historical view of your data, and helps you set up and adjust your optimal [risk score thresholds](https://go.microsoft.com/fwlink/?linkid=2082325). This information can then be transformed into [model operating points]( https://go.microsoft.com/fwlink/?linkid=2082115), shaping your real-time decision-making in accepting or rejecting customer transactions.

The virtual fraud analyst helps you balance acceptable levels of lost revenue and customer support costs with chargebacks, fees, and refunds. Its configuration experience implements and tests your model operating points against historical customer data. 

In the virtual fraud analyst, we recommend the following order when creating your stack:

- First, start your analyses with your model operating points. You can use these points on all transactions at once or specific subsets. For instance, you could apply a model operating point only to products of a specific price range. Using filters from standard and customized [ontology nodes and attributes](https://go.microsoft.com/fwlink/?linkid=2082342), choose an appropriate [list](https://go.microsoft.com/fwlink/?linkid=2082115) that contains the corresponding dataset. For instance, a model operating point could be set to screen for high-priced products being bought only by users in high-risk countries. The virtual fraud analyst enables you to be more assertive stopping fraud in these subsets of traffic.
- Next, if lists don’t exist in the virtual fraud analyst, create them in [List management](https://go.microsoft.com/fwlink/?linkid=2082115).
- Lastly, create a ‘catch-all fraud’ model operating point for all your traffic. Do this by creating custom lists and populating them to suit your specific needs for all transactions. Once created, these lists can be used by manually creating model operating points or with the virtual fraud analyst. You can have a broader reach here as you’ll already have built model operating points for high-risk locales and traffic.

In Step 1, select the target data (a combination of node, attribute, and list) to apply your model operating point.
The following table defines the node and attribute combinations to build your lists. You can create up to three filters per rule; and a total of 30 rules.

|Node   |Attribute   |
|---|---|
|User   |Country   |
|Device   |DeviceType, IPCountry   |
|Billing   |Country   |
|PaymentInstrument   |Type   |
|Product   |Type, Sku, Category, Market   |

When complete, select **Analyze** and your interactive risk chart appears.

In Step 2, select a date range for past transactions data and explore how varying risk scores can impact fraud catch rates and customer friction. Choose a risk score from the chart and click a model operating point to examine the effect upon your historical transaction data. To further refine your analysis in creating a model operating point, use the two slider bars, **Transaction data** (to adjust the risk range to display in the graph) and **Risk impact** (select a risk score between 0 and 100). From the transaction data dropdown, you have three viewing options:

- Graph view: Percentage of transactions
- Graph view: Total value of transactions
- Table view

In the chart, the x-axis represents the risk score; and depending on the view you select, the y-axis represents the percentage or number of transactions.

The machine learning model in Dynamics 365 Fraud Protection evaluates every transaction using cutting-edge AI, and assigns a risk score. The higher the risk score, the higher the perceived risk. The machine learning model uses a risk score range from 0-999 – similar to the fraud protection network. We, in turn, transpose this risk score into a more manageable 0-100 range for simpler decision making and reporting.

Occasionally, a transaction has an unscored risk score. This means that the transaction has not yet been scored by the model. The virtual fraud analyst generates unscored risk scores as an indicator for you to create rules for these transactions if the volume is sufficiently high.

This interactive chart shows the fraud impact on your revenues related to the risk score, from 0-100 in these categories:

- Approved transactions. Represented by light blue.
- Confirmed fraud (combines both chargebacks and refunds). Represented by dark blue.
- Rejected transactions. Represented by red.
Hover over any model operating point to see these values represented.

Simultaneously, key metrics accompany the chart, represented in the risk impact panel:

|Impact   |Definition   |
|---|---|
|Fraud catch rate   |Fraudulent transactions blocked. Rejections are always above the risk score you select.   |
|Customer friction   |Good transactions blocked. Approvals are equal to or less than the score you select.   |

In Step 3, create a model operating point based on a risk score that meets your satisfaction.

After you have settled on your model operating point, a Model Operating Point Summary appears explicitly defining when transactions will be rejected according to the parameters above your defined risk score.

## Recommendations

The machine learning models in the fraud protection network help find emerging fraud patterns and risky attributes across all participating merchants. The virtual fraud analyst can leverage these findings and make recommendations to all Dynamics 365 Fraud Protection merchants about improving the configuration of their rules. The virtual fraud analyst also makes recommendations about how to augment existing data by adding additional attributes and information into the knowledge graph (for example, chargeback data, margins, and COGS) to maximize the impact of the product.

## Balance fraud loss versus opportunity loss

The goal of any world-class fraud protection system is to enable companies to optimize their bottom line. Using Dynamics 365 Fraud Protection, you can quickly find a risk threshold to help balance fraud protection while keeping the impact to your legitimate transactions at comfortably low levels.



