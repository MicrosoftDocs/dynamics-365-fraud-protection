---
author: josaw1
description: This topic explains how conduct a searche for a transaction in Microsoft Dynamics 365 Fraud Protection and how you can use the search results.
ms.author: josaw
ms.date: 10/07/2021
ms.topic: how-to
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Search transactions
---

# Search transactions

[!include [preview banner](includes/preview-banner.md)]

**Transaction search** enables you to search and find transactions in Dynamics 365 Fraud Protection based on speficic filter values. You can then view, export, and interact with those transactions. 

For example, you can find all of the transactions associated with the email address "user@contoso.com". Then, you can view detailed information about each transaction such as risk score, user information, device information, and more. Finally, you can add elements of the transactions to support lists and apply a status such as **Block** to "user@contoso.com".

To access search, select the **Transaction search** tab on the **Purchase protection** page.

## Filter transactions

You can use various filter options to find a specific transaction or multiple matching transactions. To view transactions, you must first specify a date filter and an attribute filter. 

### Filter by date

Use the **Date filter** to include transactions that occurred in a certain date range. You can search for transactions that occurred up to 13 months in the past. 

### Filter by attribute

To filter your transactions by an attribute, do the following. 

1. Select an attribute that you want to filter by (for example, "email").

1. Enter the value of this attribute that you want to filter by. The value can be one of the following: 

    - **Exact term to match** - Enter the exact term or value. For example, "user@contoso.com".

    - **Prefix term to match** - Use the "\*" wildcard to represent any or any number of characters. For example, "user\*" returns both "user1@contoso.com" and "user22@contoso.com". 

You can add multiple attribute filters separated by **And** or **Or**.

## Transaction search results

After you apply your filters, a table of matching transactions is displayed. By default, transactions are sorted by **Merchant local date**, with the most recent at the top. 

>[!IMPORTANT]
>A maximum of 300 transactions is displayed. If you want to view more results, select **Export** to create a file containing the full set of results. For more information, see [Export transactions](search.md#export-transactions) below.
>
>If your results include multi-value columns, only the first value is shown. For example, if multiple payment instruments were used in a single transaction, only the first will appear in the **Payment instrument** column.  

### Column options

You can add, remove, and change the order of columns in the search results grid. You can also sort by a specific column.

- To add or remove columns, select **Column options** in the command bar. 

- To reorder columns, select the column and drag it to the location you want. You can select the column in the **Column options** panel, or in the search results grid. 

- To sort by a column (ascending or descending order), select a column name in the grid. 
  >[!NOTE]
  >Only the transactions loaded on the screen are sorted, unless you sort by **Merchant local date**. 

## Export transactions

To view a full list of the search results, you can export your transactions to a .csv file on your computer. 

Select **Export** next to the search results grid, then choose one of the following options.

- **All Columns** – All relevant data is exported, including information in both the API request and API response. 

- **Current Columns** – Only data in the columns currently diplayed in the grid will be exported. 

Objects that represent a list in the API schema, such as ProductList and PaymentInstrumentList, are displayed as a single column. 

>[!IMPORTANT]
>Exports are limited to 10,000 rows each. 
>
>Export operations that take longer than two minutes are automatically cancelled. 


## Review individual transactions

You can drill down on specific transactions by selecting **Purchase ID** for the transaction in your search results that you want to investigate.

In addition to viewing information about the transaction, you can apply **Safe**, **Block**, or **Watch** status to certain elements of the transaction. To add or change a status, select the pencil icon next to the element. For more information on support lists, see [Manage support lists](manage-support-lists.md)

## Additional resources

[Manage support lists](manage-support-lists.md)

[Manage custom lists](lists.md)
