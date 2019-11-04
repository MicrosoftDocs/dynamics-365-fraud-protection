---
author: v-davido
description: This topic explains how to manage lists and rules in Microsoft Dynamics 365 Fraud Protection.
ms.author: v-davido
ms.service: fraud-protection
ms.date: 11/04/2019

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin

title: Manage lists and rules
---

# Manage lists and rules

You can use lists and rules to help manage your purchase protection and tailor the behavior of Microsoft Dynamics 365 Fraud Protection.

*Rules* shape real-time decision making by accepting or rejecting transactions based on conditions and risk score thresholds that you select. The rules use *lists*, such as the Safe list, Block list, and custom lists of data that are relevant to your business. These capabilities help you define and screen for risky transaction types. They also help you enforce various policies, such as geofencing. These capabilities are designed to help you manage the trade-offs that are inherent when you must prevent fraud but also minimize false positives.

## List management

To manage the Safe and Block lists, and to create your own custom lists, select **List management** in the navigation.

Note that due to caching, any changes saved using the following steps may take up to two minutes to become active.

### Bulk list updates

You can add, remove, or edit large sets of information in your Safe list or Block list by using the **Bulk list updates** tab.

To begin, search the contents of your lists to find any existing matches. Select your search parameters in the **Search lists** field,  then paste in the customer or payment instrument information that you want to find. You can include up to 1,000 entries at one time. Each entry must be on a separate line.

Any matches appear in the **Found in lists** section. This shows a summary of the key properties of the entries and the lists that they are assigned to. Any entry that isn't currently assigned to an existing list appears in the **Not found in lists** section.

To edit entries in one or both sections, select their check boxes, and then select **Bulk list actions**. This screen lets you add or remove list assignments, select expiry dates, state your reason for the change, and add comments.

### Create custom lists

You can create any number of custom lists and add entries to them to suit specific business needs. After these lists are created, they can be used by manually created rules or by the [virtual fraud analyst](virtual-fraud-analyst.md). To create a custom list, select the **Custom lists** tab.

Each list that you create comprises a collection of entities that you want to screen for, such as high-priced products or high-risk countries or regions. After you create a list, enter a name and a description to summarize its contents. Then select the appropriate node and attribute, and add entries to the attribute list. *Nodes* represent essential categories of data, and *attributes* describe specific properties of those categories. Only the nodes and attributes that are relevant to the transaction payload are available in lists and rules.

For example, if you want to create a list that contains high-priced products, **Product** is the relevant node, and **SKU** is the main attribute type. To enter the individual SKUs of the highest-priced products in your inventory, paste these list items into the entry field. Each entry must be on a separate line.

The following table defines the node and attribute combinations that you can use to build your lists.

| Node | Attributes 
|---|---|
| User | Id, CountryRegion, ZipCode, Email |
| Device | DeviceType, IPAddress, IPCity, IPCountryRegion, IPState |
| Billing Address | AddressId, City, State, District, ZipCode, CountryRegion |
| Shipping Address | AddressId, Ciy, State, District, ZipCode, CountryRegion |
| PaymentInstrument | PaymentInstrumentId, MerchantPaymentInstrumentId, Type, CardType, State, HolderName, Email |
| Purchase | TotalAmount, TotalAmountInUSD, Currency |
| Product | ProductId, ProductName, Type, SKU, Category, Market, SalesPrice, COGS |

After you save your new custom list, it can be viewed and edited under **Custom lists** on the **List management** page. It can also be selected when rules are configured.

## Rules

Rules can be configured manually or by using the guidance of the virtual fraud analyst. To create a rule from scratch, open the **Rules** page, and select **Create new rule**.

Rules can be used on all transactions at the same time or just on specific subsets of transactions. For example, a rule can be applied only to products that cost certain prices. To create a filter, select the appropriate node and attribute, and then select the list that contains the corresponding dataset. Up to three filters can be applied simultaneously. For example, a rule can be set to screen for high-priced products that are being bought only by users in high-risk countries or regions.

Continue to the next page to select the desired behavior. For example, you can reject all transactions that meet the conditions that you specify, or you can reject transactions only if they meet the specified conditions and exceed a specific risk score threshold. Name your rule, set its state (either active or inactive), and save it. You can create a total of 30 rules. Note that due to caching, any changes saved may take up to two minutes to become active.

A rule can be edited after it's created. To change its settings, select it in the list, make your changes, and save. Active rules are indicated in the list with a green dot. To enable, disable, or delete a rule, select the vertical ellipsis on the right side of the page and select from the available choices. 

> [!NOTE]
> For purchase transactions, if no rules are configured yet or no configured rules reject a transaction, the default decision returned is to accept the transaction. This is not a recommendation, only a baseline intended to simplify your process when configuring new rule conditions. Once you have created rules, the decisions returned by Dynamics 365 Fraud Protection will reflect your chosen settings.
