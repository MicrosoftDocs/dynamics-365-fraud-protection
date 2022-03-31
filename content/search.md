---
author: josaw1
description: This topic explains how to search for a transaction in Microsoft Dynamics 365 Fraud Protection and how you can use the search results.
ms.author: josaw
ms.date: 03/31/2022
ms.topic: how-to
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Search transactions
---

# Search transactions

[!include [preview banner](includes/preview-banner.md)]

The **Search** page helps you find and view details about events in Dynamics 365 Fraud Protection, based on specific filter values. You can search for an individual event ID or use filters to find all transactions that match some criteria. You can export the search results or drill into an individual event to show a more detailed view.  

For example, you can search for all the events associated with the email address 'kayla@contoso.com'. You can review the details for each event such as risk score, user information, and device information. You can also add the email address, or other attributes such as DeviceID or UserID, to safe or block [support lists](manage-support-lists.md). 

To search events, select the **Search** page on the left navigation. 

## Select event type and timeframe

First select which assessment event you want to search for: purchase, account creation, or account login. 
You can then choose the timeframe you want to search across. You can search between any two dates within the past 13 months. 
> [!NOTE]
> Search will not display events that were sent prior to the search feature being turned on. 

### Filter events by attribute

To find transactions, you must filter by one or more attributes of the transactions. You can search by attributes in the following categories.

- Attributes sent as part of the API request schema, such as information about the user, device, payment instrument (PI), or address. 
- Custom data attributes that were included in the API request.
- Fraud Protection AI scores, such as risk score and bot score, and the associated reason codes.
- Rules triggered and the decisions resulting from the rules being triggered.
- Device information returned by device fingerprinting in Fraud Protection.
- Information sent as part of related events such as bank events and chargebacks, and status and label events.
> [!NOTE]
> When you search on a field from a related event, only the most recent event of that type will be searched. For example, if there were multiple bank events sent for a transaction, the most recent bank event will be searched on.

You can add up to five filters, separated by a single **And** or **Or** condition.


## View search results

After you select **Search**, the **Results** tile shows all of the events that match your specified filters. By default, events are sorted by the **Transaction date** attribute, which is shown in your local time zone. The most recent event will appear at the top of the grid. You can sort by other attributes by selecting the column title. However, this will only sort the events that have already loaded on the results grid. By default, 100 transactions are loaded on the page. As you scroll, more transactions will be loaded. 

If your results include multi-value columns, only the first value is shown. For example, if multiple payment instruments were used in a single event, the first payment instrument appears in the **Payment instrument** column.

## Change column options

Select **Column options** to customize which columns are shown in the results grid. You can add or remove columns to show specific attributes, or you can drag a column to a new position. Your column settings are  valid only for you, and will persist if you return to the **Search** page later. To reset your column options to the default, select **Default view**. 

## Export transactions

Select **Export** to export your search results to a comma-separated values (CSV) file on your computer. You can select one of the following export options.

- **All Columns** – Export all data associated with this event. This includes all attributes in the API request and API response, and any attributes from related events.  
- **Current Columns** – Export only data in the columns that are currently shown in the grid.

> [!IMPORTANT]
> Exports which exceed 10,000 rows, or take longer than two minutes, are automatically canceled. 


## Review individual events

### Event details
To drill down into a specific event, select the event ID for the event that you want to investigate. On the **Event details** page, all the information related to the specific event will be displayed, including information from rule evaluation, AI scoring, and device fingerprinting. Other information will also be displayed, such as information sent in the assessment API request, or other related events such as bank events, chargebacks, and status or label events.

On the **Velocities** tile at the bottom of the page, values for a variety of velocities across several different timeframes are displayed. For example, the number of purchase attempts that came from a particular email address in the last seven days is shown. You can select a velocity value to open a new tab and display the corresponding events. The velocity values on the **Event details** page are shown in real time and may have changed since the original purchase event occurred. Definitions for the default velocities are shown on the **Velocity** page.

You can also select **JSON view** in the upper right corner of the page to display the JSON API requests and responses associated with this transaction.

### Add attributes to support lists
You can apply a status of **Safe**, **Block**, or **Watch** to specific attributes such as email or IP address. To add or change a status, select the pencil icon next to the element. For more information about support lists and statuses, see [Manage support lists](manage-support-lists.md).

### Add notes
Select **Notes** on the top right of the page to view or add notes to a transaction. Notes will be visible to anyone who views the transaction.

### Link analysis
Select the **Link Analysis** tab to view other events that have attributes in common with the event you are currently reviewing. For example, if you select **Email**, you can view all events that were made with the same email in the selected timeframe. If you select multiple attributes, use the dropdown to specify whether you want to see events that match all the attributes you have selected, or at least one of the attributes. 

Select **Column options** to customize the fields shown in the results grid, or select **Export** to export the data into a CSV file.

If want to further investigate a specific pattern, you can select **Open** on the **Search** page to open a new tab with the appropriate search filters pre-loaded. 

## Additional resources

[Manage support lists](manage-support-lists.md)

[Manage custom lists](lists.md)
