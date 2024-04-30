---
author: cschlegel2
description: This article explains how to search for a transaction in Microsoft Dynamics 365 Fraud Protection and how you can use the search results.  We're adding a few revisions to the existing doc for how to enable search and a note on Eport Transactions.
ms.author: cschlegel
ms.date: 04/28/2024
ms.topic: how-to
search.audienceType:
  - admin
title: Search
ms.custom
---

# Search


The **Search** page helps you find and view details about events in Microsoft Dynamics 365 Fraud Protection, based on specific filter values. You can search for an individual event ID or use filters to find all transactions that match some criteria. You can export the search results or drill into an individual event to show a more detailed view.  

For example, you can search for all the events associated with the email address `kayla@contoso.com`. You can review the details for each event such as risk score, user information, and device information. You can also add the email address, or other attributes such as DeviceID or UserID, to safe or block [support lists](manage-support-lists.md). 

To search events, select the **Search** page on the left navigation. 

If your Fraud Protection instance has multiple environments, **Search for each environment** can be found by using the environment switcher on the top right of the menu bar. If the environment has child environments, the search results include transactions for all the child environments. To view the environment information in the search results, use **Environment name** or **Environment ID** in **Column options**. To limit the search results to a specific environment, use **Environment ID** as an attribute in the **Search** filter.    

> [!NOTE]
> The **Device fingerprinting** template doesn't support search. All other [Assessment templates](assessment-create-new.md#template) support search. To check if you enabled search for your assessment, go to the **Assessment configuration** setting and confirm. Search will only find transactions that are processed after you enabled the search feature for your assessment. Historical transactions that were sent before search was enabled aren't available.

> [!NOTE]  
Before you can use the “Search” feature, you need to first enable Search in the Admin Settings. Also, you need to have the ‘Product Admin’ role permissions to access the Search tab in Admin settings. ‘AllAreasAdmin’ role does not have access to enable Search. 

### How to enable the Search 
To enable the Search, follow these steps: 
1.	Sign in to the dynamics 365 fraud protection portal with your Product Admin role credentials. 
2.	Go to the settings page and select the **Search** tab. 
3.	Toggle the switch to **on** to provision Search for your DFP tenant.  
You can now use the Search feature to find and review transactions and events in Dynamics 365 Fraud Protection. You cannot turn the Search feature off once you enable it.  
 
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
> When you search on a field from a related event, only the most recent event of that type issearched. For example, if there were multiple bank events sent for a transaction, the most recent bank event is searched on.

You can add up to five filters, separated by a single **And** or **Or** condition.

### Operators
The list of available Operators can change based on the data type of the selected attribute.

- Use the operator **Equals** to find records that have the same value as the one entered for the attribute selected.

  Example: Search for payloads where the billing address city is listed as "Seattle”.

|Attribute|Operator|Value|    
|---------|---------|---------|
|(City) Billing address|Equals|Seattle|


- Use the operator **Does not equal** to find records that have a different value as the one entered for the attribute selected.

  Example: Search for payloads where the billing address city is not listed as "Seattle".

|Attribute|Operator|Value|
|---------|---------|---------|
|(City) Billing address|Does not equal|Seattle|

- Use the operator **Contains** to find records that include the value entered for the attributes selected.

  Example: Search for payloads with the product category that contains the word "Luxury".

|Attribute|Operator|Value|
|---------|---------|---------|
|Merchant product category|Contains|Luxury|

- Use the operator **Does not contain** to find records that don't include the value entered for the attributes selected.

  Example: Search for payloads with the product category that doesn't contain the word "Luxury”.

|Attribute|Operator|Value|
|---------|---------|---------|
|Merchant product category|Does not contain|Luxury|

- Use the operator **Starts with** to find records that begin with the value entered.

  Example: Search for payloads with a bank name that starts with "credit".

|Attribute|Operator|Value|
|---------|---------|---------|
|Bank name|Starts with|Credit|

- Use the operator **Ends with** to find records that finish with your search value.

  Example: Search for payloads with a bank name that ends with "Union".

|Attribute|Operator|Value|
|---------|---------|---------|
|Bank name|Ends with|Union|

- Use the operator **Is empty** to find records that have an empty value.

  Example: Search for payloads with an email that is empty.

|Attribute|Operator|
|---------|---------|
|Email|Is empty|

- Use the operator **Is not empty** to search for records without an empty value.

  Example: Search for payloads with an email that isn't empty.

|Attribute|Operator|
|---------|---------|
|Email|Is not empty|

- Use the operator **Is null** to records that aren't required on payloads and with an unknown value: 1) not on the payload or 2) with a null value.

  Example: Search for payloads where a user ID value isn't required on the payload and unknown.

|Attribute|Operator|
|---------|---------|
|User ID|Is null |

- Use the operator **Is not null** to find records with any value.

  Example: Search for payloads where a user ID value is known.

|Attribute|Operator|
|---------|---------|
|User ID|Is not null|

- Use the operator **Before** to search for records with dates prior to the date entered.

  Example: Search for payloads with a shipping date before 9/18/2023.

|Attribute|Operator|Value|
|---------|---------|---------|
|Shipping date|Before|9/18/2023|

- Use the operator **After** to search for records with date attributes that are after your date entered.

  Example: Search for payloads with a shipping date after 9/18/2023.

|Attribute|Operator|Value|
|---------|---------|---------|
|Shipping date|After|9/18/2023|

## View search results

After you select **Search**, the **Results** tile shows all of the events that match your specified filters. By default, events are sorted by the **Transaction date** attribute, which is shown in your local time zone. The most recent event appears at the top of the grid. You can sort by other attributes by selecting the column title. However, only the events that have already loaded on the results grid are sorted. By default, 100 transactions are loaded on the page. As you scroll, more transactions are loaded. 

If your results include multi-value columns, only the first value is shown. For example, if multiple payment instruments were used in a single event, the first payment instrument appears in the **Payment instrument** column.

## Change column options

Select **Column options** to customize which columns are shown in the results grid. You can add or remove columns to show specific attributes, or you can drag a column to a new position. Your column settings are  valid only for you, and persist if you return to the **Search** page later. To reset your column options to the default, select **Default view**. 

## Export transactions

> [!NOTE]  
If you do not see the exported CSV file, it is possible you may need to consent to allow pop-ups in your browser to view the export results. 

Select **Export** to export your search results to a comma-separated values (CSV) file on your computer. You can select one of the following export options.

- **All Columns** – Export all data associated with this event. This includes all attributes in the API request and API response, and any attributes from related events.  
- **Current Columns** – Export only data in the columns that are currently shown in the grid.

> [!IMPORTANT]
> Exports which exceed 10,000 rows, or take longer than two minutes, are automatically canceled. 


## Review individual events

### Event details
To drill down into a specific event, select the event ID for the event that you want to investigate. On the **Event details** page, all the information related to the specific event is displayed, including information from rule evaluation, AI scoring, and device fingerprinting. Other information is displayed, such as information sent in the assessment API request, or other related events such as bank events, chargebacks, and status or label events.

On the **Velocities** tile at the bottom of the page, values for various velocities across several different timeframes are displayed. For example, the number of purchase attempts that came from a particular email address in the last seven days is shown. You can select a velocity value to open a new tab and display the corresponding events. The velocity values on the **Event details** page are shown in real time and may have changed since the original purchase event occurred. Definitions for the default velocities are shown on the **Velocity** page.

You can also select **JSON view** in the upper right corner of the page to display the JSON API requests and responses associated with this transaction.

### Add attributes to support lists
You can apply a status of **Safe**, **Block**, or **Watch** to specific attributes such as email or IP address. To add or change a status, select the pencil icon next to the element. For more information about support lists and statuses, see [Manage support lists](manage-support-lists.md).

## Notes panel

Notes allow your team to have a rich collaboration when reviewing event details. You can create, edit, reply, delete, and tag users on the **Notes** panel attached to individual event details through **Search and Case Management**.

1. To create a new note, select **+ New Note** in the upper-right corner, enter your text in the text box, and then select the blue paper plane icon at the bottom right to publish your draft. To delete your draft, select the blue cross at the bottom right.
2. To edit or delete a note, select the vertical ellipsis to view the menu, and select the desired command.
3. To reply, enter your text in the **Reply** text box below the note you are replying to.
4. To tag a user in your note, type the **@** symbol followed by the users name or email alias with tenant access. After the note is published, the tagged user receives an in-product notification.

You may also type hyperlinks that are clickable after they're published.

### Link analysis
Select the **Link Analysis** tab to view other events that have attributes in common with the event you are currently reviewing. For example, if you select **Email**, you can view all events that were made with the same email in the selected timeframe. If you select multiple attributes, use the dropdown to specify whether you want to see events that match all the attributes you have selected, or at least one of the attributes. 

Select **Column options** to customize the fields shown in the results grid, or select **Export** to export the data into a CSV file.

To further investigate a specific pattern, select **Open in search** to open a new tab with the appropriate search filters pre-loaded. 

## Resources

[Manage support lists](manage-support-lists.md)

[Manage custom lists](lists.md)
