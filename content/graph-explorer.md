---
author: jegrif
description: Visually explore your data
ms.author: v-jegrif
ms.service: crm-online
ms.date: 02/25/2019

ms.topic: conceptual
title: Visually explore your data
---


# Visually explore your data

The graph explorer in Microsoft Dynamics 365 Fraud Protection enables you to explore your data and navigate to the information you need. Use it to understand the connections between data, search for specific data points, and view their specific attributes. 

## Visualize your ontology

Selecting **Graph explorer** displays the search and filtering options. When first opened, the graph explorer also shows the ontology to illustrate its structure. Each *node* shown represents an essential category of data. Select any node to see its attributes, which describe the node's specific properties. Related nodes are connected by *edges*, which may have their own properties depending on the nature of the data. For example, the Purchase node includes attributes like PurchaseId, TotalAmount, and Currency. It is connected to other nodes, like the Product being purchased, the User who bought it, and the Payment Instrument they used.

## Find data

To find specific data in the Graph explorer, search using the fields and filters at the top of the screen. For example, searching by User:Email will display users associated with the specified email address and any nodes related to them, like the purchases they made. Choose date ranges if desired to narrow your search.

If more than ten instances of a single node type exist, like multiple purchases, these will be clustered together. Double-click to expand this cluster and reveal the individual nodes.

To pivot your search to a new node, double-click the node. While viewing any node, you can also select **Query** to run a new search against a specific entity or attribute.

Select **Previous query** to step back to your last search. To navigate previous queries with more specificity, use the **Query history** feature. There, you can review a list of the queries you made during this session, their type, and the values you entered. Re-run any search in this list with **Go to query**. 

## View, sort, and filter attributes 
In the search results, select any node to see its attributes. Select any other node in the **Entity list** to see the attributes of other nodes of the same type. 

While viewing these details, click any column heading for sorting and filtering options. Choose **Default**, **Ascending**, or **Descending** to change the sorting order, or type your desired terms into the **Filter by** field. 

## Analyze results

Visualizing data in the graph explorer can help familiarize you with typical data relations. For instance, a single user may have multiple legitimate address nodes, such as a billing address and a shipping address, or more than one payment instrument, like a credit card and an electronic payment account. You can also evaluate these connections for signs of possible fraudulent activity. For example, a stolen payment instrument may have been used to make purchases across several user accounts. Viewing that payment instrument will show all the users connected to it.

For deeper investigative options, see [Support your customers](risk-support.md). 
