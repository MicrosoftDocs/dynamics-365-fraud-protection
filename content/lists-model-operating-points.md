---
author: jegrif
description: Manage lists and model operating points  
ms.author: v-jegrif
ms.service: fraud-protection
ms.date: 03/28/2019

ms.topic: conceptual
title: Manage lists and model operating points  
---


# Manage lists and model operating points  

Help manage your risk decisions and tailor the behavior of Microsoft Dynamics 365 Fraud Protection with lists and model operations. 

*Model operating points* shape real-time decision-making by accepting or rejecting transactions based on your chosen conditions and risk score thresholds. The model operating points use *lists*, including the safe list, block list, and custom lists of data that are relevant to your business. With these, you can help define and screen for risky transaction types, or enforce various policies such as geofencing. These capabilities are designed to help you manage the trade-offs inherent in preventing fraud while minimizing false positives. 

## List management
To manage the Safe and Block lists and create your own custom lists, select **List management** in the navigation. 

### Bulk list updates 
Add, remove, or edit large sets of information in your Safe list or Block list with **Bulk list updates**.  

Begin by searching the contents of your lists to find any existing matches. Choose your search parameters from the **Search lists** dropdown, then paste in the customer or payment instrument information you want to find. Up to 1,000 entries can be entered at a time. Each entry must be on a separate line. 

Any matches appear under **Found in lists**, along with a summary of their key properties and their specific list assignment. Any entry not currently in an existing list appears under **Not found in lists**.  

To edit entries from either or both sections, select their checkboxes, then choose **Bulk list actions**. This screen enables you to add or remove list assignments, pick expiry dates, state your reason for the change, and add comments. 

### Create custom lists 
You can create and populate custom lists to suit specific needs. Once created, these lists can be used by manually created model operating points or by the [virtual fraud analyst](virtual-fraud-analyst.md). To create a custom list, select the **Custom lists** tab. 

Each list you create comprises a collection of entities you want to screen for, such as high-priced products or high-risk countries. Name and describe your list to summarize its contents, then select the appropriate node and attribute and populate the attribute list. *Nodes* represent essential categories of data, and *attributes* describe their specific properties. The nodes and attributes available in list and model operations are those relevant to the transaction payload.

For example, to create a list containing high-priced products, *Product* would be the relevant node and *SKU* would be the key attribute type. To enter the individual SKUs of the highest-priced products in your inventory, paste these list items into the neighboring field. Each entry must be on a separate line.

Once saved, your new custom list will be viewable and editable under **Custom lists** on the **List management** page, and can be selected when configuring model operating points. 

## Model operating points

Model operating points can be configured manually or by utilizing the guidance of the virtual fraud analyst. To create a model operating point from scratch, open the **Model operation** page and select **Create new model operating point**.

Model operating points can be used on all transactions at once or specific subsets. For instance, a model operating point could be applied only to products of a specific price range. To create a filter, select the appropriate node and attribute. Then choose your list that contains the corresponding dataset. Up to three filters can be applied simultaneously. For instance, a model operating point could be set to screen for high-priced products being bought only by users in high-risk countries.

Continue to the next screen to choose the desired behavior, such as to reject all transactions that meet your specified conditions, or to reject transactions only if they meet the conditions and cross a specific risk score threshold. Name your model operating point, set its state (active or inactive), and save.

Once created, any model operating point on this page can be edited. To deactivate, set the toggle to **Inactive**. To delete a model operating point completely, click the vertical ellipses on the right-hand side of the screen and select **Delete**. 
