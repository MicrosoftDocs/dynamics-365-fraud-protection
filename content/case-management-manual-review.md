---
author: josaw1
description: This article explains how to complete manual reviews in Case management for Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 04/10/2024
ms.topic: reference
search.audienceType:
  - developer
title: Case management for manual reviewers
ms.custom:
---

# Case management for manual reviewers

This article explains how to complete manual reviews in Case management for Microsoft Dynamics 365 Fraud Protection.

To complete a manual review of a case in Case management for Microsoft Dynamics 365 Fraud Protection, you must be assigned one of the following roles:

- **Manual review agent**
- **Manual review fraud manager**
- **All areas administrator**
- **All areas editor** 
- **PSP administrator** (available only in payment service provider \[PSP\] environments)
- **Fraud manager** (available only in PSP environments)
- **Fraud supervisor** (available only in PSP environments)
- **Manual review agent** (available only in PSP environments)

## View cases in a queue

On the **Case management** page, you can view all the cases that you have access to in a specific queue. To view the cases in a queue, select **View cases** on the queue's tile. The upper grid lists all the cases that are pending review, and the lower grid lists all the cases that are currently under review.

You can select the purchase ID of a case to view the details of the transaction. For example, you can see whether the transaction is under review by another agent.

From the **Case management** page, you can also make bulk decisions about cases that are pending review. For more information, see the [Make bulk decisions](#make-bulk-decisions) section.

## Review a case and linked transactions

You can start a review of a case in multiple ways:

- Select **Start review** on the queue's tile.
- If you're viewing the cases in the queue, you can select **Start review** in the upper right of **Pending review** grid.
- You can also select the purchase ID of a case in the queue to view the details of the transaction. You have the option to start the review from the **Transaction details** page. If the queue that you're viewing allows for unrestricted processing, you can hover over the purchase ID of any case in the **Pending review** grid and then select **Start review**.

After you select **Start review**, the **Transaction review** page appears and shows categorized details of the transaction. To have the raw data for the transaction sent to Fraud Protection, select **JSON view** in the upper-right corner of the page. On the **Link analysis** tab, you can view other transactions that are linked to the case that you're reviewing. The **Cases in review** grid shows all transactions that are currently pending review, including cases that are being actively reviewed by other manual review agents. The lower **Decisioned cases** grid shows all linked cases that decisions have been made about. To track the linkage, you can select one or more attributes. Use the drop-down menu to filter for transactions that match any or all the selected attributes. To help with your decision, select **Column options** to customize the fields that are shown. You can export the results of linked transactions for additional analysis. You can also make bulk decisions about cases in the **Cases in review** grid. For more information, see the [Make bulk decisions](#make-bulk-decisions) section.

## Decisions and notes for a case

After you've reviewed the details of the transaction and are ready to make a decision about the case, select **Approve**, or **Reject** in the upper-left corner of the **Transaction review** page. Based on your selection, the dialog box that appears presents a list of reason codes that you can select from to support your decision. You can also add your own notes for record keeping about the transaction. These notes are associated with the transaction. Therefore, any user who searches for and views the transaction will be able to view the notes that you've added.

> [!NOTE]
> The **Transaction review** page monitors the amount of time that you spend reviewing cases. If you've been reviewing a case for 30 minutes, you'll receive an alert. If you're still reviewing the case, you can extend the time for another 30 minutes by selecting **Continue reviewing** in the message. If you don't make a selection in the message, the case will be sent back to the queue and made available for another agent to review.

## Notes panel

Notes allow your team to have a rich collaboration when reviewing event details. You can create, edit, reply, delete, and tag users on the **Notes** panel attached to individual event details through **Search and Case Management**.

1. To create a new note, select **+ New Note** in the upper-right corner, enter your text in the text box, and then select the blue paper plane icon at the bottom right to publish your draft. To delete your draft, select the blue cross at the bottom right.
2. To edit or delete a note, select the vertical ellipsis to view the menu, and select the desired command.
3. To reply, enter your text in the **Reply** text box below the note you are replying to.
4. To tag a user in your note, type the **@** symbol followed by the users name or email alias with tenant access. After the note is published, the tagged user receives an in-product notification.

You may also type hyperlinks that are clickable after they're published.

## Make bulk decisions

You can make bulk decisions in multiple ways.

- If you're viewing the cases in the queue, you can select any number of cases in the **Pending review** grid. Then select **Approve**, or **Reject** in the upper right of **Pending review** grid. Finally, select the appropriate reason, add any notes, and submit the decision.
- You can also make bulk decisions from the **Link analysis** tab. When you're reviewing a single case, you can select the **Link analysis** tab and search for linked cases. You can then select one or more cases in the **Cases in review** grid, select the appropriate decision and reason, add any notes, and submit the decision. If you select a case that is being reviewed by another manual review agent in your bulk decision, the other manual review agent will receive a notification that a decision has already been made about the case, and they won't be allowed to submit a decision. The original case can't be included in the bulk decision. You'll have to submit a decision for the original case individually by selecting the appropriate decision type at the top of the page. You can select a case in the **Decisioned cases** grid. Although you can't make another manual review decision about a decisioned case, you can make bulk decisions about linked cases that appear in the **Cases in review** grid on the **Link analysis** page of a decisioned case.   


