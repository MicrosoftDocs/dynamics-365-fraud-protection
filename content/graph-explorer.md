---
author: yvonnedeq
description: This topic explains how you can visually explore your data in Microsoft Dynamics 365 Fraud Protection.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 07/09/2020
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Visually explore your data with the graph explorer
---

# Visually explore your data with the graph explorer

The graph explorer in Microsoft Dynamics 365 Fraud Protection enables you to understand the connections between data, search for specific data points, and view the attributes of data points.

## Visualize your ontology

To display search and filtering options in Fraud Protection, select **Data engineering** and then select **Graph explorer**. 

When the graph explorer first opens, it displays the ontology so you can view its structure. Each *node* represents an essential category of data. Select a node to see its *attributes*. Attributes describe the node's specific properties. Related nodes are connected by *edges*, which may have their own properties depending on the nature of the data.

For example, the **Purchase** node has attributes such as **PurchaseId**, **TotalAmount**, and **Currency**. It's connected to other nodes, such as the nodes for the product that was bought, the user who bought it, and the payment instrument that was used to buy it.

## Find data

To find specific data in the graph explorer, use the search fields and filters at the top of the page. For example, search by **User:Email** to show users who are associated with the specified email address and any nodes that are related to those users, such as the purchases that they made. You can also select date ranges to narrow your search.

If more than ten instances of a single node type exist (for example, if there are multiple purchases), the nodes are clustered together. Double-click a cluster to expand it and show the individual nodes.

To pivot your search to a new node, double-click the node. While you're viewing any node, you can also select **Query** to run a new search against a specific entity or attribute.

To step back to your last search, select **Previous query**. To navigate your previous queries with more specificity, you can use the query **History** feature. This feature lets you review a list of the queries that you've run during your current session, the type of each query, and the values that you entered. You can rerun any query in the list by selecting **Go to query**.

## View, sort, and filter attributes

In the search results, select a node to see its attributes. To see the attributes of other nodes of the same type, select a node in the **Entity list**.

While you're viewing these details, you can click any column heading to access the sorting and filtering options. Select **Default**, **Ascending**, or **Descending** to change the sort order, or enter search terms in the **Filter by** field.

## Analyze results

By visualizing data in the graph explorer, you can become familiar with typical data relations. For example, a single user might have multiple legitimate address nodes, such as a billing address and a shipping address, or multiple payment instruments, such as a credit card and an electronic payment account. You can also evaluate these connections for signs of possible fraudulent activity. For example, a stolen payment instrument might have been used to make purchases across several user accounts. By viewing the payment instrument, you can see all the users who are connected to it.

For information about options available for doing deeper investigations, see [Support your customers](risk-support.md).
