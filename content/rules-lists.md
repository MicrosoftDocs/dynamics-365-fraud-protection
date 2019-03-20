---
author: jegrif
description: Customize rules and lists
ms.author: v-jegrif
ms.date: 03/18/2019
ms.service:
 - d365-fraud-protection
ms.topic: conceptual
title: Customize rules and lists
---


# Manage rules and lists

Help manage your risk decisions and tailor the behavior of Microsoft Dynamics 365 Fraud Protection to suit your business’s needs with the rules engine.

*Rules* shape real-time decision-making by accepting or rejecting transactions. Your rules operate across *lists*, including safe and block lists for customers, and custom lists based around chosen conditions relevant to your business needs. These capabilities are designed to help you manage the trade-offs inherent in preventing fraud while minimizing false positives. You can also enforce various types of business policies such as government-prescribed trade embargos, geofencing, and control of reseller activity.

In the Evaluate experience, use the rules engine to build your rules and lists and learn how they can improve your fraud protection strategies. In Protect, apply them to your production environment for real-time results.

## List management 

### Search 
Use the search feature to find customers or payment instruments already entered in the Safe or Block lists. Select your entry type, then paste in the information you wish to find. Each entry must be on a separate line. Any matches will display in **Search results**, along with a summary of their key properties.

To edit an entry or remove it from a list, click the ellipses to the right. Edit will enable you to change list assignment, pick a new expiry date, state your reason for the change, add comments, and review any past notes about this case.

### Bulk list updates 
To add multiple entries simultaneously to the Safe or Block lists, select **Bulk list updates**. All fields are required, and all entries must be listed on separate lines. Up to 1,000 entries can be added at a time.

### Create custom lists 
Custom lists can be created and populated to suit specific needs. Once created, these lists are usable within manually created rules or by the [virtual fraud analyst](virtual-fraud-analyst.md). To create a new list from scratch, open **List management** and select **Create new custom list**.

Each list comprises a collection of things you want to screen for, such as high-priced products or high-risk countries. Name and describe your list to summarize its contents, then select the appropriate node and attribute and populate the attribute list. Nodes represent essential categories of data, and attributes describe their specific properties. The nodes and attributes available in list and rules configuration are those relevant to the transaction payload.

For example, to create a list containing high-priced products, Product would be the relevant node and SKU would be the key attribute type. To enter the individual SKUs of the highest-priced products in your inventory, paste these list items into the neighboring field. Each entry must be on a separate line.

Once saved, your new custom list will be viewable and editable under **Custom lists** on the **List management** page, and can be selected when configuring rules.

## Rules

New rules can be created manually or by utilizing the guidance of the [virtual fraud analyst](virtual-fraud-analyst.md). To create a custom rule, select **Create new rule** on the **Rules management** page. 

Rules can be applied to all transactions or specific subsets. For instance, a rule could operate only on products of a specific price. To create that filter, set your parameters by selecting the appropriate node and attribute. Then choose the list that contains your specified attributes. Up to three filters can be applied to make a rule operate across multiple lists simultaneously. For instance, a rule could be set to screen for high-priced products being bought by users in high-risk countries.

On the next screen, choose the desired behavior of this rule, such as to reject all transactions that meet the specified conditions, or to reject transactions only if they meet the conditions and cross a specific risk score threshold. Name your rule, set its state (active or inactive), and save.

Once created, any rule on this page can be edited. To deactivate a rule, toggle it to **Inactive**. To delete a rule completely, click the ellipses on the right-hand side of the screen and select **Delete**. 
