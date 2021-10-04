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

You can take advantage of various filter options to easily find a specific transaction or multiple matching transactions. To view transactions, you must first specify a date filter and an attribute filter. 

### Filter by date

Use the **Date filter** to include transactions that occurred in a certain date range. You can search for transactions that occurred up to 13 months in the past. 

### Filter by attribute

To filter your transactions by an attribute, do the following. 

1. Select an attribute that you want to filter by (for example, "email").

1. Enter the value of this attribute that you want to filter by. The value can be one of the following: 

  - Exact term to match (eg. `user@contoso.com`) 

  - Prefix term to match, using the `*` wildcard (eg.  `user*` matches both `user1@contoso.com` and `user2@contoso.com`) 

You can add multiple attribute filters separated by **And** or **Or**.

## Transaction search results

Once filter(s) have been applied, you will see a table of matching transactions. 

Note the following: 

- A maximum of 300 transactions can be shown. If you want more results, select **Export**. For more information, see [Export transactions](search.md#export-transactions) below.

- Transactions are sorted by **Merchant local date** with the most recent at the top. 

- Only the first value of multi-value columns will be shown. For example, if multiple payment instruments were used in a single transaction, only the first will appear in the “Payment Instrument” column.  

### Column options

- Add or remove shown columns by selecting the Column Options button in the command bar. 

- Reorder columns by selecting columns and dragging, either in the Column Options panel, or on the search results grid. 

- Sort by a column (ascending or descending) by selecting a column name in the table. Note: Only the transactions loaded on the screen are sorted, unless sorting by Merchant Local Date. 

## Export transactions

You can export your transactions to a .csv file on your computer to view your data in full. 

Select **Export**, then choose one of the following options.

- **All Columns** – All data relevant to the transactions will be exported. This includes all information in both the API request and API response. 

- **Current Columns** – Only data in the columns you currently have shown will be exported. 

Note the following: 

- Exports are limited to 10,000 rows each. Export operations taking longer than 2 minutes will automatically be cancelled. 

- Objects that represent a List in the API schema (such as ProductList, PaymentInstrumentList, etc.) will be displayed as a single column. 

## Review individual transactions

You can drill down on specific transactions by selecting **Purchase ID** for the transaction in your search results that you want to investigate.

In addition to viewing information about the transaction, you can apply **Safe**, **Block**, or **Watch** status to certain elements of the transaction. To add or change a status, select the pencil icon next to the element. For more information on support lists, see [Manage support lists](manage-support-lists.md)

## Additional resources

[Manage support lists](manage-support-lists.md)

[Manage custom lists](lists.md)
