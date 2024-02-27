---
author: josaw1
description: This article explains how to use activity logs in Microsoft Dynamics 365 Fraud Protection.
ms.author: cschointuch
ms.date: 02/23/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Activity Logs

---

# Activity logs

The *Activity Logs* page lets you search for and view details of who changed what and when within Microsoft Dynamics 365 Fraud Protection, based on specific filters. You can export the search results or drill into an individual activity log to show a more detailed view.
For example, you can search for all the activity logs associated with a specific environment ID and when clicking on the log, you can review the details of an individual log before and after the associated event.

> [!NOTE]
> - If the environment has child environments, the search results include logs for all the child environments. To view the environment information in the search results, use Environment name or Environment ID as search filters.

## Getting started
- Permissions: This setting is only accessible to users assigned the roles Product Admin and All Area Admin from [User roles and access](user-roles-access.md) as well as PSP Admin and Reporting roles from [Payment service provider user roles and access
](psp-user-roles.md).
- Go to Activity logs: The page is located under Settings in the left hand navigation.
- Select timeframe: Select your search timeframe. You can search between any two dates within the past 13 months.
- Filter logs by attribute: You may filter your search by one or more attributes. You can use up to five filters, with an Operator between them: In, Not in, Is empty, Is not empty, Is null and Is not null.
You can search by the following common log fields:
- Log ID: unique guid for this log entry​
- Changed by ID: ID of the user who performed the operation
- Operation type: Create, Update, Delete​...
- Timestamp: timestamp (in ISO format) of the time the rule was created
- Resource type: (environment, external call, published rules…)​
- Resource name: name of the resource (as chosen by the user)
- Resource ID: guid of the resource (decision rule)
- Assessment name: friendly name of the assessment (as of the time when operation was completed)
- Assessment ID: guid of the assessment the rule was under
- Environment name: friendly name of the env. (as of the time when operation was completed)
- Environment ID: guid of the environment the user was in

## Operation type:
<table>
    <thead>
        <tr>
            <th>Resource type</th>
            <td colspan="5">Operation type</th>
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
          <td>Transaction acceptance booster</td>
            <td>Update</td>
                 </tr>
        <tr>
           <td>Case</td>
            <td>Requeue</td>
                  </tr>
    </tbody>
</table>

## View search Activity Logs results
After you select Search, the Results tile shows all of the events that match your specified filters. By default, logs are sorted by the event date/time attribute, which is shown in your local time zone. The most recent event appears at the top of the grid. You can sort by other attributes by selecting the column title. However, only the logs that have already loaded on the results grid are sorted. By default, 100 logs are loaded on the page. As you scroll, more logs are loaded.

## Change column options
Select Column options to customize which columns are shown in the results grid. You can add or remove columns to show specific attributes, or you can drag a column to a new position. Your column settings are saved only for you, and persist if you return to the Activity logs page later. To reset your column options to the default, select Default view.

## Export activity logs
Select Export to export your search results to a comma-separated values (CSV) file on your computer. You can select one of the following export options.
- All Columns – Export all data associated with this event.
- Current Columns – Export only data in the columns that are currently shown in the grid.
> [!NOTE]
>•	Exports which exceed 10,000 rows, or take longer than two minutes to generate, are automatically canceled.

## Review individual activity logs
To explore a particular activity log in more detail, choose the event ID of the event that you want to examine. On the Activity logs details page, at the top, you can see the individual log common fields (see the"search by the following common log fields" list above). You may click on them to open a new tab and start a related quick search. On the change viewer, you can see the operation specific fields. You can copy the fields in the Change viewer by clicking on "copy original" and "copy modified" buttons. You also have the option to jump to changes using the arrows button and show all fields or just the modified ones.

## Notes panel
Notes allow your team to collaborate when reviewing event details. You can create, edit, reply, delete, and tag user's on the Notes panel attached to individual event details.

1.	To create a new note, select + New Note in the upper-right corner, enter your text in the text box, and then select the blue paper plane icon at the bottom right to publish your draft. To delete your draft, select the blue cross at the bottom right.
2.	To edit or delete a note, select the vertical ellipsis to view the menu, and select the desired command.
3.	To reply, enter your text in the "Reply" text box below the note you are replying to.
4.	To tag a user in your note, type the @ symbol followed by the user's name or email alias with tenant access. After the note is published, the tagged user receives an in-product notification.
   
You may also type hyperlinks that are clickable after they're published.

## Event Tracing:
•	You may create an event tracing subscription for your Activity logs event that shows the same fields shown on the Activity logs page using the FraudProtection.ActivityLog namespace. See the [Event tracing](event-tracing.md) page for more details.

[!INCLUDE[footer-include](includes/footer-banner.md)]

