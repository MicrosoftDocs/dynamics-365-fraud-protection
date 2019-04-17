---
author: jegrif
description: This topic explains how to manage lists and model operating points in Microsoft Dynamics 365 Fraud Protection.
ms.author: v-jegrif
ms.service: crm-online
ms.date: 03/28/2019

ms.topic: conceptual
title: Manage lists and model operating points
---

# Manage lists and model operating points

You can use lists and model operations to help manage your risk decisions and tailor the behavior of Microsoft Dynamics 365 Fraud Protection.

*Model operating points* shape real-time decision making by accepting or rejecting transactions based on conditions and risk score thresholds that you select. The model operating points use *lists*, such as the Safe list, Block list, and custom lists of data that are relevant to your business. These capabilities help you define and screen for risky transaction types. They also help you enforce various policies, such as geofencing. These capabilities are designed to help you manage the trade-offs that are inherent when you must prevent fraud but also minimize false positives.

## List management

To manage the Safe and Block lists, and to create your own custom lists, select **List management** in the navigation.

### Bulk list updates

You can add, remove, or edit large sets of information in your Safe list or Block list by using the **Bulk list updates** tab.

To begin, search the contents of your lists to find any existing matches. Select your search parameters in the **Search lists** field,  then paste in the customer or payment instrument information that you want to find. You can include up to 1,000 entries at one time. Each entry must be on a separate line.

Any matches appear in the **Found in lists** section. This shows a summary of the key properties of the entries and the lists that they are assigned to. Any entry that isn't currently assigned to an existing list appears in the **Not found in lists** section.

To edit entries in one or both sections, select their check boxes, and then select **Bulk list actions**. This screen lets you add or remove list assignments, select expiry dates, state your reason for the change, and add comments.

### Create custom lists

You can create custom lists and add entries to them to suit specific business needs. After these lists are created, they can be used by manually created model operating points or by the [virtual fraud analyst](virtual-fraud-analyst.md). To create a custom list, select the **Custom lists** tab.

Each list that you create comprises a collection of entities that you want to screen for, such as high-priced products or high-risk countries or regions. After you create a list, enter a name and a description to summarize its contents. Then select the appropriate node and attribute, and add entries to the attribute list. *Nodes* represent essential categories of data, and *attributes* describe specific properties of those categories. Only the nodes and attributes that are relevant to the transaction payload are available in list and model operations.

For example, if you want to create a list that contains high-priced products, **Product** is the relevant node, and **SKU** is the main attribute type. To enter the individual SKUs of the highest-priced products in your inventory, paste these list items into the entry field. Each entry must be on a separate line.

After you save your new custom list, it can be viewed and edited under **Custom lists** on the **List management** page. It can also be selected when model operating points are configured.

## Model operating points

Model operating points can be configured manually or by using the guidance of the virtual fraud analyst. To create a model operating point from scratch, open the **Model operation** page, and select **Create new model operating point**.

Model operating points can be used on all transactions at the same time or just on specific subsets of transactions. For example, a model operating point can be applied only to products that are in a specific price range. To create a filter, select the appropriate node and attribute, and then select the list that contains the corresponding dataset. Up to three filters can be applied simultaneously. For example, a model operating point can be set to screen for high-priced products that are being bought only by users in high-risk countries or regions.

Continue to the next page to select the desired behavior. For example, you can reject all transactions that meet the conditions that you specify, or you can reject transactions only if they meet the specified conditions and exceed a specific risk score threshold. Name your model operating point, set its state (either active or inactive), and save it.

Any model operating point can be edited after it's created. To inactivate a model operating point, set the option to **Inactive**. To delete a model operating point, select the vertical ellipsis on the right side of the page, and then select **Delete**.
