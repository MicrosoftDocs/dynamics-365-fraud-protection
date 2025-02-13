---
author: josaw1
description: This article describes how to use activity logs in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw1
ms.date: 03/28/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Activity Logs

---

# Activity logs

[!include[deprecation](includes/deprecation.md)]

This article describes how to use activity logs in Microsoft Dynamics 365 Fraud Protection.

The **Activity logs** page lets you search for and view details of who changed what and when within Microsoft Dynamics 365 Fraud Protection, based on specific filters. You can export the search results or select an individual activity log to show a more detailed view. For example, you can search for all the activity logs associated with a specific environment ID and then select a specific activity log to review the details of the log before and after the associated event.

> [!NOTE]
> If your environment has child environments, the search results include logs for all the child environments. To view the environment information in the search results, use the environment name or environment ID as search filters.

## Get started

- Permissions: This setting is only accessible to users assigned the Product Admin and All Area Admin roles from [User roles and access](user-roles-access.md) as well as PSP Admin and Reporting roles from [Payment service provider user roles and access](psp-user-roles.md).
- Go to the **Activity logs** page: The **Activity logs** page is located in the left navigation pane under **Settings**.
- Select timeframe: You can select your search timeframe by searching between any two dates within the past 13 months.
- Filter logs by attribute: You can filter your search by one or more attributes. You can use up to five filters, with an operator between them: **In**, **Not in**, **Is empty**, **Is not empty**, **Is null**, and **Is not null**.
- Search using common log fields:
    - Log ID: unique GUID for this log entry​.
    - Changed by ID: ID of the user who performed the operation.
    - Operation type: Create, Update, Delete​.
    - Timestamp: Timestamp (in ISO format) of the time the rule was created.
    - Resource type: For example, environment, external call, or published rules)​.
    - Resource name: Name of the resource (as chosen by the user).
    - Resource ID: GUID of the resource (decision rule).
    - Assessment name: Friendly name of the assessment (as of the time the operation completed).
    - Assessment ID: GUID of the assessment the rule was under.
    - Environment name: Friendly name of the environment (as of the time the operation completed).
    - Environment ID: GUID of the environment the user was in.

## Supported resources and operation types

<table>
    <thead>
        <tr>
          <th>Resource type</th>
          <th>Operation type</th>
        </tr>
    </thead>
    <tbody>
        <tr>
<td>Post decision action</td>
            <td>Create</td>
            <td>Update</td>
            <td>Activate</td>
           <td>Deactivate</td>
            <td>Rename</td>
          <td>Reorder</td>
            <td>Delete</td>
        </tr>
        <tr>
          <td>Decision rule</td>
            <td>Create</td>
            <td>Update</td>
            <td>Activate</td>
           <td>Deactivate</td>
            <td>Rename</td>
          <td>Reorder</td>
            <td>Delete</td>
        </tr>
        <tr>
            <td>Routing rule</td>
            <td>Create</td>
            <td>Update</td>
            <td>Activate</td>
           <td>Deactivate</td>
            <td>Rename</td>
          <td>Reorder</td>
            <td>Delete</td>
           </tr>
        <tr>
  <td>Velocity set</td>
            <td>Create</td>
            <td>Update</td>
            <td>Activate</td>
           <td>Deactivate</td>
            <td>Delete</td>
        </tr>
        <tr>
  <td>Event tracing subscription</td>
            <td>Create</td>
            <td>Update</td>
            <td>Activate</td>
           <td>Deactivate</td>
            <td>Delete</td>
        </tr>
        <tr>
          <td>Assessment</td>
            <td>Create</td>
            <td>Update</td>
            <td>Delete</td>
        </tr>
        <tr>
           <td>Custom list</td>
            <td>Create</td>
            <td>Update</td>
            <td>Delete</td>
        </tr>
        <tr>
           <td>Case management queue</td>
            <td>Create</td>
            <td>Update</td>
            <td>Delete</td>
        </tr>
        <tr>
          <td>Functions</td>
            <td>Create</td>
            <td>Update</td>
            <td>Delete</td>
        </tr>
        <tr>
          <td>External Calls</td>
            <td>Create</td>
            <td>Update</td>
            <td>Delete</td>
        </tr>
      <tr>
          <td>External Assessments</td>
            <td>Create</td>
            <td>Update</td>
            <td>Delete</td>
        </tr>
        <tr>
          <td>Transaction acceptance booster</td>
            <td>Update</td>
                 </tr>
        <tr>
           <td>Case</td>
            <td>Requeue</td>
                  </tr>
    </tbody>
</table>

## Resources not yet supported

<table>
    <thead>
        <tr>
          <th>Resource type</th>
        </tr>
    </thead>
    <tbody>
        <tr>
<td>Templates</td>
        </tr>
      <tr>
<td>Branching</td>
        </tr>
           <tr>
<td>Support list</td>
        </tr>
     <tr>
<td>Data upload</td>
        </tr>
      <tr>
<td>Notification subscription</td>
        </tr>
        <tr>
<td>Pay-as-you-go</td>
        </tr>
      <tr>
<td>User access</td>
        </tr>
           <tr>
<td>Device fingerprinting certificate setup</td>
        </tr>
     <tr>
<td>Environment management</td>
        </tr>
     <tr>
<td>Application Id creation</td>
        </tr>
      <tr>
<td>Subject request</td>
        </tr>
      <tr>
<td>Search</td>
        </tr>
      <tr>
<td>FCRA</td>
        </tr>
        <tr>
<td>Actions</td>
        </tr>
   </tbody>
</table>
      


## View search activity logs results

After you select **Search**, the **Results** tile shows all of the events that match your specified filters. By default, logs are sorted by the event date/time attribute, which is shown in your local time zone. The most recent event appears at the top of the grid. You can sort by other attributes by selecting the column title, but only logs that are already loaded on the results grid are sorted. By default, 100 logs are loaded on the page. As you scroll down, more logs are loaded.

## Change column options

Select **Column options** to customize which columns are shown in the results grid. You can add or remove columns to show specific attributes, or you can drag a column to a new position. Your column settings are saved only for you, and persist when you return to the **Activity logs** page. To reset your column options to the default, select **Default view**.

## Export activity logs

Select **Export** to export your search results to a comma-separated values (CSV) file on your computer. You can select one of the following export options.
- **All Columns** – Export all data associated with this event.
- **Current Columns** – Export only data in the columns that are currently shown in the grid.

> [!NOTE]
> Exports which exceed 10,000 rows, or take longer than two minutes to generate, are automatically canceled.

## Review individual activity logs

To examine an individual activity log in more detail, select the event ID of the event that you want to examine. At the top of the **Activity logs** details page, you can see the individual log common fields. You can select the fields to open a new tab and start a related quick search. On the change viewer, you can see the operation specific fields. You can copy the fields in the change viewer by selecting **Copy original** and **Copy modified**. You also have the options to jump to changes using the arrows, and to show all fields or just the modified ones.

## Notes pane

Notes allow your team to collaborate when reviewing event details. You can create, edit, reply, delete, and tag users on the **Notes** pane attached to individual event details.

- To create a new note, select **+ New Note** in the upper-right corner, enter your text in the text box, and then select the blue paper plane send symbol at the bottom right to publish your draft. To delete your draft, select the blue cross at the bottom right.
- To edit or delete a note, select the vertical ellipsis to view the menu, and then select the desired command.
- To reply, enter your text in the **Reply** text box below the note you're replying to.
- To tag a user in your note, type the @ symbol followed by the user's name, or an email alias with tenant access. After the note is published, the tagged user receives an in-product notification.
   
You may also enter hyperlinks that are clickable after they're published.

## Event tracing

You can create an event tracing subscription for your activity logs event that shows the same fields shown on the **Activity logs** page using the FraudProtection.ActivityLog namespace. For more information, see [Event tracing](event-tracing.md).

[!INCLUDE[footer-include](includes/footer-banner.md)]

