---
author: josaw1
description: This topic explains how to complete manual reviews in Case management for Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 03/28/2022
ms.topic: reference
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - developer
title: Case management for manual reviewers
ms.custom:
---

# Case management for manual reviewers

To complete a manual review of a case in Case management for Microsoft Dynamics 365 Fraud Protection, you must be assigned one of the following roles:

- Manual review agent
- All areas of Administrator
- All areas of Editor
- PSP Administrator
- Fraud manager
- Fraud supervisor

## View cases in a queue

In Case management, you can view all the cases that you have access to in a specific queue. To view the cases in a queue, select **View cases** on the queue's tile. The upper grid lists all the cases that are pending review, and the lower grid lists all the cases that are currently under review.

You can also select the purchase ID of a case to view the details of the transaction. For example, you can see whether the transaction is under review by another agent.

## Review a case and linked transactions

You can start a review of a case in multiple ways:

- Select **Start review** on the queue's tile.
- If you're viewing the cases in the queue, you can select **Start review** in the upper right of **Pending review** grid.
- Select the purchase ID of a case in the queue to view the details of the transaction. You will have the option to start the review from the **Transaction details** page. Additionally, if the queue that you're viewing allows for unrestricted processing, you can hover over the purchase ID of any case in the **Pending review** grid and select **Start review**.

After you select **Start review**, the **Transaction review** page appears and shows categorized details of the transaction. To have the raw data for the transaction sent to Fraud Protection, select **JSON view** in the upper-right corner of the page. On the **Link analysis** tab, you can view other transactions that are linked to the case that you're reviewing. To track the linkage, you can select one or more attributes. Use the drop-down menu to filter for transactions that match any or all of the selected attributes. To help you with your decision, select **Column options** to customize the fields that are shown. You can also export the results of linked transactions for additional analysis.

## Decisions and notes for a case

After you've reviewed the details of the transaction and are ready to make a decision about the case, select **Approve** or **Reject** in the upper-left corner of the **Transaction review** page. Based on your selection, the dialog box that appears presents a list of reason codes that you can select to support your decision. You can also add your own notes for record keeping about the transaction. These notes are associated with the transaction. Therefore, any user who searches for and views the transaction will be able to view the notes that you've added.

> [!NOTE]
> The **Transaction review** page monitors the amount of time that you spend reviewing cases. If you've been reviewing a case for 30 minutes, you receive an alert. If you're still reviewing the case, you can extend the time for another 30 minutes by selecting **Continue reviewing** in the message. If you don't make a selection in the message, the case will be sent back to the queue and made available for another agent to review.

## Add notes without reviewing a case

If you can't complete a review of a case, you can leave notes for the next reviewer.

1. Select **Notes** in the upper-right corner of the **Transaction review** page.
2. Select **Note** to add a note that will be associated with the transaction. Anyone who views the transaction in the future will be able to view this note.
3. Select **Send back to queue** to send the case back to the queue and make it available for another agent to review.
