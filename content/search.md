---
author: josaw1
description: This topic explains how to search for a transaction in Microsoft Dynamics 365 Fraud Protection and how you can use the search results.
ms.author: josaw
ms.date: 11/01/2021
ms.topic: how-to
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Search transactions
---

# Search transactions

[!include [preview banner](includes/preview-banner.md)]

Transaction search lets you search for transactions in Microsoft Dynamics 365 Fraud Protection, based on specific filter values. You can then view, export, and interact with the transactions that you find.

For example, you can find all the transactions that are associated with the email address `user@contoso.com`. You can then view detailed information about each transaction, such as the risk score, user information, and device information. Finally, you can add elements of the transactions to support lists, and apply a status such as *Block* to `user@contoso.com`.

To access transaction search, select the **Transaction search** tab on the **Purchase protection** page.

## Filter transactions

You can use various filter options to search for a specific matching transaction or multiple matching transactions. To view transactions, you must first specify a date filter and an attribute filter.

### Filter by date

Use the date filter to include transactions that occurred during a specific date range. You can search for transactions that occurred up to 13 months in the past.

### Filter by attribute

To filter transactions by an attribute, follow these steps.

1. Select an attribute to filter by (for example, **email**).
1. Enter the attribute value to filter by. You have the following options:

    - **Exact term to match** – Enter the exact term or value. For example, enter `user@contoso.com`.
    - **Prefix term to match** – Use a wildcard character (\*) to represent any character or any number of characters. For example, **user\*** returns both `user1@contoso.com` and `user22@contoso.com`.

You can add multiple attribute filters that are separated by **And** or **Or**.

## Transaction search results

After you apply your filters, the search results grid shows the matching transactions. By default, transactions are sorted by **Merchant local date** column. The most recent transaction appears at the top of the grid.

> [!IMPORTANT]
> A maximum of 300 transactions is shown. To view more results, select **Export** to create a file that contains the full set of results. For more information, see the [Export transactions](search.md#export-transactions) section later in this topic.
>
> If your results include multi-value columns, only the first value is shown. For example, if multiple payment instruments were used in a single transaction, only the first payment instrument appears in the **Payment instrument** column.

### Column options

You can add, remove, and change the order of columns in the search results grid. You can also sort by a specific column.

- To add or remove columns, select **Column options** on the command bar.
- To reorder columns, select a column, and drag it to the desired location. You can select the column in either the **Column options** pane or the search results grid.
- To sort by a column (in either ascending order or descending order), select the column name in the grid.

    > [!NOTE]
    > Only the transactions that are loaded on the screen are sorted, unless you sort by the **Merchant local date** column.

## Export transactions

To view the full list of the search results, you can export your transactions to a comma-separated values (CSV) file on your computer.

- Select **Export** next to the search results grid, and then select one of the following options:

    - **All Columns** – Export all relevant data, including information in both the application programming interface (API) request and the API response.
    - **Current Columns** – Export only data in the columns that are currently shown in the grid.

Objects that represent a list in the API schema, such as **ProductList** and **PaymentInstrumentList**, are shown as a single column.

> [!IMPORTANT]
> Each export is limited to 10,000 rows.
>
> Export operations that take longer than two minutes are automatically canceled.

## Review individual transactions

To drill down into a specific transaction, select the **Purchase ID** value for the transaction that you want to investigate.

You can apply a status of *Safe*, *Block*, or *Watch* to specific elements of the transaction. To add or change a status, select the **Edit** button (pencil symbol) next to the element. For more information about support lists and statuses, see [Manage support lists](manage-support-lists.md). To display the full API request and response for the transaction in JSON, select **Debug** on the upper right corner of the page.

## Additional resources

[Manage support lists](manage-support-lists.md)

[Manage custom lists](lists.md)
