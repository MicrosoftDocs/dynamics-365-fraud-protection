---
author: jegrif
description: Visually explore your data
ms.author: v-jegrif
ms.date: 02/25/2019
ms.service:
 - d365-fraud-protection
ms.topic: conceptual
title: Visually explore your data
---


# Visually explore your data

The graph explorer in Microsoft Dynamics 365 Fraud Protection enables you to explore your data and navigate to the information you need. Understand the connections between data, search for specific data points, and view their specific attributes. 

## Navigate your ontology

Selecting **Graph explorer** shows the search and filtering options. For your reference, the ontology also displays. To familiarize yourself with the structure, select any category of data, called a *node*, to view its attributes. Related nodes are connected by *edges*, which may have their own properties depending on the nature of the data. For example, the Purchase node includes attributes like PurchaseId, TotalAmount, and Currency. It is related to other nodes, like the Product being purchased, the User who bought it, and the Payment Instrument they used. 

To return to the ontology at any time and explore it in more detail, select **Ontology explorer** in the navigation. 

## Find data

To find specific data in the Graph explorer, search using the fields and filters at the top of the screen. For example, searching by User:Email will display users associated with the specified email address and any nodes related to them, like their purchase activity. Specify date ranges to narrow your search.

In the search results, select any node to see its attributes. If more than ten instances of a single node type exist, like multiple purchases, these will be clustered together. Double-click to expand this cluster and reveal the individual nodes.

When viewing details about a selected node, select any column heading to sort and filter information. Choose **Default**, **Ascending**, or **Descending** to change the sorting order, or type your desired terms into the **Filter by** field. You can also select **Query** to run a new search against a specific entity or attribute in a node.

Select **Previous query** to step back to your last search. To navigate previous queries with more specificity, use the **Query history** feature. There, you can review a list of your recent queries, their type, and the values you entered. Re-run any search in this list with **Go to query**. 

## Analyze results

Visualizing data in the graph explorer can help familiarize you with typical data relations. For instance, a single user may have multiple legitimate address nodes, such as a billing address and a shipping address, or more than one payment instrument, like a credit card and an electronic payment account. You can also evaluate these connections for signs of possible fraudulent activity. For example, a stolen payment instrument may have been used to make purchases across several user accounts. Viewing that payment instrument will show all the users connected to it. 

For deeper investigative options, see [Support your customers](customer-support.md). 
